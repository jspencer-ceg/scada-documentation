################
Beckwith M-2001D
################

Step 1. Install software.
=========================

TapTalk software is used to configure the M-2001D.

.. caution ::
   The USB cable must be disconnected from the M-2001D control before installing the TapTalk software.

1. In a web browser, go to the `Beckwith Electric`_ website.

#. Go to :menuselection:`Products --> Distribution Controls`.

#. Go to :guilabel:`LTC Transformer Controls`.

#. Find the :guilabel:`M-2001D Digital Tapchanger Control` in the list and select :guilabel:`View Details`.

#. Go to the :guilabel:`Resources and downloads` tab and in the :guilabel:`Software Downloads` section, select the link :guilabel:`S-2001D - Sign in required`.

#. Select :guilabel:`Download Software`.

#. If you don't already have an account on BecoConnect, create one with your CEG email address. Otherwise, log in.

#. A ZIP file will download to your downloads folder. Extract the file. Open the extracted folder, then open successive folders until you find the TapTalkSetup file. Open it and install the software. If asked to install device software, proceed and give permission to install it.

.. _Beckwith Electric: https://www.hubbell.com/beckwithelectric/en/

Step 2. Open the software.
==========================

Find the TapTalk S-2001D (M2001D) software in the program list using the :guilabel:`Start` menu and open it.

Step X. Set up Ethernet settings.
=================================

1. Go to :menuselection:`Communication --> Setup --> Ethernet Settings`.

#. If the device has fiber Ethernet, set :guilabel:`Auto Negotiation` to :guilabel:`Disable`.

#. Set :guilabel:`DHCP Protocol` to :guilabel:`Disable`.

#. Set :guilabel:`IP Address`, :guilabel:`Net Mask`, and :guilabel:`Gateway` according to the IP address schedule.

#. Set :guilabel:`Simple Network Time Protocol` to :guilabel:`Enable`. Set the :guilabel:`IP Address` to the IP address of the primary NTP clock, usually the SEL-2488. If there is no SEL-2488, set it to the IP address of the substation RTAC.

#. Since there is no option for Daylight Saving Time, we must use UTC with this device. Set :guilabel:`Time Zone` to :guilabel:`(GMT) Greenwich Mean Time`.

#. Select :guilabel:`Save` and then select :guilabel:`Close`.

Step Y. Set up DNP.
===================

You must be online with the device to configure DNP.


