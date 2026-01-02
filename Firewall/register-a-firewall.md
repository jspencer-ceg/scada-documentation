###################
Register a firewall
###################

There are two ways to register a firewall:

* Ask the owner or managed service provider (MSP) to register it
* Register it yourself using the Palo Alto Customer Support Portal

Option 1: Ask the owner or MSP to register the firewall
=======================================================

#. Ask the owner or MSP to register the firewall for you. Give them:

   * The site name
   * The device number for the firewall. The device number should have an A or B at the end of it to denote if it's the primary or secondary firewall if it's in an HA pair.
   * The device's serial number. You can find the serial number by going to the :guilabel:`Dashboard` and looking in the :guilabel:`General Information` section.

   If you are working with Radian, email `Cristian Pinto`_ with this information.

   .. _Cristian Pinto: mailto:cristian.pinto@radiangen.com

#. After receiving confirmation that the firewall has been registered, log into the firewall. Go to :menuselection:`Device --> Licenses` and select :guilabel:`Retrieve license keys from license server`. You should see the licenses show up.

Option 2: Register the firewall yourself
========================================

Choose this option if CEG purchased the firewall for a project.


1. Navigate to the `Palo Alto Customer Support Portal`_.

   .. _Palo Alto Customer Support Portal: support.paloaltonetworks.com

#. Click :guilabel:`Sign in` underneath:

   * I need to register a new asset
   * I want to manage my assets
   * I need to create or manage a support case

   Log in.

#. From the :guilabel:`Account Selector`, select the account to which you want to register the firewall.

#. Navigate to :menuselection:`Products --> Assets`. Select :guilabel:`Account Actions` and select :guilabel:`Register Product`.

#. Select :guilabel:`Register device using Serial Number` and select :guilabel:`Next`.

#. Enter :guilabel:`Serial Number`, :guilabel:`Device Name` (project name and device number), and the address of the firewall. Use an address of an O&M building or an office where packages can be received.

#. The next step will ask if you would like to run a Day 1 Configuration. Select :guilabel:`Skip this step`.

#. On the firewall, navigate to :menuselection:`Device --> Licenses` and select :guilabel:`Retrieve license keys from license server`. You should see the licenses show up.

