************************************
OnLogic K802 Commissioning Procedure
************************************

.. note:: This assumes bare-metal install of Windows 10 Enterprise IoT LTSC.

.. todo:: Discussion needs to be had about using Windows 11 over Windows 10.

.. todo:: Discussion needs to be had about using Windows 11 over Windows 10.

Initial Startup
===============
Initial startup is the first time the computer is powered up, done physically onsite (e.g., in the control house or during pre-commissioning).

#. Accept the terms and conditions.
#. Turn off all options to maximize privacy.
#. Set up two accounts:

    :Username: :samp:`admin`
    :Password: :samp:`<PROJ>K802!`

    :Username: :samp:`cegadmin`
    :Password: :samp:`<PROJ>K802!`

    Replace :samp:`<PROJ>` with the short project prefix. The source of truth for this is the drawings. At the bottom right of each page there is a drawing number which starts with a ~4 letter abbreviation of the project name.

    .. todo::

      We need to flesh out step 2 but I did not encounter 'options' in the startup.

    .. note::

      It may be required to set up the second user account later via Settings > Family & other users


#. Security questions:

  :Q1: :guilabel:`What was your first pet's name?` ``Patchy``
  :Q2: :guilabel:`What is the name of the city where your parents met?` ``Lakeville`` 
  :Q3: :guilabel:`What is the name of the city you were born?` ``Aitkin``

Network
=======

Rename Ethernet Adapters
------------------------
#. Run :guilabel:`NCPA.CPL` to open adapter settings.
#. Rename adapters as :samp:`Eth {x}`.

  Replace :samp:`{x}` with the physical port number (e.g. ``Eth 1``).

Set IPv4 Settings for Adapters
------------------------------
#. Configure IP, subnet, and default gateway using project-specific information.
#. Set DNS servers to ``8.8.8.8`` and ``1.1.1.1``.

Set NIC Teaming
---------------
 
.. note:: This only applies to projects with network redundancy.

There is a more in depth discussion of this topic at `this <https://woshub.com/configure-nic-teaming-windows/>`_ webpage, including details about how to do this on other versions of Windows. Below is the preferred method, utilizing PowerShell.
 
Run PowerShell as Administrator and use the following commands:
 
#. ``Get-NetAdapter``

    View and identify active adapters, noting the `InterfaceAlias` or `Name` values.

#. :samp:`New-NetSwitchTeam -Name "{NICTeamName}" -TeamMembers "{InterfaceAlias #1}","{InterfaceAlias #2}"`

    Create the NIC team with appropriate values in quoted arguments. CEG convention is to use ``NICTeamA`` for :samp:`{NICTeamName}`. The :samp:`{InterfaceAlias}` values are from the previous step.

#. ``Get-NetSwitchTeam``

    Verify that the NIC team exists and has the correct members.

    .. image:: img/get-netswitchteam.png

.. tip::

  :samp:`Remove-NetSwitchTeam -Name {NICTeamName}` can be used to remove a NIC Team.

#. We need to set the IP info on the NICTeam now. Navigate to :menuselection:`Control Panel --> Network and Sharing --> NICTeamA --> Properties --> IPv4`
#. Configure IP, subnet, and default gateway using project-specific information.
#. Set DNS servers to ``8.8.8.8`` and ``1.1.1.1``.

Enable Ping
-----------
#. Navigate to :menuselection:`Windows Defender Firewall --> Advanced Settings --> Inbound Rules` 
#. Right click :guilabel:`File and Printer Sharing (Echo Request - ICMPv4-In)` and enable. If there are two rules with this name, make sure you enable the rule that has :guilabel:`Profile` equal to `Private, Public`
#. Right click and select :guilabel:`Properties`, then set the :guilabel:`Scope` to :guilabel:`Any IP address`

Enable Remote Desktop Access
============================

#. Navigate to :menuselection:`Remote Desktop Developer Settings` from the search bar.
#. In the `Remote Desktop` section, ensure all boxes are checked.

    a. :guilabel:`Change settings to allow remote connections to this computer`
    #. :guilabel:`Change settings to allow connections only from computers running Remote Desktop with Network Level Authentication`
    #. :guilabel:`Change settings so that the PC never goes to sleep when plugged in`
    #. :guilabel:`Change settings so that the PC never hibernates when plugged in`

#. Next to the first checkbox (referenced above), click :guilabel:`Show settings`
#. In the popup, at the bottom right, select :guilabel:`Select Users` and add the `Administrator` account.
#. Click :guilabel:`Okay` on all popups to save changes and close.
#. Click :guilabel:`Apply` below the checkboxes of the :guilabel:`Remote Desktop Developer Settings` window and exit.

Time and System Settings
========================

Adjust Time Settings
--------------------
#. Open :menuselection:`Control Panel --> Clock and Region --> Date and Time --> Internet Time tab`
#. Click ``Change Settings``, type in the ``CLK-1`` IP address and click ``Update now``
#. Set the time zone to match the site location.

Rename Computer
---------------
Rename the computer with Powershell to :samp:`{PROJ_PREFIX}-SRV-{SERVER_NUM}`, replacing :samp:`{PROJ_PREFIX}` with the short project prefix and :samp:`{SERVER_NUM}` with the server number. 
  
    e.g. ``Rename-Computer -NewName "BOOT-SRV-1"``

Ensure Non-Boot Drives are Available
------------------------------------
#. Open :guilabel:`Disk Management`.
#. If prompted, inititalize the disk and choose ``GPT (GUID Partition Table)``
#. Right-click on the disk with unallocated space, it will be the disk without the :guilabel:`Windows (C:)` label. Select ``New Simple Volume``
#. Set the ``Simple volume size`` to the maximum disk space.
#. Assign the following drive letter: :guilabel:`D`. Click Next.
#. Format the partition with the following settings and set the volume label to ``Storage``

.. image:: img/format-partition.png

The final product should look like this:

.. image:: img/final-disk-config.png

Update Power Settings
---------------------
#. Navigate to :menuselection:`Control Panel --> Hardware and Sound --> Power Options`.
#. Create a power plan called ``Never Power Down``:

    - Turn off the display: :guilabel:`Never`.
    - Put the computer to sleep: :guilabel:`Never`.

#. Adjust Advanced Power Settings:

    - Turn off hard disk after: :guilabel:`Never (0 seconds)`.

#. Set active plan to :guilabel:`Never Power Down`.
#. Adjust power button settings:

    - Power button: :guilabel:`Shut down`.
    - Sleep button: :guilabel:`Do nothing`.
    - Sleep and Hibernate: :guilabel:`Uncheck`.

Check Windows Update and BIOS Settings
--------------------------------------
To enter the BIOS, hold the :guilabel:`del` key while the machine is booting up. If the machine boots all the way into Windows, you did not get the timing right and will have to reboot and try again.

#. Enable :guilabel:`Auto Power On` in BIOS.
#. :menuselection:`Setup Utility --> Advanced --> PCH-IO --> State After G3` should be set to :guilabel:`S0 State`.
#. Return to the beginning of the menu and select :menuselection:`Continue` to boot normally.

.. todo::
  More detail needed about how to alter BIOS. Either a write up or a link to official Windows docs?
  Also, should this include info about Windows Update like the heading says?
  
Useful Software and Services
=============================
- `Firefox <https://getfirefox.com>`_
- `Wireshark <https://www.wireshark.org>`_
- Services :guilabel:`services.msc`
- Local Users and Groups Management :guilabel:`lusrmgr.msc`
- Network Connections Control Panel :guilabel:`ncpa.cpl`
- Computer Management :guilabel:`compmgmt.msc`
