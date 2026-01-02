############################
SQL Server Automated Install
############################

This guide walks through the installation and commissioning of MSSQL software via an automated script.

Gather Files
============
#. The updated deployment files live at ``Z:\CEG\SCADA Fun\Ignition\MSSQL\2024 Automated Deployment Files``.
#. Transfer these files into the ``Downloads`` folder of your remote server. You may need to put these files on your local computer before pasting to the remote server, as you may be prevented from moving the folder directly to the remote server.

Acquire License
===============
#. Purchase ``SQL Server 2019 Standard with 5 CALs`` from directdeals.com.
#. Receive the license key and download link.
#. Place into 1Password as ``<Site> MSSQL License`` and attach the download link.

Update Configuration
====================
#. Open the deployment folder and edit ``ConfigurationFile.ini`` in notepad or another text editor.
#. Check ``SQLMAXMEMORY`` and set to 75% of available system memory.
        
        * On a 32GB machine only serving MSSQL, set to ``24576`` (24 of 32GB).
        * On a 64GB machine only serving MSSQL, set to ``49152`` (48 of 64GB).

#. Set ``SQLMINMEMORY`` to this same value.

Prepare SQL Installer
=====================
#. Download `SQL Server 2019 <https://go.microsoft.com/fwlink/?linkid=866664>`_ from Microsoft.
#. Run the download manager and choose :guilabel:`Download Media`.
#. Select :guilabel:`CAB` to download the ``.exe`` and ``.box`` files.
#. Open ``SQLServer2019-x64-ENU.exe`` which will unpack the ``.box`` file to an install folder.
#. Create folder ``D:\MSSQL`` for database files

Perform Scripted Install
========================
#. Run :guilabel:`Command Prompt` as Administrator.
#. Navigate to the install folder containing unpacked SQL install files::

        cd "C:\Users\CEGAdmin\Downloads\SQLServer2019-x64-ENU"

#. Obtain the SQL license key from 1Password. If it is not available yet, you can use another site's license and swap it out later.
#. In the command prompt copy the following command and replace variables as needed::

    setup.exe /PID="{PRODUCT_LICENSE}" /IAcceptSQLServerLicenseTerms  /SQLSYSADMINACCOUNTS="CEGAdmin" /ConfigurationFile="C:\Users\cegadmin\Downloads\2024 Automated Deployment Files\ConfigurationFile.ini" /Role="AllFeatures_WithDefaults"

For documentation on parameters in configurationfile.ini or flags in the command, visit `the Microsoft documentation <https://learn.microsoft.com/en-us/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-ver15>`_.

Example command from White Tail::

    setup.exe /PID="W49D9-9YRDQ-JTKN8-VJFC7-463JP" /IAcceptSQLServerLicenseTerms  /SQLSYSADMINACCOUNTS="CEGAdmin" /ConfigurationFile="C:\Users\cegadmin\Downloads\2024 Automated Deployment Files\ConfigurationFile.ini" /Role="AllFeatures_WithDefaults"

You will see a notice that you have provided a product key, but otherwise no output. The installer should only take a minute or two.

Install SQL Server Management Studio
====================================
This is available from a link on the front of the SQL Server installation center, but is a separate install. Download `here <https://aka.ms/ssmsfullsetup>`_.
For the installation, defaults are ok. You do not need restart the computer after installing.

Confirm Successful installation
===============================
#. Open SSMS.
#. Connect to the server. The correct credentials should be supplied and it should default to using Windows Authentication. It may be necessary to add ``encrypt=false`` to your connection string properties.
#. Click :guilabel:`New Query` in the top ribbon.
#. Enter this query: ``SELECT * FROM sys.objects;``
#. Click :guilabel:`Execute` in the top ribbon or right click in the query input area.
#. Expected output should show that the query executed successfully and the results are not empty:

.. image:: ../img/hello-sql-server.png

Create Ignition Database
========================
#. Go to your ``Automated Deployment Files`` folder.
#. Open ``SetupIgnitionDBandUser.sql``, which should open a SQL script inside SQL Server Management Studio.
#. Find the line towards the bottom that starts with ``CREATE LOGIN [ignition] WITH PASSWORD=N'password''``.
#. Copy the password from `this 1Password entry <https://start.1password.com/open/i?a=4NQ37CA7XFH4HF64NK75ZPQLYY&v=tgldcjjgrrtnjdmqlowyzk5pwy&i=djhdrchm3t4vr4fdltlifi3ene&h=my.1password.com>`_ and paste into this command.
#. You should have ``CREATE LOGIN [ignition] WITH PASSWORD=N'hereIsThePassword', DEFAULT_DATABASE=[Ignition], CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF``.
#. Save the file and click the :guilabel:`Execute` button to run the script.
#. A database named ``Ignition`` should appear under :guilabel:`<Server> > Databases` in the tree. You may need to refresh the tree.
#. After Ignition is deployed and the Gateway is configured, you can confirm that ``LocalIgnitionDB`` is connected.

Troubleshooting
===============
Can't get into the database via SSMS?

* Try using ``Windows Authentication`` instead of ``SQL Authentication/sa``
* Try adding `Encrypt=false` to your connection string parameters.

Getting the O&M Team SQL Access
===============================
O&M teams, like Radian Generation, should use their Windows credentials to authenticate with the SQL database. These are the general steps to follow:

#. Create Windows local Administrator account, if it does not exist already.
    :Username: :samp:`RadianGen`
    :Password: :samp:`{PROJ}K802!`
#. Launch SQL Server Management Studio.
#. Expand the ``Object Explorer`` tree and find ``Security > Logins`` folder. Right-click and select ``New Login``.
#. Select ``Windows authentication``.
#. Click ``Search`` and type in the name of the account.
#. Add the user to the ``sysadmin`` server role.
#. Confirm permissions match the ``ignition`` user.
#. When logging in to SSMS for the first time, you may need to check the "Trust server certificate" checkbox.

.. image:: ../img/ssms-login.png

If you have the credentials for the Windows user, you can test access to SSMS:

#. Temporarily add the user to Remote Desktop-enabled users.
#. RDP as this user & open SSMS.
#. Log in with Windows authentication.
#. Remove the user from RDP-enabled users.

Finally, provide the Windows credentials via 1Password or another secure sharing platform.
