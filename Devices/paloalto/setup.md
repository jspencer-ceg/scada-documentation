****************************************
Palo Alto PA-440 Commissioning Procedure
****************************************

.. note:: Leave all settings at their defaults, except as specified in this guide.

Integrate the Firewall into Your Management Network
===================================================

Perform Initial Configuration
-----------------------------

By default, the PA-Series firewall has an IP address of 192.168.1.1 and a username/password of admin/admin. For security reasons, you must change these settings before continuing with other firewall configuration tasks. You must perform these initial configuration tasks either from the MGT interface, even if you do not plan to use this interface for your firewall management, or using a direct serial connection to the console port on the firewall.

Step 1: Install your firewall and connect power to it.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. tip:: If your firewall model has dual power supplies, connect the second power supply for redundancy. Refer to the hardware reference guide for your model for details.

Step 2: Gather the required information from SCADA design documents.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* IP address for the MGT port
* Netmask
* Default gateway
* DNS server address

Step 3: Connect your computer to the firewall and log in.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can connect to the firewall either with a serial connection or with an Ethernet connection. The serial method is preferred as the initial method to connect to the firewall because it is more straightforward and you can see status messages from the firewall as it boots. With either method, you will need to know that the default username is ``admin`` and the default password is ``admin``.

Serial Connection
"""""""""""""""""

#. Connect a serial cable from your computer to the Console port. You may use an RJ45-to-DE-9 cable connected to a serial-to-USB cable like an SEL C662 cable, or an RJ45-to-USB cable that has a serial adapter built in.
#. Use Windows Device Manager to determine the COM port number of your serial adapter.
#. Open up terminal emulation software such as PuTTY or SEL AcSELerator QuickSet. Open a connection to the COM port you found in the previous step using the following settings:

   * Baud rate: 9600
   * Start bits: 8
   * Parity: N
   * Stop bits: 1

#. If the firewall was recently turned on or rebooted, you will see boot-up messages streaming down your serial console window. Wait a few minuts for the boot-up sequence to complete. When the firewall is ready, the prompt changes to the name of the firewall, for example, ``PA-220 login``.
#. Log in with the default username and password.

Ethernet Connection
"""""""""""""""""""

#. Connect an RJ-45 Ethernet cable from your computer to the MGT port on the firewall. 
#. On your computer, set the Ethernet adapter you are using for this connection to 192.168.1.10/24 with no default gateway.
#. Open an SSH client such as PuTTY and open an SSH session to the firewall with the following parameters:

    :IP address: ``192.168.1.1``
    :Username: ``admin``
    :Password: ``admin``

   .. note:: You may see a warning such as the one below::

         @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
         @    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
         @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
         IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
         Someone could be eavesdropping on you right now (man-in-the-middle attack)!
         It is also possible that a host key has just been changed.
         The fingerprint for the RSA key sent by the remote host is
         SHA256:oqXULF2uaXr4lKGklA3bzsT4KhpctqleVxq0kBlrmUU.
         Please contact your system administrator.
         Add correct host key in /Users/ntmoe/.ssh/known_hosts to get rid of this message.
         Offending RSA key in /Users/ntmoe/.ssh/known_hosts:282
         Host key for 192.168.1.1 has changed and you have requested strict checking.
         Host key verification failed.

      If so, you may safely delete the offending RSA key in your ``known_hosts`` file.

      You may also see a warning like this::

         The authenticity of host '192.168.1.1 (192.168.1.1)' can't be established.
         RSA key fingerprint is SHA256:oqXULF2uaXr4lKGklA3bzsT4KhpctqleVxq0kBlrmUU.
         This key is not known by any other names
         Are you sure you want to continue connecting (yes/no/[fingerprint])?

      This is expected for the first time connecting to a particular remote SSH host. Since you are directly plugged into the firewall, you may safely type ``yes`` and then ``<Enter>`` to continue connecting.

#. From a browser, go to ``https://192.168.1.1``.


Step 4: Set a new password for the admin account.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. note:: Starting with PAN-OS 9.0.4, the predefined, default administrator password (admin/admin) must be changed on the first login on a device. The new password must be a
   minimum of eight characters and include a minimum of one lowercase and one uppercase character, as well as one number or special character.
   
   Be sure to use the best practices for password strength to ensure a strict password and review the password complexity settings.


The firewall will force you to change the password. It will be wiped out in a later step, but use a standard password to help you remember the password in case something goes wrong.

The standard password is in this format::

   <Proj>PA440!

where ``<Proj>`` is a four-letter prefix representing the project. Only the first letter of this prefix is capitalized; the following letters are lowercase. Oftentimes the prefix is the same as the project prefix used on the drawing set numbering system, but please consult with Nick before chosing the prefix.

Step 5: Disable ZTP and switch to standard mode.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

After you change the password, you will see the following in the terminal:

.. code-block:: text

   Number of failed attempts since last successful login: 0


   ==========================================================================

   Zero Touch Provisioning (ZTP) of the firewall is in progress. ZTP requires Panorama and pre-registration with the Customer Support Portal and ZTP Service to provision the firewall. To disable ZTP and switch to standard mode, please use the command below. This will restart the firewall in standard mode, and allow regular configuration of the firewall.

   Operational command to disable ZTP and switch to standard mode:
           > set system ztp disable
   Warning: This will cause a system reboot.

   ==========================================================================


   Warning: Your device is still configured with the default admin account credentials. Please change your password prior to deployment.
   admin@PA-440>

Type the following::

   admin@PA-440> set system ztp disable

This prompt will appear::

   Executing this command will disable Zero Touch Provisioning (ZTP), and remove all logs and configuration. The system will restart in standard mode for regular configuration of the firewall. Are you sure you want to continue?  (y or n)

Type ``y`` to continue. The firewall will reboot::

   Broadcast message from root (console) (Thu Dec  5 10:47:40 2024):

   The system is going down for reboot NOW!

The firewall will reboot. Wait for the firewall to boot up again. If you are connected with a serial cable, you will see the login prompt, ``PA-440 login:``, when the device has rebooted. If you are connected through the MGT port, you can ping 192.168.1.1 until you get responses again.

..
  , and then you can try to SSH again. The host key will change again so you may have to clear out the offending key.

Step 6: Log into the firewall using a web browser.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Set up your computer to connect to the MGT port with an Ethernet cable. If you haven't done so already, set the Ethernet adapter you are using for this connection to ``192.168.1.10/24`` with no default gateway.
#. Open a browser and enter ``https://192.168.1.1`` in the address bar. A certificate warning will appear, which you can safely disregard.
#. Log in with the default username of ``admin`` and password of ``admin``. They were reset after disabling ZTP mode.
#. You will see a **Password Change Required** screen. Enter the old password of ``admin`` and enter the new standard password according to the method in Step 5. Select **Change Password**.
#. Log in using the new password.
#. You will be greeted by a welcome modal. Select the **Do not show again** checkbox and select **Close**.
#. Next, you will see a **Telemetry Data Collection** modal. Select **OK**.


Step 7: Set up accounts for SCADA team members.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You will create an account for each member of the CEG SCADA team. The username is the same as each member's email username:

+---------------------+----------------+
| Employee Name       | Username       |
+=====================+================+
| Anton Silburn       | ``asilburn``   |
+---------------------+----------------+
| Celeste Osterheld   | ``costerheld`` |
+---------------------+----------------+
| Dave Ayers          | ``dayers``     |
+---------------------+----------------+
| Devin Slack         | ``dslack``     |
+---------------------+----------------+
| Elizabeth Leeser    | ``eleeser``    |
+---------------------+----------------+
| Junior Metayer      | ``jmetayer``   |
+---------------------+----------------+
| Josh Walker         | ``jwalker``    |
+---------------------+----------------+
| Matt Steele         | ``msteele``    |
+---------------------+----------------+
| Nick Moe            | ``ntmoe``      |
+---------------------+----------------+
| Sandeep Thadiparthy | ``sandeep``    |
+---------------------+----------------+
| Taylor Meador       | ``tmeador``    |
+---------------------+----------------+



#. Select **Device** > **Administrators**.
#. For each user:

   a. Select **Add**.
   b. Configure as follows:

      :Name: Enter the username as listed in the table above.
      :Password: Enter the standard password, as described above.
      :Confirm Password: Re-enter the password.
      :Administrator Type: Select **Dynamic** and select **Superuser** from the drop-down menu.

   c. Select **OK**.

Step 8: Configure the MGT interface.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Select **Device** > **Setup** > **Interfaces** and edit the **Management** interface. Use information from the IP address schedule or the logical network diagram [#agree]_ to fill in the following:

   :IP Type: Select **Static**.
   :IP Address: Management IP address for the firewall. This is typically ``192.168.x.3`` for the primary firewall and ``192.168.x.4`` for the secondary firewall, where *x* is the third octet of the Management LAN.
   :Netmask: Enter the mask for the Management network. It is typically ``255.255.255.240``.
   :Default Gateway: Set to the IP address of the Management network interface, typically ``192.168.x.1``.
   :Speed: Select **auto-negotiate**.

#. For **Administrative Management Services**, ensure that **HTTPS** and **SSH** are both checked.

   .. tip:: Make sure **Telnet** and **HTTP** are not selected because these services use plaintext and are not as secure as the other services and could compromise administrator credentials.

#. For **Network Services**, ensure that **Ping** is checked.

#. Select **OK**.

.. image:: bp-management-interface-settings.png

.. [#agree] These two documents should agree with each other. If they don't, work to resolve the differences.

Step 9: Configure DNS and date and time (NTP) settings.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. note:: You must manually configure at least one DNS server on the firewall or it will not be able to resolve hostnames; it will not use DNS server settings from another source, such as an ISP.

#. Select **Device** > **Setup** > **Services** and edit the Services section.
#. On the **Services** tab, for **DNS Settings**, enter the **Primary DNS Server** address and **Secondary DNS Server** address:

   :Primary DNS Server: 8.8.8.8
   :Secondary DNS Server: 8.8.4.4

   .. image:: setup-services-services.png

#. On the **NTP** tab, enter the IP address of the primary NTP server as the **Primary NTP Server**. This will usually be the IP address of the SEL-2488 satellite clock.
#. Enter a **Secondary NTP Server** address. This will usually be the IP address of the substation RTAC if this is a CEG substation; otherwise, it will be the IP address of the first PPC RTAC.
#. Select **OK**.

Step 10: Configure general firewall settings as needed.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Select **Device** > **Setup** > **Management** and edit the General Settings:
#. Select :menuselection:`Start --> Programs`

   :Hostname: :samp:`{PROJ}-{DEVICE}` where :samp:`{PROJ}` is the project code and :samp:`{DEVICE}` is the device name of the firewall. Example: ``BELK4-16ERFC-1A``
   :Login Banner: This system is for the use of authorized users only. Individuals using this system without authority, or in excess of their authority, are subject to having all their activities on this system monitored and recorded by system personnel. Anyone using this system expressly consents to such monitoring and is advised that if such monitoring reveals possible evidence of criminal activity, system personnel may provide the evidence of such monitoring to law enforcement officials.
   :Time Zone: Select the correct time zone for the project.

#. Enter the :guilabel:`Latitude` and :guilabel:`Longitude` **Latitude** and **Longitude** in decimal degree form to enable accurate placement of the firewall on the world map. You can use an online service, like Google Maps, to determine coordinates for the firewall.
#. Select **OK**.

Step 11: Commit your changes.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. note:: When the configuration changes are saved, you will lose connectivity to the web interface because the IP address has changed.

Select **Commit** at the top right of the web interface. The firewall can take up to 90 seconds to save your changes.

Because you have changed the management IP address, the progress bar will seem to stop at 98% and you will lose your connection to the firewall. This is expected.

Step 12: Connect the firewall to your network.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Disconnect the firewall from your computer.
#. Connect the MGT port to a switch port on the Management network using an Ethernet cable. Make sure that the switch port you cable the firewall to is configured for auto-negotiation.
#. Plug your computer's Ethernet adapter into a switch port that is also on the Management VLAN and set the adapter's IP address to an address on the Management network.

.. attention:: If this is the primary firewall, continue to the next section. If this is the backup firewall, skip to step TBD in section TBD.

Step TBD: Open an SSH management session to the firewall.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Using a terminal emulation software, such as PuTTY, launch an SSH session to the firewall using the new IP address you assigned to it.

Step TBD: Verify network access to external services required for firewall management, such as the Palo Alto Networks Update Server.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Verify that you have connectivity and then proceed to Register the Firewall and Activate Subscription Licenses.

#. Use update server connectivity test to verify network connectivity to the Palo Alto Networks Update server as shown in the following example:

   #. Select **Device** > **Troubleshooting**, and select **Update Server Connectivity** from the Select Test drop-down.
   #. **Execute** the update server connectivity test.

#. Use the following CLI command to retrieve information on the support entitlement for the firewall from the Palo Alto Networks update server:

   .. code-block:: console

      request support check

   If you have connectivity, the update server will respond with the support status for your firewall. If your firewall is not yet registered, the update server returns the following message:

   .. code-block:: text

      Contact Us 

      https://www.paloaltonetworks.com/company/contact-us.html 

      Support Home 

      https://www.paloaltonetworks.com/support/tabs/overview.html 

      Device not found on this update server 

Segment Your Network Using Interfaces and Zones
===============================================

Traffic must pass through the firewall in order for the firewall to manage and control it. Physically, traffic enters and exits the firewall through *interfaces*. The firewall determines how to act on a packet based on whether the packet matches a *Security policy rule*. At the most basic level, each Security policy rule must identify where the traffic came from and where it is going. On a Palo Alto Networks next-generation firewall, Security policy rules are applied between zones. A *zone* is a grouping of interfaces (physical or virtual) that represents a segment of your network that is connected to, and controlled by, the firewall. Because traffic can only flow between zones if there is a Security policy rule to allow it, this is your first line of defense. The more granular the zones you create, the greater control you have over access to sensitive applications and data and the more protection you have against malware moving laterally throughout your network. For example, you might want to segment access to the database servers that store your customer data into a zone called Customer Data. You can then define security policies that only permit certain users or groups of users to access the Customer Data zone, thereby preventing unauthorized internal or external access to the data stored in that segment.

Network Segmentation for a Reduced Attack Surface
-------------------------------------------------

The following diagram shows a very basic example of Network Segmentation Using Zones. The more granular you make your zones (and the corresponding security policy rules that allows traffic between zones), the more you reduce the attack surface on your network. This is because traffic can flow freely within a zone (intra-zone traffic), but traffic cannot flow between zones (inter-zone traffic) until you define a Security policy rule that allows it. Additionally, an interface cannot process traffic until you have assigned it to a zone. Therefore, by segmenting your network into granular zones you have more control over access to sensitive applications or data and you can prevent malicious traffic from establishing a communication channel within your network, thereby reducing the likelihood of a successful attack on your network.

.. image:: zone-interface-mapping.png

Configure Interfaces and Zones
------------------------------

After you identify how you want to segment your network and the zones you will need to create to achieve the segmentation (as well as the interfaces to map to each zone), you can begin configuring the interfaces and zones on the firewall. Configure interfaces on the firewall the to support the topology of each part of the network you are connecting to. The following workflow shows how to configure Layer 3 interfaces and assign them to zones. For details on integrating the firewall using a different type of interface deployments (for example as virtual wire interfaces or as Layer 2 interfaces), see the PAN-OS Networking Adminstrator’s Guide.

Step 1: Log into the web interface.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Using a secure connection (https) from your web browser, log in using the new IP address and password you assigned during initial configuration (https://<IP address>). You will see a certificate warning; that is okay. Continue to the web page.

Step 2: Delete the default virtual wire interface.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The firewall comes preconfigured with a default virtual wire interface between ports Ethernet 1/1 and Ethernet 1/2 (and a corresponding default security policy and zones). You must manually delete the configuration to prevent it from interfering with other interface settings you define.

You must delete the configuration in the following order:

#. To delete the default security policy, select **Policies** > **Security**, select the ``rule1`` rule, and select **Delete**. The only rules left should be ``intrazone-default`` and ``interzone-default``.
#. To delete the default trust and untrust zones, select **Network** > **Zones**, select each zone and select **Delete**.
#. To delete the default virtual wire, select **Network** > **Virtual Wires**, select the virtual wire and select **Delete**.
#. To delete the interface configurations, select **Network** > **Interfaces** and then select each interface (ethernet1/1 and ethernet1/2) and select **Delete**.
#. **Commit** the changes.

Step 3: Create security zones.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Consult the logical network diagram. You will create zones that correspond to the subnets directly connected to the firewall. The name of each zone will be that of the corresponding subnet, in `Headline Case <https://titlecaseconverter.com/>`_ according to *The Chicago Manual of Style*. The exception is that the subnet(s) connected to the Internet will be in the Internet zone. Examples:

- Internet
- Management
- Engineering
- Protection
- Transformer
- Field Management

For each zone:

#. Select **Network** > **Zones** and select **Add**. Enter the **Name** of the zone. In the **Type** drop-down, select **Layer3**.
#. Select **OK**.

Step 4: Create management profiles.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An Interface Management profile protects the firewall from unauthorized access by defining the protocols, services, and IP addresses that a firewall interface permits for management traffic. For example, you might want to prevent users from accessing the firewall web interface over the ethernet1/1 interface but allow that interface to receive SNMP queries from your network monitoring system. In this case, you would enable SNMP and disable HTTP/HTTPS in an Interface Management profile and assign the profile to ethernet1/1.

You can assign an Interface Management profile to Layer 3 Ethernet interfaces (including subinterfaces) and to logical interfaces (aggregate group, VLAN, loopback, and tunnel interfaces). If you do not assign an Interface Management profile to an interface, it denies access for all IP addresses, protocols, and services by default.

.. note:: The management (MGT) interface does not require an Interface Management profile. You restrict protocols, services, and IP addresses for the MGT interface when you perform initial configuration of the firewall. In case the MGT interface goes down, allowing management access over another interface enables you to continue managing the firewall.

.. tip:: When enabling access to a firewall interface using an Interface Management profile, do not enable management access (HTTP, HTTPS, SSH, or Telnet) from the internet or from other untrusted zones inside your enterprise security boundary, and never enable HTTP or Telnet access because those protocols transmit in cleartext. Follow the Best Practices for Securing Administrative Access to ensure that you are properly securing management access to your firewall. 


#. Select **Network** > **Network Profiles** > **Interface Mgmt** and select **Add**.
#. Enter a **Name**: Ping
#. Under **Network Services**, select **Ping**.
#. Select **OK**.
#. Select **Add**.
#. Enter a **Name**: Remote Management
#. For **Administrative Management Services**, select **HTTPS** and **SSH**.
#. For **Network Services**, select **Ping**.
#. Select **Add** to add a permitted IP address. Enter the CEG's public subnet: 209.237.110.201
#. Select **OK**.

Step 5: Rename and add virtual routers.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The project may have either one or two ISPs. Each ISP will have a virtual router named after it. We will rename the default virtual router and name it after the primary ISP. If there is a secondary ISP, we will create a second default router and name it after it.

#. Select **Network** > **Virtual Routers** and then select the **default** link to open the Virtual Router dialog.
#. Select the **Router Settings** tab. Enter:

   :Name: ``VR-<ISP>``, where ``<ISP>`` is the name of the primary ISP in HeadlineCamelCase.

#. Select the **Static Routes** tab and select **Add**. Enter:

   :Name: ``<ISP>``, where ``<ISP>`` is the same name used in the name of the virtual router.
   :Destination: 0.0.0.0/0

#. Select the **IP Address** option in the **Next Hop** drop-down and then enter the IP address for your Internet gateway (for example, 203.0.113.1). If you don't know this address yet (such as when fiber has not been installed), use a fake IP address: 198.51.100.1. The 198.51.100.0/24 network is reserved for documentation purposes and will not lead to anything real. Just don't forget to come back and put in the actual address later!

   .. image:: default-route.png

#. Select **OK** to save the static route.
#. Select **OK**.
#. If there is (or will be) a secondary ISP, select **Add**. Enter a **Name** and **Static Route** for the secondary virtual router in the same fashion as the name of the virtual router for the primary ISP. Select **OK**.

Step 5: Configure the external interfaces (the interfaces that connect to the Internet).
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Single ISP per physical interface
"""""""""""""""""""""""""""""""""

#. Select **Network** > **Interfaces**, select the interface that is connected to the primary ISP, and enter:
   
   :Comment: Give the interface a name in the form ``ISP-<ISP>``, where ``<ISP>`` is the name of the ISP in CapitalCamelCase.
   :Interface Type: Layer3

#. On the **Config** tab, select the **Internet** zone from the **Security Zone** drop-down.
#. In the **Virtual Router** drop-down, select **default**. You will rename this later.
#. To assign an IP address to the interface, select the **IPv4** tab, select **Add** in the IP section, and enter the IP address and network mask to assign to the interface, for example 203.0.113.23/24.

   .. image:: interface-config.png

#. To enable you to ping the interface, select **Advanced** > **Other Info**, expand the **Management Profile** drop-down, and select **Ping**.
#. To save the interface configuration, select **OK**.

Dual ISPs per physical interface
""""""""""""""""""""""""""""""""

#. Select **Network** > **Interfaces** and edit the physical interface that will be used for each ISP's VLANs from the external switch.
#. Set the **Interface Type** to **Layer3**.
#. Select **OK**.
#. For each ISP:

   #. Select the physical interface's row and select **Add Subinterface**.
   #. To the right of the **Interface Name** field, enter the VLAN ID.
   #. Enter the following:

      :Comment: Give the interface a name in the form ``ISP-<ISP>``, where ``<ISP>`` is the name of the ISP in CapitalCamelCase.
      :Tag: Enter the VLAN ID again.
      :Virtual Router: Select the router corresponding to the ISP for this interface.
      :Security Zone: **Internet**
   
   #. Select the **IPv4** tab and select **Add**. Enter the IP address and subnet mask to assign to the interface using CIDR notation, e.g. 203.0.113.23/24.
   #. Select the **Advanced** tab. From the **Management Profile** drop-down, select **Ping**.

Step 6: Configure the interfaces that connects to the substation's internal networks.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Typically, one cable connects each firewall to the switch that contains internal networks. This cable is represented by an *interface*, and each VLAN that is tagged on that cable is represented by a *subinterface*. Only the subinterfaces have IP addresses, zones, and management profiles assigned to them.

Consult the Logical Network Diagram to determine what subinterfaces are needed. Only create interfaces or subinterfaces for networks that are logically directly connected to the firewall.

#. Select **Network** > **Interfaces** > **Ethernet** and select the interface you want to configure. In this example, we are configuring Ethernet1/15 as the internal interface our users connect to.
#. Enter a **Comment** that describes what the interface is connected to, such as "Connected to 16ESM-1 Port 1/7 (primary) or Port 1/8 (secondary)". This tells me that the primary firewall is connected to Port 1/7 and the secondary firewall is plugged into Port 1/8.
#. Select **Layer3** as the **Interface Type**.
#. Select **OK**.

For each internal subnet directly connected to the firewall:

#. Add a subinterface by selecting the interface it belongs to. (Don't select the name of the interface; rather, select somewhere else in the row to select it.) Select **Add Subinterface**.
#. The **Interface Name** defaults to the interface (e.g. ethernet1/2). In the field to the right of the **Interface Name**, enter the VLAN ID.
#. For **Comment**, describe the subinterface in Headline Case, e.g. Engineering.
#. For **Tag**, enter the VLAN ID.
#. On the **Config** tab, select the virtual router. If there is a backup ISP, select the virtual router corresponding to that ISP.
#. Expand the **Security Zone** drop-down and select the zone that corresponds to this subinterface. For example, if this is the Management subinterface, select **Management**.
#. To assign an IP address to the subinterface, select the **IPv4** tab, click **Add** in the IP section, and enter the IP address and network mask to assign to the interface in CIDR notation, for example: 192.168.241.3/24.
#. To enable you to ping the interface, select **Advanced** > **Other Info**, expand the **Management Profile** drop-down, and select **Ping**.
#. To save the subinterface configuration, click **OK**.

Check your work. Review the **Interface**, **Management Profile**, **IP Address**, **Virtual Router**, **Tag**, **Security Zone**, and **Comment** columns to ensure that you got everything correct.

Create Security Policies
========================

Now that you defined some zones and attached them to interfaces, you are ready to begin creating your Security Policy. The firewall will not allow any traffic to flow from one zone to another unless there is a Security policy rule that allows it. When a packet enters a firewall interface, the firewall matches the attributes in the packet against the Security policy rules to determine whether to block or allow the session based on attributes such as the source and destination security zone, the source and destination IP address, the application, user, and the service. The firewall evaluates incoming traffic against the Security policy rulebase from left to right and from top to bottom and then takes the action specified in the first Security rule that matches (for example, whether to allow, deny, or drop the packet). This means that you must order the rules in your Security policy rulebase so that more specific rules are at the top of the rulebase and more general rules are at the bottom to ensure that the firewall is enforcing policy as expected.

Even though a Security policy rule allows a packet, this does not mean that the traffic is free of threats. To enable the firewall to scan the traffic that it allows based on a Security policy rule, you must also attach Security Profiles—including URL Filtering, Antivirus, Anti-Spyware, File Blocking, and WildFire Analysis—to each rule (the profiles you can use depend on which Subscriptions you purchased). When creating your basic Security policy, use the predefined security profiles to ensure that the traffic you allow into your network is being scanned for threats. You can customize these profiles later as needed for your environment.

Use the following workflow set up a very basic Security policy that enables access to the network infrastructure, to data center applications, and to the internet. This enables you to get the firewall up and running so that you can verify that you have successfully configured the firewall. However, this initial policy is not comprehensive enough to protect your network. After you verify that you successfully configured the firewall and integrated it into your network, proceed with creating a Best Practice Internet Gateway Security Policy that safely enables application access while protecting your network from attack.

Refer to the Firewall Rule List for the project for the rules that you will need to create.

#. Select **Policies** > **Security** and click **Add**.
#. In the **General** tab, enter a descriptive **Name** for the rule using Headline Case. Write names in the form *A* to *B* if possible, where *A* is the source and *B* is the destination. Destinations may be devices, zones, or services.
#. In the **Source** tab, set the **Source Zone**.
#. In the **Destination** tab, set the **Destination Zone**.

   .. tip:: As a best practice, use address objects in the **Destination Address** field to enable access to specific servers or groups of servers only, particularly for services such as DNS and SMTP that are commonly exploited. By restricting users to specific destination server addresses, you can prevent data exfiltration and command and control traffic from establishing communication through techniques such as DNS tunneling.

#. In the **Applications** tab, **Add** the applications that correspond to the network services you want to safely enable. For example, you can select **dns**, **ntp**, **ocsp**, **ping**, and **smtp**.
#. In the **Service/URL Category** tab, keep the **Service** set to **application-default** if the services are using their default ports. If the services are using non-default ports, either add the ports or set to **any**.
#. In the **Actions** tab, set the **Action Setting** to **Allow** to allow the traffic, or **Deny** to deny the traffic.
#. Set **Profile Type** to **Profiles** and select the following security profiles to attach to the policy rule:

   - For **Antivirus**, select **default**
     For Vulnerability Protection, select strict
   - For Anti-Spyware, select strict
   - For URL Filtering, select default
   - For File Blocking, select basic file blocking
   - For WildFire Analysis, select default
#. Verify that **Log at Session End** is enabled. Only traffic that matches a Security policy rule will be logged.
#. Click **OK**.

Create IPsec Tunnels
====================

Create an Aggregate Interface
=============================

Procedure
---------

Step 1: Configure the general interface group parameters.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Select **Network** > **Interfaces** > **Ethernet** and **Add Aggregate Group**.
#. In the field adjacent to the read-only **Interface Name**, enter a number to identify the aggregate group. Enter 1 for the first group.
#. Enter a comment to describe the ports on the other side of the link. For example: 16ESM-1 Ports 1/6 and 1/7
#. For the Interface Type, select **Layer 3**.

Step 2: Configure the LACP settings.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Select the **LACP** tab and **Enable LACP**.
#. Set the **Mode** for LACP status queries to **Passive** (the firewall just responds—the default) or **Active** (the firewall queries peer devices). For us, set this to **Passive**.

   .. tip:: As a best practice, set one LACP peer to active and the other to passive. LACP cannot function if both peers are passive. The firewall cannot detect the mode of its peer device.

#. Set the **Transmission Rate** for LACP query and response exchanges to **Slow** (every 30 seconds—the default) or **Fast** (every second). Base your selection on how much LACP processing your network supports and how quickly LACP peers must detect and resolve interface failures. CEG: Select **Fast**.
#. Select **Fast Failover** if you want to enable failover to a standby interface in less than one second. By default, the option is disabled and the firewall uses the IEEE 802.1ax standard for failover processing, which takes at least three seconds. CEG: Check this box.

   .. tip:: As a best practice, use **Fast Failover** in deployments where you might lose critical data during the standard failover interval.

#. Enter the **Maximum Interfaces** (number of interfaces) that are active (1 to 8) in the aggregate group. If the number of interfaces you assign to the group exceeds the **Max Ports**, the remaining interfaces will be in standby mode. The firewall uses the **LACP Port Priority** of each interface you assign (Step 3) to determine which interfaces are initially active and to determine the order in which standby interfaces become active upon failover. If the LACP peers have non-matching port priority values, the values of the peer with the lower **System Priority** number (default is 32,768; range is 1 to 65,535) will override the other peer. CEG: Leave this at the default of 8.
#. (Optional) For active/passive firewalls only, select **Enable in HA Passive State** if you want to enable LACP pre-negotiation for the passive firewall. LACP pre-negotiation enables quicker failover to the passive firewall (for details, see LACP and LLDP Pre-Negotiation for Active/Passive HA).

   .. note:: If you select this option, you cannot select **Same System MAC Address for Active-Passive HA**; pre-negotiation requires unique interface MAC addresses on each HA firewall.

#. (Optional; not applicable to CEG) For active/passive firewalls only, select **Same System MAC Address for Active-Passive HA** and specify a single **MAC Address** for both HA firewalls. This option minimizes failover latency if the LACP peers are virtualized (appearing to the network as a single device). By default, the option is disabled: each firewall in an HA pair has a unique MAC address.

   .. tip:: If the LACP peers are not virtualized, use unique MAC addresses to minimize failover latency.

Step 3: Click **OK**.
^^^^^^^^^^^^^^^^^^^^^

Step 4: Assign interfaces to the aggregate group.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Assign interfaces to the aggregate group.
Perform the following steps for each interface (1–8) that will be a member of the aggregate group.

#. Select **Network** > **Interfaces** > **Ethernet** and click the interface name to edit it.
#. Enter a **Comment** describing what the port connects to. For example: 16ESM-1 Port 1/6 or 16ESM-2 Port 1/6
#. Set the **Interface Type** to **Aggregate Ethernet**.
#. Select the **Aggregate Group** you just defined.
#. Select the **Link Speed**, **Link Duplex**, and **Link State**.

   .. tip:: As a best practice, set the same link speed and duplex values for every interface in the group. For non-matching values, the firewall defaults to the higher speed and full duplex.

#. (Optional) Enter an **LACP Port Priority** (default is 32,768; range is 1 to 65,535) if you enabled LACP for the aggregate group. If the number of interfaces you assign exceeds the **Max Ports** value of the group, the port priorities determine which interfaces are active or standby. The interfaces with the lower numeric values (higher priorities) will be active.
#. Click **OK**.
#. Add subinterfaces for each subnet to be reached with the aggregate group.

Step 5
^^^^^^

(Not applicable to CEG installations)
If the firewalls have an active/active configuration and you are aggregating HA3 interfaces, enable packet forwarding for the aggregate group.

#. Select **Device** > **High Availability** > **Active/Active Config** and edit the Packet Forwarding section.
#. Select the aggregate group you configured for the **HA3 Interface** and click **OK**.

Step 6: Commit your changes.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Step 7: Verify the aggregate group status.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Select **Network** > **Interfaces** > **Ethernet**.
#. Verify that the Link State column displays a green icon for the aggregate group, indicating that all member interfaces are up. If the icon is grey, at least one member is down but not all. If the icon is red, all members are down.
#. If you configured LACP, verify that the Features column displays the LACP enabled icon for the aggregate group.

Step 8: Set up subinterfaces for the aggregate group.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Select the aggregate group and add subinterfaces to it for each subnet that connects to the aggregate group.
