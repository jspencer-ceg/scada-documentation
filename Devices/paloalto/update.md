###################
Update the firewall
###################

********************************
Prepare the firewall for updates
********************************

To prepare the firewall for updates, you must create policies that allow the firewall to reach the update servers. The firewall needs to reach DNS servers on the Internet to resolve FQDNs to IP addresses, and then the firewall needs to reach the update servers themselves.

Step 1. Verify that the management interface on each firewall has DNS servers configured.
=========================================================================================

#. Navigate to :menuselection:`Device --> Setup --> Services`.
#. On the :guilabel:`Services` card, verify that a :guilabel:`Primary DNS Server` and :guilabel:`Secondary DNS Server` are set.

Step 2. Verify NAT rules.
=========================

#. Navigate to :menuselection:`Policies --> NAT`. Verify that a NAT rule exists that allows the firewall's management interface to communicate with the Internet. If there are multiple ISP connections, there should be a NAT rule for each connection.

Step 3. Create address objects.
===============================

#. Navigate to :menuselection:`Objects --> Addresses`.

#. Create an address object for each firewall. For each object, select :guilabel:`Add`.

   a. Enter a :guilabel:`Name`:

         :samp:`{DEVICE_NUMBER} Management`

      Replace :samp:`{DEVICE_NUMBER}` with the device number of the firewall, for example, ``16ERFC-1A``.

   #. Ensure that :guilabel:`IP Netmask` is selected for :guilabel:`Type` and enter the IP address of the management interface, followed by ``/32``. For example, ``192.168.108.3/32``.

   #. Select :guilabel:`OK` to save the address object.

Step 4. Create an address group for each firewall.
==================================================

#. Navigate to :menuselection:`Objects --> Address Groups`.

#. :guilabel:`Add` an address object.

#. Enter a :guilabel:`Name`:

      :samp:`{FIREWALL_MODEL} Management Interfaces`

   Replace :samp:`{FIREWALL_MODEL}` with the model of the firewall, for example, ``PA-440``.

#. Select :guilabel:`Add` to add an address object for each firewall.

#. Select :guilabel:`OK`.

Step 5. Create security policies
================================

Create the following rules. Leave all settings at their defaults unless noted otherwise.

Firewalls to Internet - ICMP
----------------------------

   :Source zone: ``Management``
   :Source address: Select the address group for the firewall management interfaces.
   :Destination zone: ``Internet``
   :Applications: Select :guilabel:`icmp`, :guilabel:`ping`, and :guilabel:`traceroute`.

Firewalls to Internet - DNS
----------------------------

   :Source zone: ``Management``
   :Source address: Select the address group for the firewall management interfaces.
   :Destination zone: ``Internet``
   :Applications: :guilabel:`dns`

Firewalls to Internet - Palo Alto Updates
-----------------------------------------

   :Source zone: ``Management``
   :Source address: Select the address group for the firewall management interfaces.
   :Destination zone: ``Internet``
   :Applications: Select :guilabel:`Add` and create a new :guilabel:`Application Filter`. Name the filter ``Palo Alto Networks``. Scroll through the :guilabel:`Tags` column and select :guilabel:`Palo Alto Networks`. Select :guilabel:`OK` to save the filter.

Step 6. Commit changes.
=======================

Select :guilabel:`Commit` to commit changes to the firewall.

Step 7. Verify that the firewall can reach the update servers.
==============================================================

#. Navigate to :menuselection:`Device --> Troubleshooting`.

#. In the :guilabel:`Test Configuration` pane, set :guilabel:`Select Test` to :guilabel:`Update Server Connectivity`.

#. Select :guilabel:`Execute`. The test will run.

#. If the test is successful, the :guilabel:`Test Result` pane will list :guilabel:`Update Server is Connected`. If the test is not successful, check your configuration.

*****************
Retrieve licenses
*****************

Before updates can be installed, the firewall needs to know that it has an active license.

Step 1
======

Navigate to :menuselection:`Device --> Licenses`.

Step 2
======

Select :guilabel:`Retrieve license keys from license server`. If successful, the page will list the licenses registered to the firewall.

.. tip::

   If you get the following error:

      :guilabel:`Failed to install licenses. The device is not registered.`

   Contact the owner of the firewall and ask that the firewall be registered on the Palo Alto Customer Support Portal for their account. Send them the names of the firewalls and the serial number that belongs to each one.







Navigate to :menuselection:`Device --> Licenses` and select :guilabel:`Retrieve license keys from license server`.
