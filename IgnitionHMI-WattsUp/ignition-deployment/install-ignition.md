################
Install Ignition
################

Please ensure you have completed :doc:`windows-firewall` before installing Ignition.

Create Backup Location
======================
Create ``D:\Ignition\GWBKs`` folder for automated backups. If ``D:\`` doesn't exist, you may need to initialize and format the RAID array per :doc:`../../vendors/onlogic/commission`  

Install Ignition.exe
====================
#. Download the Ignition installation executable from `Inductive Automation <https://inductiveautomation.com/>`_, or move/load the executable to the desired installation computer. 

  .. note::
   
    You may not always want the latest Ignition install. The general rule of thumb is that if the latest release was in the past 2 weeks, we prefer to use the previous release. All software has bugs, especially newly released software. This avoids being the guinea pig and finding the new bugs.

#. Open the executable to run the installation wizard.
#. In the wizard, leave the default install location. Also, leave the default Gateway Service Name of ``Ignition``. This is the name of the Ignition service on the computer, such as in Windows Services control panel.

Configure Modules
=================
It's generally easiest to manage modules at install, but can also be added/removed easily later on. Licensed modules must match what our license includes in order to work. Installing modules that are not licensed could result in the :guilabel:`Reset Trial` banner to display in the Ignition gateway, and the modules could deactivate after the timer runs out.

#. Click :menuselection:`Custom`.
#. Keep the following modules checked and uncheck any not in this list:

        * Alarm Notification
        * DNP3 Driver
        * IEC 61850 Driver
        * Legacy DNP3 Driver
        * Modbus Driver
        * OPC-UA
        * Perspective
        * SQL Bridge
        * Tag Historian
        * UDP and TCP Drivers

#. Finish the wizard

Initial Configuration
=====================
#. Navigate to http://localhost:8088 where you should now see a :guilabel:`Gateway Starting` message. This can take 5-10 minutes.
#. Choose :menuselection:`Standard Installation`.
#. Use ``admin`` / ``password`` for the credentials. Your username will be overwritten when you later restore from the Golden GWBK.
#. Leave all ports at their default settings.
#. Finish the wizard and Start and Launch the Gateway.
#. Click on the :menuselection:`Config` tab and log into the gateway using the credentials you set up.

Apply License
=============
* The license is unique to this site and purchased from Inductive Automation. Reach out to `vannessa@inductiveautomation.com` and provide the list of modules above.
* The license should be accessible through the `Ignition License Portal <https://licenses.inductiveautomation.com/data/perspective/client/LicensePortal/licenses>`_.
* To apply the license, login to the Gateway and click :guilabel:`Activate Ignition` in the banner. 
* This step can be completed any time after installation and before site commissioning.
* The license persists after GWBK restoration.
