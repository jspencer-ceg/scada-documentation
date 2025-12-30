################
PA-440 Lab Setup
################

   ::todo: Change RX1501 to RX1500 throughout

Overview
========

This document describes how Nick got the lab PA-440 set up so that it can be used to test configurations for site PA-440s before they are sent to site.

The goal is to take a configuration from a site PA-440, copy it to the lab PA-440, and use the Siemens RUGGEDCOM RX1501 to simulate the site's network. One port on the RX1501 would simulate the port on the site's external switch through which the ISP connectios would be made available. That port would have subinterfaces to simulate the default router for each ISP. Another port on the RX1501 would simulate a host on the management lan to create a path to the MGT port on the PA-440. This RX1501 port would have an address on the management LAN and would be set up with a source NAT to translate an address on the SCADA lab's 172.23.216.0/24 network to an address on the site's management network.

Setup
=====

The PA-440 is set up with the following connections

+---------------+-------------+--------------------+------------------+---------------------------------------------+
| Source Device | Source Port | Destination Device | Destination Port | Purpose                                     |
+===============+=============+====================+==================+=============================================+
| PA-440        | CONSOLE     | SEL-3620           | COM 3            | Access to the console port                  |
+---------------+-------------+--------------------+------------------+---------------------------------------------+
| PA-440        | MGT         | RX1501             | 4                | Access to the MGT interface                 |
+---------------+-------------+--------------------+------------------+---------------------------------------------+
| PA-440        | 1           | RX1501             | 5                | Access to the firewall's external interface |
+---------------+-------------+--------------------+------------------+---------------------------------------------+

Console access
==============

   :IP address: ``172.23.216.2``
   :FQDN: ``fw02.lkv.scada.ceg.mn``
   :Username: ``CEG``
   :Password: ``Ceg3620!``

The SEL-3620 is set up with a port mapping that maps COM 3 to the addresses above on TCP 50603 with an SSH connection. To access the console port, set your SSH client to use either the IP address or the fully-qualified domain name (FQDN) with port 50603. On the command line, the ssh command would be::

   $ ssh -p 50603 CEG@fw02.lkv.scada.ceg.mn

When you first connect, you will see a warning like the following. To proceed, type ``yes``::

   The authenticity of host '[fw02.lkv.scada.ceg.mn]:50603 ([172.23.216.2]:50603)' can't be established.
   RSA key fingerprint is SHA256:Wt3MaFEIOQnMMldg1yy4hpVUFqpWrt1MDjZk3k1i9rE.
   This key is not known by any other names.
   Are you sure you want to continue connecting (yes/no/[fingerprint])? yes

Next, enter the password at the password prompt::

   Warning: Permanently added '[fw02.lkv.scada.ceg.mn]:50603' (RSA) to the list of known hosts.
   This system is for the use of authorized users only. Individuals using this system without authority, or in excess of their authority, are subject to having all their activities on this system monitored and recorded by system personnel. Anyone using this system expressly consents to such monitoring and is advised that if such monitoring reveals possible evidence of criminal activity, system personnel may provide the evidence of such monitoring to law enforcement officials.
   CEG@fw02.lkv.scada.ceg.mn's password:

After you enter the password, you will probably get a cursor on a blank line. Just press :kbd:`Enter` and you will see a prompt from the PA-440.

Quit your SSH client when you are done with your session. If you are on the command line, press :kbd:`Enter` and then immediately type `~.` to quit the session.

RX1501 access
=============

   :IP address: ``172.23.216.3``
   :FQDN: ``fw03.lkv.scada.ceg.mn``
   :Username: ``CEG``
   :Password: ``Ceg1500!``

PA-440 CLI
==========

Show management IP::

   > show system info





