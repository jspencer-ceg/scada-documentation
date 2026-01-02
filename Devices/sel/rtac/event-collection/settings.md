################################
Settings for RTAC client devices
################################

Step 1. Open the device settings.
=================================

1. Select the SEL client device that you are using for SER data and event collection from the :guilabel:`Project` pane and go to the :guilabel:`Settings` tab.

#. Select :guilabel:`Advanced Settings` on the upper-right side of the settings pane.

Step 2. Configure event collection settings.
============================================

There are two types of event report formats: CEV and COMTRADE. Most relays support COMTRADE. Configure the RTAC to collect COMTRADE reports from a relay if the relay supports it. If the relay doesn’t support COMTRADE, configure the RTAC to collect CEV event reports.

These relays do not support COMTRADE:

   * SEL-387A
   * SEL-587

1. Scroll down to the :guilabel:`Event` section of the settings.

#. Turn on event collection:

      * For CEV events, set :guilabel:`Enable Event Collection` to True.
      * For COMTRADE events, set :guilabel:`Enable Comtrade Collection` to True.

#. For COMTRADE collection, perform the following:

   a. Set :guilabel:`Connection to use when performang Comtrade Event Collection`:

         * For serial connections, select :guilabel:`Primary`.
         * For Ethernet connections, select :guilabel:`FTP`.

   #. Set :guilabel:`FTP Username for Comtrade Event Collection` to be the FTP username that is set in the relay's settings. This will usually have been left at the default value. Default values for various relays are listed in the following table. This setting will be hidden if the COMTRADE event collection connection setting is set to Primary, or if the device is using a serial or Ethernet-tunneled serial connection.


        .. list-table::
           :header-rows: 1

           * - IED Model
             - Username
           * - SEL-400 Series
             - ``ACC``
           * - SEL-311L
             - ``2AC``
           * - | SEL-311C
               | SEL-351S
               | SEL-651R
               | SEL-735
               | SEL-751
               | SEL-787
               | SEL-851
               | SEL-2411
               | SEL-2414
             - ``FTPUSER``

        .. note::
           For SEL-400 series relays, ``ACC`` is a baked-in value and cannot be changed. Other relays could have different values for these usernames. Confirm the value of the username for a particular IED by checking its ``FTPUSER`` setting. For an SEL-851, check the ``Port_02.FTP_Username`` setting.

   #. Set :guilabel:`FTP Password for Comtrade Event Collection` according to the following table. This setting will be hidden if the COMTRADE event collection connection setting is set to Primary, or if the device is using a serial or Ethernet-tunneled serial connection.

         .. list-table::
              :header-rows: 1

              * - IED Model
                - Username
              * - SEL-400 Series
                - ``Level_1``
              * - SEL-311L
                - ``Level_2``
              * - | SEL-311C
                  | SEL-351S
                  | SEL-651R
                  | SEL-735
                  | SEL-751
                  | SEL-787
                  | SEL-851
                  | SEL-2411
                  | SEL-2414
                - ``Level_1``

         .. note::
            The manuals for the SEL-787 and SEL-2411 do not specify the access level whose password is used for FTP. Nick assumes that the access level is ``Level_2``, but has not confirmed it.

#. For CEV collection, set :guilabel:`Event Collection Parameter` according to the following table:

      +-----------------+---------------+--------------------------------------------------+
      | Model           | CEV Parameter | Description                                      |
      +=================+===============+==================================================+
      | SEL-311C        | ``S128 R``    | 128 samples/cycle, LER + 1 cycle in length       |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-311L        | ``R``         | 16 samples/cycle, LER + 1 cycle in length        |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-351S        | ``S128 R``    | 128 samples/cycle, LER + 1 cycle in length       |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-387A        | ``R S64``     | 64 samples/cycle                                 |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-411L        | ``S8``        | 8 samples/cycle at full length                   |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-487B        | ``S12``       | 12 samples/cycle at full length                  |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-487E        | ``S8``        | 8 samples/cycle at full length                   |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-587         | *Leave blank* | *Unknown*                                        |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-651R        | ``S128 R``    | 128 samples/cycle, LER + 1 cycle in length       |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-735         | *Leave blank* | 16 samples/cycle                                 |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-751         | ``R``         | 32 samples/cycle                                 |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-787         | ``R``         | 16 samples/cycle                                 |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-787-2/-3/-4 | ``R``         | 32 samples/cycle                                 |
      +-----------------+---------------+--------------------------------------------------+
      | SEL-851         | *N/A*         | This relay does not support the ``CEV`` command. |
      +-----------------+---------------+--------------------------------------------------+

#. Set :guilabel:`Event Name Format` to :guilabel:`COMNAME`.

#. Set :guilabel:`COMNAME Event Name String`:

      :samp:`{STATION_ID},{DEVICE_ID},{COMPANY}`

   Replace the following:

   * :samp:`{STATION_ID}`: the name of the substation in CapitalCamelCase. Confirm your choice with Nick. :samp:`{STATION_ID}` shall be identical for each COMNAME string in the project.
   * :samp:`{DEVICE_ID}`: the device number of the IED with the device number in all caps. Include hyphons. If there is a slash in the device number, substitute an underscore (``_``).
   * :samp:`{COMPANY}`: the name of the owner in CapitalCamelCase or as an acronym. The preference is to use a short form of the owner's name. Be consistent with its use across projects. :samp:`{COMPANY}` shall be identical for each COMNAME strig in the project.

   An example of a COMNAME string would be:

      :samp:`FillmoreSolar,51-F11,NGR`




Step 3. Configure SER logging settings.
=======================================

.. note::
   The SEL-587 does not support SER data collection. Skip this step for that relay.

1. *For RTAC firmware versions R155 and above, or R201 and above:* Set :guilabel:`Enable ASCII SER Logging` to :guilabel:`True`.

#. Set :guilabel:`ASCII SER Logging Collection Period` to ``300000``, for SER logging collection every five minutes.

Step 4. Set a GUID.
===================

A *globally unique identifier* (GUID) is, for us, a globally unique name for a relay. A traditional GUID, or sometimes, a *universally unique identifier* (UUID), is a 128-bit number. We use a more human-readable identifier, in the form of a *fully qualified domain name* (FQDN). FQDNs are globally unique if used with a registered *top-level domain name* (TLD), such as one of the TLDs that CEG owns, :samp:`ceg.mn`.

In the :guilabel:`General` section of the RTAC device settings, set :guilabel:`Device GUID`:

   :samp:`{DEVICE_NUMBER}.{PROJECT_PREFIX}.scada.ceg.mn`

Replace the follewing:

   * :samp:`{DEVICE_NUMBER}`: the device number in all caps, as it appears on the one-line drawings, with hyphens if it has any. If there is a slash in the device number, replace it with an underscore (:samp:`_`).

   * :samp:`{PROJECT_PREFIX}`: the project's prefix in lowercase.

Example GUIDs:

* 51-H1 relay at Hornshadow: :samp:`51-H1.horn.scada.ceg.mn`

* ETM/T1, the ETM for TR1, at Assembly: :samp:`ETM_TR1.asmb.scada.ceg.mn`

Step 5. Assign a Virtual Port Number.
=====================================

In the :guilabel:`SEL` section of the RTAC device settings, set the :guilabel:`Virtual Port Number`. See the `RTAC Programming Style Guide`_ in ClickUp for instructions on how to assign a Virtual Port Number.

.. _RTAC Programming Style Guide: https://app.clickup.com/8453910/v/dc/81zrp-6600/81zrp-900
