####################################
Configure Site-Specific HMI Elements
####################################

Each site is unique and requires some work to tailor our HMI accordingly. The oneline diagram screen is crucial for site operators to monitor substation status and control equipment. This page will detail how to set up a oneline diagram for a new site.

Creating the Oneline Diagram
============================
Prerequisites
-------------
1. Understand what a oneline diagram is 
    .. todo:: insert video or other resource
#. Understand basic substation components. `This Wikipedia page for ANSI standards <https://en.wikipedia.org/wiki/ANSI_device_numbersis/>`_ is helpful to reference substation equipment names and prefixes.
#. Get familiar with our :doc:`./ignition-development`, including using the Dev server and deploying to Prod sites.
#. Create substation tags for this site following the procedure in :doc:`./create-tags`. Work with the PPC engineer to make sure they are reporting accurately.

Initial Setup
-------------
* Work with Joe Spencer to get the base image for the oneline diagram
    * Typically, we receive a screenshot of the oneline diagram already configured in the RTAC HMI. Then, Joe will create a **\*.svg** file of the oneline and save it in the Dev server.

.. todo:: add Figma steps 

Populate the Oneline Diagram
--------------------------
#. Log in to the Gateway for the Dev server as ``cegadmin``. 
#. Set the default tag provider to the desired site for all projects.
#. Launch the Designer for the Dev server.
#. Select the desired site as the tag provider.
#. Open Perspective and select the view that Joe set up, most likely saved at ``Views/Diagrams/Designer/<Site>1Line``. You should see the **\*.svg** diagram.
#. Copy the appropriate components from ``Perspective/Views/Diagrams/ElectricalNew`` and paste to the oneline diagram. This will typically include breakers, (un)telemetered switches, and capacitor banks.
#. Update parameters for all oneline components to point to the correct tags and display the correct labels.
#. For breakers, update the following parameters:

    +---------------+-----------------------------------+-----------------------------------+
    | Parameter     | Typical Tag Path                  | Function                          |
    +===============+===================================+===================================+
    | tagPath       | Substation/<device>_closed        | Indicate if the breaker is closed |
    +---------------+-----------------------------------+-----------------------------------+
    | tagPathClose  | Substation/Close_breaker_<device> | Close the breaker                 |
    +---------------+-----------------------------------+-----------------------------------+
    | tagPathClosed | Substation/<device>_closed        | Indicate if the breaker is closed |
    +---------------+-----------------------------------+-----------------------------------+
    | tagPathOpen   | Substation/<device>_open          | Indicate if the breaker is open   |
    +---------------+-----------------------------------+-----------------------------------+
    | tagPathTrip   | Substation/Trip_breaker_<device>  | Trip (open) the breaker           |
    +---------------+-----------------------------------+-----------------------------------+

#. Verify that the ``BreakerOperableVertical`` and ``BreakerOperableHorizontal`` will pass parameters along as expected. Logically follow the commands and parameters that will be passed from the click action all the way to the RTAC.
#. Create memory tags for all untelemetered switches. These tags need an initial state set by the operator. Reference Hornshadow for an example.
#. Update the ``tagPath`` parameter for the switches in the oneline.

Deploy the Oneline Diagram
--------------------------
When everything is working as intended (except breaker actions that shouldn't be tested without approval), we can deploy the oneline to the site.

#. Have the Dev Designer open with the completed oneline view.
#. Open the Designer for the production site.
#. Copy the oneline view/page into the prod site Designer.
#. Refresh the MultiXRef cache.
#. Verify everything is working on the site HMI.

Testing & Spot Checks
---------------------
Before formal breaker testing, it is possible to test breaker operation without sending any commands to the breakers.

#. Communicate with the site team to have someone put the breakers in "local" mode. They will not accept remote commands to trip or close.
#. Communicate with someone with substation RTAC access. This might be our own engineer or a third-party. Verify all breaker tags are referencing the correct points.
#. Coordinate with the site team and RTAC engineer to issue trip/close commands. The RTAC engineer must confirm that the signals were received at the correct time and in the correct format for each breaker.
#. If any commands are not received, investigate the oneline configuration.

Untelemetered switches should also be tested to ensure they can be marked open or closed. This does not require any other people involved, except for leaving them in the correct state.

How it Works
============
Each object that we just created on the oneline is essentially an embedded view (e.g. BreakerOperableVertical1) pulling from a generic view (e.g. BreakerOperableVertical) stored in the ``ElectricalNew`` folder. Actions and events must be configured on the generic views.

Displaying equipment status
---------------------------
* Since the objects in the oneline are linked to tags that indicate equipment status, we can change their appearance accordingly.
.. todo:: Fill this in

Sending trip/close commands
---------------------------
* Breaker views in ``ElectricalNew`` have an **onClick** action configured in the root page. This is how we bring up the trip/close pop-up window at ``ElectricalNew/BreakerControl``.
* The *BreakerControl* window has a *FlexContainer* with *Trip* and *Close* button components. Each button has a script action that calls ``control.doWriteDnp3Bo()`` to communicate with the breaker. This function works with the new DNP3 driver (not the legacy driver).
* We use the **oper.LatchOff** command to trip the breaker by sending at value of ``4`` to a tag like *Trip_breaker_52F2*. We use the **oper.LatchOn** command to close the breaker by sending a value of ``3`` to a tag like *Close_breaker_52F2*. **oper.Pulse** commands may also be used at some sites by sending a value of ``2``.
* The legacy driver uses ``control.doWriteValueToPath()`` to write a ``1`` for **oper.LatchOn** and ``0`` **for oper.LatchOff** to a tag like *52F1/Control/CommandBreakerClose*. We also use this for CapBank control via the PPC.
* This can be seen in the deprecated version at *Lib/CEGassetCards/Substation/BreakerControl*