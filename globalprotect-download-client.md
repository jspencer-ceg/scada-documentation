###########################################################
Download the GlobalProtect client installer to the firewall
###########################################################

Step 1: Ensure that the firewall is registered.
===============================================

Go to :menuselection:`Device --> Licenses`. Verify that the firewall has licenses. If not, :doc:`get licenses on the firewall <../register>`.

Step 2: Download the GlobalProtect client to the firewall
=========================================================

#. Go to :menuselection:`Device --> GlobalProtect Client` and select :guilabel:`Check Now`. If an error message appears, try :guilabel:`Check Now` again. This will download a list of available GlobalProtect versions that you can download and install.

#. Use Palo Alto's `Preferred Release Guidance`_ to choose a version of GlobalProtect. Find the row for that version in the list and select :guilabel:`Download`.

   .. _Preferred Release Guidance: https://live.paloaltonetworks.com/t5/customer-resources/pan-os-globalprotect-amp-user-id-preferred-release-guidance-from/ta-p/258304

#. If the firewall is in an HA pair, select :guilabel:`Sync to HA Peer`. Otherwise, leave it unchecked. Then, select :guilabel:`Continue Download`. A modal will appear and the download will begin. When it is finished, select :guilabel:`Close`.

#. If the download was successful, the row for the version you chose will have a check mark in the :guilabel:`Downloaded` column. In the :guilabel:`Action` column, select :guilabel:`Activate`. Confirm that you want to activate this version and select :guilabel:`Yes`. When the activation process completes, select :guilabel:`Close`. A check mark should appear in the :guilabel:`Currently Activated` column.
