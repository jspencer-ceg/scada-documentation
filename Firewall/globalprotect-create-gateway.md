##############################
Create a GlobalProtect gateway
##############################

Create a gateway for each ISP connection.

Step 1. Add address objects.
============================

#. Go to :menuselection:`Objects --> Addresses`.
#. :guilabel:`Add` the following address objects:

   * Entire Plant: Enter the subnet address that encompasses the entire site.
   * GlobalProtect ISP1 Clients: Use 10.251.251.0/24
   * GlobalProtect ISP2 Clients: Use 10.252.252.0/24

Step 2. Add a gateway.
======================

#. Navigate to :menuselection:`Network --> GlobalProtect --> Gateways`.
#. Select :guilabel:`Add`.
#. Give the gateway a :guilabel:`Name`:

      :samp:`{ISP} Gateway`

   Replace: :samp:`{ISP}` with :samp:`ISP1` if this is for the primary ISP, and :samp:`ISP2` if this is for the secondary ISP.

#. Select the :guilabel:`Interface` corresponding to the ISP connection.

#. Leave :guilabel:`IP Address Type` set to :guilabel:`IPv4 Only`.

#. Leave :guilabel:`IPv4 Address` blank.

Step 3. Configure authentication settings.
==========================================

#. Navigate to the :guilabel:`Authentication` tab.

#. Select the :guilabel:`SSL/TLS Service Profile` that you created for
   GlobalProtect.

#. :guilabel:`Add` a :guilabel:`Client Authentication` configuration with the
   following settings:

   a. Set a :guilabel:`Name`:

         :samp:`Client Auth`

   b.  Set the :guilabel:`Authentication Profile` to the name of the profile you
       created earlier.

   c. Select :guilabel:`OK` to save the configuration.

Step 4. Enable tunneling and then configure the tunnel parameters.
==================================================================

#. In the GlobalProtect Gateway Configuration dialog, navigate to :menuselection:`Agent --> Tunnel Settings`.

#. Enable :guilabel:`Tunnel Mode` to enable split tunneling.

#. Select the :guilabel:`Tunnel Interface` you defined that corresponds to this
   gateway's ISP.

#. Leave :guilabel:`Enable IPSec` selected and leave :guilabel:`GlobalProtect
   IPSec Crypto` set to ``default``.

Step 5. Configure client settings.
==================================

#. In the GlobalProtect Gateway Configuration dialog, navigate to :menuselection:`Agent --> Client Settings`.

#. :guilabel:`Add` a client settings configuration.

#. Select :guilabel:`Config Selection Criteria` and set a :guilabel:`Name`:

      :samp:`Client Settings`

#. Go to :guilabel:`Authentication Override` and for the
   :guilabel:`Certificate to Encrype/Decrypt Cookie`, select the GlobalProtect
   certificate you created.

Step 6. Configure an IP pool.
=============================

#. Go to :guilabel:`IP Pools` and select :guilabel:`Add` from the
   :guilabel:`IP Pool` list.

#. Add address objects to Enter an IP range for the IP pool:

   *  For the first ISP connection, use :samp:`GlobalProtect ISP1 Clients`.
   *  For the second ISP connection, use :samp:`GlobalProtect ISP2 Clients`.
   *  For additional ISPs, create address objects similar to the first two and increment the second and third octets by one.

Step 7. Configure split tunnel settings.
========================================

#. Select :guilabel:`Split Tunnel` and :guilabel:`Add` an entry to the :guilabel:`Include` list.

#. Select the :samp:`Entire Plant` address object.

#. Select :guilabel:`OK` to save the settings in the Configs dialog.

Step 8. Set a timeout period.
=============================

#. In the GlobalProtect Gateway Configuration dialog, select :menuselection:`Agent --> Connection Settings`.

#. Set the :guilabel:`Login Lifetime` to :guilabel:`Days` and ``1``.

#. Select :guilabel:`OK` to save the settings in the GlobalProtect Gateway
   Configuration dialog.
