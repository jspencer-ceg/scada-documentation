##########################
Configure Windows Firewall
##########################

By default, Windows Firewall will block access to Ignition, MSSQL, etc from another computer. Therefore it's usually necessary to create a Windows Firewall rule on a Windows computer hosting Ignition and MSSQL.
Turning off Windows Firewall is an option for troubleshooting or temporary access, but a firewall rule should be in effect otherwise.

.. note:: This is for Windows 10 IOT LTSC. Other systems such as Windows Server or Windows 11 may be slightly different.

Set Local Network Profile
=========================
#. Run PowerShell as administrator.
#. Command ``Get-NetConnectionProfile``.
#. Note the `InterfaceIndex` of the adapter you want to change. This is either the connected ethernet network, or the NIC team.
#. If this interface already has :guilabel:`NetworkCategory` = ``Private``, you do not need to change it.
#. Otherwise, command :samp:`Set-NetConnectionProfile -InterfaceIndex {InterfaceIndex} -NetworkCategory Private`
#. Command ``Get-NetConnectionProfile`` again to validate that :guilabel:`NetworkCategory` is set to ``Private``

Turn On Firewall Notifications
==============================
#. Navigate to :menuselection:`Windows Security --> Firewall & Network Protection --> Firewall Notification Settings --> Manage Notifications`
#. Scroll down to :guilabel:`Firewall & network protection notifications` and check all boxes. This will turn on notifications for firewall settings.

Add Incoming Rules for Ignition and MSSQL
=========================================
#. Navigate to :menuselection:`Windows Defender Firewall --> Advanced Settings`
#. Right click :guilabel:`Inbound Rules` and select :menuselection:`New Rule...`.
#. Select :guilabel:`Rule Type` = :menuselection:`Port` and continue.
#. Leave :guilabel:`TCP` selected and enter application specific ports and continue.

        - Ignition: ``8088, 8043, 8060``.
        - If outside hosts will connect to Ignition's OPC-UA server, then also include ``62541``.
        - MSSQL: ``1433``.

#. Ensure :guilabel:`Allow the connection` is checked, then continue.
#. For profile, leave all three checkboxes checked (Domain, Private, Public), then continue.
#. Set the name to ``Ignition Incoming`` or ``MSSQL Incoming`` and click `Finish`.

Test Access
===========
These tests should be run after MSSQL and Ignition are installed and configured.

Ignition
--------
- On a browser on another computer (test device) on the network, try navigating to :samp:`http://{IP_ADDRESS}:8088`.
- If this doesn't work, try pinging the Ignition host from the test device.

MSSQL
-----
- Open PowerShell on another device, e.g. the Ignition machine, to test connection to the SQL machine.
- Command ``tnc -ComputerName <IP or hostname> -port 1433``.

