##########
Namespaces
##########

What's in a Namespace? That which we call a rose, by any other Namespace would smell as sweet.
But as we all know, there's nothing rosey about defining and instantiating a complex hierarchy of UDTs in the Ignition platform.
Namespaces are a way to avoid doing that as much as possible, and make it foolproof when you have no other choice but to do so.


* Namespaces are a collection of categories such that all dynamically deployed views/UDTs that exist in any project could correctly be categorized under at least one Namespace.
* Namespaces define *what* the HMI displays and controls, but are not concerned with *how* the HMI does so.
* Namespaces serve as an interface that both the View and the UDT must satisfy, and be programmed to.


.. todo::

    Define all Namespaces and integrate them into the framework. Link to the technical definition of the Namespaces here.

Working List of Namespaces
==========================

The following pertain to so called "Inverters":

* Power Conversion System (PCS)
* PCS Control Interface
* Meter
* Step-Up Transformer
* Inverter Module
* DC Branch

To be fleshed out:

* Trackers
* Substation
* Environmental
* Network
* Some other small things


