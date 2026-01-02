###############
Device settings
###############

You must configure a device's settings to prepare it for having its SOE and events collected by the RTAC.

.. todo ::

   * Say that you need to set up time correctly. But understand if this is really necessary and how it affects the time stamping of events and SOEs.
   * Reference the SCADA relay settings guide as the source of truth.

On each device, deternmine the port that will be used for SOE and event collection. Configure the following settings on that port:

* Enable Telnet, if it is an Ethernet port.
* Enable SEL Protocol, if it is a serial port.
* Enable Auto Messages. This allows a device to send an unsolicited message to the RTAC as soon as an event occurs so that the event report can be retrieved as soon as possible.
* Enable RTS/CTS, if it is a serial port. This improves the reliability of the connection.
* Enable and configure FTP, if it is an Ethernet port and if the device supports it. This allows the RTAC to use FTP instead of SEL Protocol to collect event reports. This is especially useful if the SCADA data and engineering access connections cannot be separate, as the event collection and SCADA data do not have to share the same connection.

Each IED has a slightly different way of doing this. The settings below are only a subset of the settings needed for a complete SCADA implementation. They only show the settings that are essential or desired for event and SOE collection.

SEL-311L relays
===============

:menuselection:`Global --> General`

+--------------+---------------------+---------+
| Setting Name | Setting Description | Setting |
+==============+=====================+=========+
| DATE_F       | Date Format         | MDY     |
+--------------+---------------------+---------+

Ethernet connection
-------------------

:menuselection:`Port 5 --> Communications`

+--------------+----------------------------+------------+
| Setting Name | Setting Description        | Setting    |
+==============+============================+============+
| ETELNET      | Enable Telnet              | Y          |
+--------------+----------------------------+------------+
| EFTPSERV     | Enable FTP Server          | Y          |
+--------------+----------------------------+------------+
| FTPUSER      | FTP User Name              | 2AC        |
+--------------+----------------------------+------------+
| FTPCBAN      | FTP Connect Banner         | FTP SERVER |
+--------------+----------------------------+------------+
| FTPIDLE      | FTP Idle Timeout (minutes) | 5          |
+--------------+----------------------------+------------+

Serial connection
-----------------

Replace **N** with the number of the port being used.

:menuselection:`Port N --> Communications`

+--------------+-----------------------------+---------+
| Setting Name | Setting Description         | Setting |
+==============+=============================+=========+
| PROTO        | Protocol                    | SEL     |
+--------------+-----------------------------+---------+
| AUTO         | Send Auto Messages to Port  | Y       |
+--------------+-----------------------------+---------+
| RTSCTS       | Enable Hardware Handshaking | Y       |
+--------------+-----------------------------+---------+

SEL-351S relays
===============

:menuselection:`Global --> General`

+--------------+---------------------+---------+
| Setting Name | Setting Description | Setting |
+==============+=====================+=========+
| DATE_F       | Date Format         | MDY     |
+--------------+---------------------+---------+

:menuselection:`Global --> Time and Date Management Settings`

+--------------+--------------------------------+------------------------------------------------------------+
| Setting Name | Setting Description            | Setting                                                    |
+==============+================================+============================================================+
| IRIGC        | IRIG-B Control Bits Definition | C37.118                                                    |
+--------------+--------------------------------+------------------------------------------------------------+
| UTC_OFF      | Offset from UTC (hr)           | *Set according to the project's time zone*                 |
+--------------+--------------------------------+------------------------------------------------------------+
| DST_BEGM     | Month to Begin DST             | 3 *(Set to NA if the project's area does not observe DST)* |
+--------------+--------------------------------+------------------------------------------------------------+
| DST_BEGD     | Day of the Week to Begin DST   | SUN                                                        |
+--------------+--------------------------------+------------------------------------------------------------+
| DST_BEGH     | Local Hour to Begin DST        | 2                                                          |
+--------------+--------------------------------+------------------------------------------------------------+
| DST_ENDM     | Month to End DST               | 11                                                         |
+--------------+--------------------------------+------------------------------------------------------------+
| DST_ENDW     | Week of the Month to End DST   | 1                                                          |
+--------------+--------------------------------+------------------------------------------------------------+
| DST_ENDD     | Day of the Week to End DST     | SUN                                                        |
+--------------+--------------------------------+------------------------------------------------------------+
| DST_ENDH     | Local Hour to End DST          | 2                                                          |
+--------------+--------------------------------+------------------------------------------------------------+


Ethernet connection
-------------------

:menuselection:`Port 5 --> Ethernet Port Settings`

+--------------+----------------------------+------------+
| Setting Name | Setting Description        | Setting    |
+==============+============================+============+
| ETELNET      | Enable Telnet              | Y          |
+--------------+----------------------------+------------+
| TPORT        | Telnet Port                | 23         |
+--------------+----------------------------+------------+
| AUTO         | Send Auto Messages to Port | Y          |
+--------------+----------------------------+------------+
| EFTPSERV     | Enable FTP                 | Y          |
+--------------+----------------------------+------------+
| FTPUSER      | FTP User Name              | FTPUSER    |
+--------------+----------------------------+------------+
| FTPCBAN      | FTP Connect Banner         | FTP SERVER |
+--------------+----------------------------+------------+
| FTPIDLE      | FTP Idle Timeout (min)     | 5          |
+--------------+----------------------------+------------+

Serial connection
-----------------

Replace **N** with the number of the port being used.

:menuselection:`Port N --> Protocol Selection`

+--------------+---------------------+---------+
| Setting Name | Setting Description | Setting |
+==============+=====================+=========+
| PROTO        | Protocol            | SEL     |
+--------------+---------------------+---------+

:menuselection:`Port N --> Communications`

+--------------+-----------------------------+---------+
| Setting Name | Setting Description         | Setting |
+==============+=============================+=========+
| RTSCTS       | Enable Hardware Handshaking | Y       |
+--------------+-----------------------------+---------+
| AUTO         | Send Auto Messages to Port  | Y       |
+--------------+-----------------------------+---------+

SEL-387A relays
===============

:menuselection:`Global --> Relay Settings`

+--------------+---------------------+---------+
| Setting Name | Setting Description | Setting |
+==============+=====================+=========+
| DATE_F       | Date Format         | MDY     |
+--------------+---------------------+---------+

Serial connection
-----------------

Replace **N** with the number of the port being used.

:menuselection:`Port N`

+--------------+-----------------------------+---------+
| Setting Name | Setting Description         | Setting |
+==============+=============================+=========+
| PROTO        | Protocol                    | SEL     |
+--------------+-----------------------------+---------+
| AUTO         | Send Auto Messages to Port  | Y       |
+--------------+-----------------------------+---------+
| RTSCTS       | Enable Hardware Handshaking | Y       |
+--------------+-----------------------------+---------+

SEL-400 series relays
=====================

These settings apply to all relays in the SEL-400 series, including the SEL-411L, SEL-451, SEL-487E, and SEL-487V. Settings pages may contain more settings than listed in these tables. Only the settings listed here are relevant to event and SOE collection.

:menuselection:`Global --> Time and Date Management`

+--------------+--------------------------------+-------------------------------------------------------------------+
| Setting Name | Setting Description            | Setting                                                           |
+==============+================================+===================================================================+
| DATE_F       | Date Format                    | MDY                                                               |
+--------------+--------------------------------+-------------------------------------------------------------------+
| IRIGC        | IRIG-B Control Bits Definition | C37.118                                                           |
+--------------+--------------------------------+-------------------------------------------------------------------+
| UTCOFF       | Offset from UTC to Local Time  | *Set according to the project's time zone*                        |
+--------------+--------------------------------+-------------------------------------------------------------------+
| BEG_DST      | Begin DST                      | 2,2,1,3 *(Set to OFF if the project's area does not observe DST)* |
+--------------+--------------------------------+-------------------------------------------------------------------+
| END_DST      | End DST                        | 2,1,1,11 *(Hidden if BEG_DST = OFF)*                              |
+--------------+--------------------------------+-------------------------------------------------------------------+

Ethernet connection
-------------------

:menuselection:`Port --> Port 5 --> SEL Protocol`

+--------------+----------------------------+---------+
| Setting Name | Setting Description        | Setting |
+==============+============================+=========+
| AUTO         | Send Auto-Messages to Port | Y       |
+--------------+----------------------------+---------+

:menuselection:`Port --> Port 5 --> FTP Configuration`

+--------------+-----------------------------+-------------------------------------+
| Setting Name | Setting Description         | Setting                             |
+==============+=============================+=====================================+
| FTPSERV      | Enable FTP Server           | Y                                   |
+--------------+-----------------------------+-------------------------------------+
| FTPCBAN      | FTP Connect Banner          | FTP SERVER:                         |
+--------------+-----------------------------+-------------------------------------+
| FTPIDLE      | FTP Idle Time-Out (mins)    | 5                                   |
+--------------+-----------------------------+-------------------------------------+
| FTPANMS      | Enable Anonymous FTP Login  | N                                   |
+--------------+-----------------------------+-------------------------------------+
| FTPAUSR      | Anonymous User Access Level | 0 *(Setting hidden if FTPANMS = N)* |
+--------------+-----------------------------+-------------------------------------+

Serial connection
-----------------

Replace **N** with the number of the port being used.

:menuselection:`Port Settings --> Port N`

+--------------+-----------------------------+---------+
| Setting Name | Setting Description         | Setting |
+==============+=============================+=========+
| EPORT        | Enable Port                 | Y       |
+--------------+-----------------------------+---------+
| PROTO        | Protocol                    | SEL     |
+--------------+-----------------------------+---------+
| RTSCTS       | Enable Hardware Handshaking | Y       |
+--------------+-----------------------------+---------+

:menuselection:`Port --> Port N --> SEL Protocol`

+--------------+----------------------------+---------+
| Setting Name | Setting Description        | Setting |
+==============+============================+=========+
| AUTO         | Send Auto-Messages to Port | Y       |
+--------------+----------------------------+---------+

