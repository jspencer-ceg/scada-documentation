##############################
Event and SOE collection setup
##############################




************************
Configure SOE collection
************************

.. note::
   The SEL-587 does not support SOE collection. For that relay, skip this section.

1. Select an SEL client device from the :guilabel:`Project` pane and go to to the :guilabel:`POU Pin Settings` tab.

#. Set :guilabel:`Enable_ASCII_SER_Logging` to :guilabel:`True` in the :guilabel:`Default Value` column.

#. Go to to the :guilabel:`Settings` tab and select :guilabel:`Advanced Settings`.

#. Configure or confirm the following settings in the :guilabel:`Event` section. Values in **bold** are non-default values.

   +-------------------------------------+------------+
   | Setting                             | Value      |
   +=====================================+============+
   | ASCII SER Logging Command Parameter | 100        |
   +-------------------------------------+------------+
   | ASCII SER Logging Date Format       | MDY        |
   +-------------------------------------+------------+
   | ASCII SER Logging Collection Period | **300000** |
   +-------------------------------------+------------+
   | ASCII SER Logging Severity Level    | Debug      |
   +-------------------------------------+------------+
   | Adjust ASCII SER Logging Timestamps | False      |
   +-------------------------------------+------------+

#. In the :guilabel:`General` section, :ref:`device-guid`, below.

**************************
Configure event collection
**************************

There are two types of event report formats: CEV and COMTRADE. Most relays support COMTRADE. Configure the RTAC to collect COMTRADE reports from a relay if the relay supports it. If the relay doesn't support COMTRADE, configure the RTAC to collect CEV event reports.

1. Select an SEL client device from the :guilabel:`Project` pane and navigate to the :guilabel:`POU Pin Settings` tab.

#. Set :guilabel:`Enable_New_Event_Filtering` to :guilabel:`True`.

#. Navigate to the :guilabel:`Settings` tab and check the :guilabel:`Advanced Settings` checkbox.

#. Navigate to the :guilabel:`Event` section of the settings.

#. Turn on event collection:

   * For CEV events, set :guilabel:`Enable Event Collection` to :guilabel:`True`.
   * For COMTRADE events, set :guilabel:`Enable Comtrade Collection` to :guilabel:`True`.

#. For COMTRADE connections:

   a. Set :guilabel:`Connection to use when performing Comtrade Event Collection`:

      * For serial connections, select :guilabel:`Primary`.
      * For Ethernet connections, select :guilabel:`FTP`.

   #. Set :guilabel:`FTP Username for Comtrade Event Collection` to be the FTP username that is set in the relay's settings. This will usually be left at the default value. Default values for various relays are:

      +----------------+-------------+
      | IED Model      | Username    |
      +================+=============+
      | SEL-400 Series | ``ACC``     |
      +----------------+-------------+
      | SEL-311L       | ``2AC``     |
      +----------------+-------------+
      | SEL-311C       | ``FTPUSER`` |
      | SEL-351S       |             |
      | SEL-651R       |             |
      | SEL-735        |             |
      | SEL-751        |             |
      | SEL-787        |             |
      | SEL-851        |             |
      | SEL-2411       |             |
      | SEL-2414       |             |
      +----------------+-------------+

      .. note::
         For SEL-400 series relays, ``ACC`` is a baked-in value and cannot be changed. Other relays could have different values for these usernames. Confirm the value of the username for a particular IED by checking its ``FTPUSER`` setting. For an SEL-851, check the ``Port_02.FTP_Username`` setting.

   #. Set :guilabel:`FTP Password for Comtrade Event Collection` according to the following table. This setting will be hidden if the COMTRADE event collection connection setting is set to Primary, or if the device is using a serial or Ethernet-tunneled serial connection.

      +----------------+--------------+
      | IED Model      | Access Level |
      +================+==============+
      | SEL-400 Series | Level_1      |
      +----------------+--------------+
      | SEL-311L       | Level_2      |
      +----------------+--------------+
      | SEL-311C       | Level_2      |
      | SEL-351S       |              |
      | SEL-651R       |              |
      | SEL-735        |              |
      | SEL-751        |              |
      | SEL-787        |              |
      | SEL-851        |              |
      | SEL-2411       |              |
      | SEL-2414       |              |
      +----------------+--------------+

      .. note::
         The manuals for the SEL-787 and SEL-2411 do not specify the access level whose password is used for FTP. Nick assumes that the access level is Level_2, but has not confirmed it.

   #. Set 

.. _device-guid:

*****************
Set a device GUID
*****************

1. Select an SEL client device from the :guilabel:`Project` pane and navigate to the  :guilabel:`Settings` tab. Check the :guilabel:`Advanced Settings` checkbox near the top-right corner of the screen.

#. In the :guilabel:`General` section of the settings, enter a :guilabel:`Device GUID` in the following format:

   :samp:`{DEVICE_NUMBER}.{PROJECT_SLUG}.scada.ceg.mn`

   Replace:

   * :samp:`{DEVICE_NUMBER}` with the device number in ALL CAPS. Type the device number as it would appear on the one-line diagram and include hyphens, but if there is a slash in the device number, replace it with an underscore (``_``).
   * :samp:`{PROJECT_SLUG}` with the project's name slug in lowercase.

