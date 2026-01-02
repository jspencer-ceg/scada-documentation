############
Introduction
############

Most SEL relays have a sequence-of-event recorder (SER) that logs sequence-of-event (SOE) data, and have the ability to record event data with oscillography when triggered by relay protection elements. These will be referred to below as SOEs and events.

Configure the RTAC to collect SOE records and event oscillography from each SEL relay in the substation. Some relays, like the SEL-587, do not have an SER.

Event and SOE collection is available only on SEL protocol client connections.

Multiple device connections
===========================

Our goal is to have stable, trouble-free SCADA connections. Data offtakers expect the data streams to not have hiccups. When they have hiccups, we get called in to troubleshoot and that takes away our time for other things. We want to minimize this.

It is important to understand what can cause interruptions in these connections. Two things can:

* SOE and event collection can sometimes cause hiccups in SCADA data connections that are difficult to troubleshoot and avoid.

* Engineering access will pause SCADA data connections when used in direct transparent mode. Most engineering access tasks—terminal interactions, settings upload and download, and event file download—can happen with standard transparent mode. Use of the device's HMI requires the use of direct transparent mode, however.

One way to avoid SCADA data interruptions is to use multiple connections to a device. One connection will be used for the SCADA data connection, and the other connection will be used for engineering access and event collection.

Dual connections are only available in certain circumstances:

* If using Ethernet, the device must be capable of enough Telnet sessions to support both a SCADA connection and an engineering access connection. The SEL-311L can only have one Telnet session on its Ethernet ports.

* If using serial connections, the device must have two serial cables connecting it to the RTAC, or to a serial port server that the RTAC can access. By CEG convention, the port with the lower number is used for the SCADA connection, and the port with the higher number is used for the engineering access connection.

Name the SCADA connection with a ``Dev`` prefix, for example, ``Dev51F1``. Name the engineering access connection with an ``Eng`` prefix, for example, ``Eng51F1``.

If two connections are not possible, only create a device with a ``Dev`` prefix. Configure the device for both SCADA communications and event and SOE collection.

