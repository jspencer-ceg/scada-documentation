#################
Configure Gateway
#################

All items on this page are within the gateway configuration portal, accessed via web browser at ``localhost:8088`` or over the network at :samp:`{IGNITION_HOST_IP}:8088`.

Restore From Golden GWBK
========================
.. important:: This process should only be done once per site, because it will override everything on the gateway.

#. Navigate to :menuselection:`Config --> System --> Backup/Restore`.
#. If we are recommissioning this site for some reason, click :guilabel:`Download Backup` to get an as-found gateway backup. This is best practice whenever pushing major changes, since there could be unforeseen consequences with a full restore.
#. On the :guilabel:`Restore` tab:
        
        #. Check :guilabel:`Overwrite Gateway Name`.
        #. Set :guilabel:`New Gateway Name` as the machine hostname. e.g. ``SALT-SRV-2``
        #. Browse for the latest ``.gwbk`` file at ``Z:\CEG\SCADA Fun\Ignition\Golden GWBK`` 
        #. Load it.

#. Once this is complete, the gateway will restart. Credentials will then be from the identity provider in the Gateway backup (details not posted here). It includes a standard list of SCADA team members.

If you need to reset the credentials in the Gateway, follow these steps:

#. Navigate to the Ignition installation directory: ``C:\Program Files\Inductive Automation\Ignition``
#. Reset the credentials with ``gwcmd.bat -p``
#. Restart the Gateway with ``gwcmd.bat -r``
#. Navigate to the Gateway URL and set temporary credentials.

Change Gateway Name
===================
This setting should be changed early in the setup process, then never altered once the site is setup. Consult Matt Steele if you need to change this later so we can test for potential impacts first.

#. Navigate to :menuselection:`Config --> System --> Gateway Settings`
#. Click the pencil to edit the :guilabel:`System Name`
#. Accept the warning message, assuming this is a change during initial site setup.
#. Update the system name to match the device name of the host (e.g. ``GRN-SRV-02``).

Adjust Memory Parameters for Ignition
=====================================
The default from the Golden Gateway backup is 2GB. It should be changed to about half of the available RAM on the Ignition server. This is flexible and can be set to higher.

#. Log in to the Ignition server.
#. Open a command prompt as Administrator.
#. Navigate to ``C:\Program Files\Inductive Automation\Ignition\data``
#. Run ``notepad ignition.conf`` to launch the config file in Notepad.
#. Change the ``wrapper.java.initmemory`` and ``wrapper.java.maxmemory`` settings to the appropriate amount and save the file.
#. Change directories up one level.
#. Restart the Gateway with ``gwcmd.bat -r``
#. Confirm the new memory limits in the Gateway under :menuselection:`Status`.


Update CEG SCADA Credentials
============================
#. Navigate to :menuselection:`Config --> Security --> Users, Roles`
#. Find :guilabel:`default` user source and navigate to :menuselection:`More --> manage users`
#. Update the passwords for these three users: 

    +-------------+---------------------+---------------+
    | Username    | Password            | Role          |
    +=============+=====================+===============+
    | ceguser     | ``{PROJ}K802!``     | ReadOnly      |
    +-------------+---------------------+---------------+
    | cegoperator | ``{PROJ}K802!``     | Operator      |
    +-------------+---------------------+---------------+
    | cegadmin    | ``{PROJ}AdminK802!``| Administrator |
    +-------------+---------------------+---------------+

#. Add these three users to the ``Shared`` 1Password vault. Format the title like ``Site Name Ignition`` and add the Gateway URL as a website.
#. The last step is to enable the :guilabel:`default` user source. Navigate to :menuselection:`Config --> Security --> General` and set the ``System Identity Provider`` and the ``System User Source`` to :guilabel:`default`

Configure Database Connection
=============================
#. Navigate to :menuselection:`Config > Databases > Connections`.
#. Create a database connection named ``LocalIgnitionDB`` if it does not already exist.
#. For the :guilabel:`JDBC Driver`, select :guilabel:`Microsoft SQLServer`
#. The :guilabel:`Connect URL` should replace ``localhost`` with the IP address or domain name of the SQL host.
#. Username will be ``Ignition`` with the password from `this 1Password entry <https://start.1password.com/open/i?a=4NQ37CA7XFH4HF64NK75ZPQLYY&v=tgldcjjgrrtnjdmqlowyzk5pwy&i=djhdrchm3t4vr4fdltlifi3ene&h=my.1password.com>`_ , which was used during the :doc:`../database-deployment/sql-server-install` procedure.
#. :guilabel:`Extra Connection Properties` shall be ``databaseName=Ignition`` assuming the database was set up according to the docs.

Troubleshooting
---------------
Unable to get a valid connection? Newer Microsoft JDBC drivers changed the default encryption flag.
Under :guilabel:`Extra Connection Properties`, add a parameter to change the encryption flag back to false: ``databaseName=Ignition;encrypt=false``

Configure Tag Providers
=======================

Realtime Tag Provider
---------------------
#. Navigate to :menuselection:`Config --> Tags --> Realtime` and edit the :guilabel:`SiteName` tag provider.
#. Change :guilabel:`SiteName` to ``SiteNameSolar``, using the actual project name without spaces, e.g. ``KimmelRoadSolar``
#. Ensure default database for the tag provider is ``LocalIgnitionDB``
#. Save.

Historical Tag Provider
-----------------------
This should be created automatically when you create the database connection. Ensure it exists and is enabled.

Configure Alarm Journal Profile
===============================
#. Navigate to :menuselection:`Config --> Alarming --> Journal`
#. There should already be an Alarm Journal named ``LocalAlarmJournal``. If so, ensure it is configured according to the below steps.
#. If there is not already an Alarm Journal, create it. Click the :guilabel:`Create a new Alarm Journal Profile` link and choose :guilabel:`Database`
#. Name it ``LocalAlarmJournal``
#. Under the :guilabel:`Events` header, change :guilabel:`Minimum Priority` from ``Low`` to ``Diagnostic``
#. Leave the defaults for other fields, and save.

Install Custom Modules
======================
Modules are imported as ``.modl`` files. Copies of the custom modules live at ``Z:/CEG/CEG/SCADA Fun/Ignition/Golden GWBK/Modules``.

#. Navigate to :menuselection:`Config --> Modules` where you should see the standard modules already installed.
#. Scroll down and click :guilabel:`Install or Upgrade a Module` at the bottom.
#. Install the following custom modules:
    
    * `Advanced Modbus Driver <https://forum.inductiveautomation.com/t/automation-professionals-advanced-modbus-driver/41312>`_ (Automation Professionals LLC)
    * `Integration Toolkit <https://forum.inductiveautomation.com/t/automation-professionals-integration-toolkit-module/74934>`_ (Automation Professionals LLC)
    * `Apex Charts Components <https://forum.inductiveautomation.com/t/kyvislabs-apexchart-module/55263>`_ (Kyvis Labs)

#. Ensure that the modules are licensed. If they are not, the :guilabel:`License Incomplete` banner will appear at the top of the webpage. Reach out to Phil Turmel at ``pturmel@automation-pros.com`` to request a license for the Advanced Modbus Driver.

Verify OPC UA Settings
======================
#. Navigate to :menuselection:`Config --> OPC UA --> Server Settings`
#. Bind Port: ``62541``
#. Bind Addresses: ``0.0.0.0``
#. Endpoint Addresses: ``<hostname>,<localhost>, 192.168.118.27`` (replace with Ignition IP for site).
#. Security Policies: ``Basic256Sha256``

Verify Server Certificate Setup
===================================
#. Navigate to :menuselection:`Config --> OPC UA --> Security --> Certificates`
#. Download and open the ``Server`` certificate.
#. Check the ``Subject Alternative Name`` under the :menuselection:`Details` tab.
#. Verify this information is correct for the site such as IP, hostname, etc.
#. If not, regenerate the ``Server`` certificate with the correct information.
    #. First, note the fingerprint and expiration date of the ``Client`` certificate.
    #. Then, navigate to :menuselection:`Server Certificate -> Regenerate`
    #. DNS name: ``<Ignition server Name>``
    #. IP Addresses: ``<Ignition IP Address>, 127.0.0.1``
    #. Crossroads Example
        #. DNS name: ``CSRD-SRV-3``
        #. IP Addresses: ``192.168.122.68, 127.0.0.1``
    #. Regenerate the server certificate.
    #. Observe a new client certificate created.
    #. Delete old ``Client`` certificate after verifying the fingerprint and expiration date.
    #. Restart OPC Module
        #. Do not do this during production!
        #. :menuselection:`Config -> Modules`
        #. Restart the ``OPC-UA`` module
