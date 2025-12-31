#############################
Create a GlobalProtect portal
#############################

Create a portal for each ISP connection.

Step 1. Add a portal.
=====================

#. Navigate to :menuselection:`Network --> GlobalProtect --> Portals`.
#. Select :guilabel:`Add`.
#. Give the portal a :guilabel:`Name`:

      :samp:`{ISP} Portal`

   Replace :samp:`{ISP}` with :samp:`ISP1` if this is for the primary ISP, and :samp:`ISP2` if this is for the secondary ISP.

Step 2. Specify network settings to enable the GlobalProtect app to communicate with the portal.
================================================================================================

#. Select the :guilabel:`Interface` corresponding to the ISP connection.

#. Leave :guilabel:`IP Address Type` set to :guilabel:`IPv4 Only`.

#. Leave :guilabel:`IPv4 Address` blank.

.. figure:: img/portal/general.png

   Completed :guilabel:`General` tab of a GlobalProtect portal.

Step 3. Specify how the portal authenticates users.
===================================================

#. In the GlobalProtect Portal Configuration dialog, navigate to :menuselection:`Authentication`.

#. Select the :guilabel:`SSL/TLS Service Profile` that you created for
   GlobalProtect.

   .. figure:: img/portal/auth.png

#. :guilabel:`Add` a :guilabel:`Client Authentication` configuration with the
   following settings:

   a. Set a :guilabel:`Name`:

         :samp:`Client Auth`

   #. Set the :guilabel:`Authentication Profile` to the name of the profile you
      created earlier.

      .. figure:: img/portal/client-auth-config.png

         Completed Client Authentication dialog.

   #. Select :guilabel:`OK` to save the configuration.

.. figure:: img/portal/auth-with-config.png

   Completed :guilabel:`Authentication` tab of a GlobalProtect portal.

Step 4. Configure how the GlobalProtect app verifies the identity of the portal and gateways.
=============================================================================================

#. In the GlobalProtect Portal Configuration dialog, navigate to :menuselection:`Agent`.

#. In the :guilabel:`Trusted Root CA` field, :guilabel:`Add` and select the
   root CA certificate that was used to issue the GlobalProtect server
   certificate.

   .. figure:: img/portal/agent.png

      Agent tab set up with a trusted root certificate.

#. :guilabel:`Add` an :guilabel:`Agent` configuration with the following
   settings:

   a. On the :guilabel:`Authentication` tab, set a :guilabel:`Name`:

         :samp:`Agent`

   #. In the :guilabel:`Authentication Override` section, select the following:

      *  :guilabel:`Generate cookie for authentication override`
      *  :guilabel:`Accept cookie for authentication override`

      For :guilabel:`Certificate to Encrypt/Decrypt Cookie`, select the GlobalProtect certificate you created.

      .. figure:: img/portal/agent-config-auth.png


   #. Navigate to the :guilabel:`External` tab.

   #. :guilabel:`Add` an
      :guilabel:`External Gateway`. Set a :guilabel:`Name` for the connection that will display in the GlobalProtect client:

         :samp:`{PROJECT_NAME} {ISP} Gateway`

      Replace 

      * :samp:`{PROJECT_NAME}` with the name of the project in Title Case.
      * :samp:`{ISP}` with :samp:`ISP1` if this is for the primary ISP, and :samp:`ISP2` if this is for the secondary ISP.

   #. If the external address is in the form of an FQDN, select :guilabel:`FQDN` and enter the address in the :guilabel:`Address` field.

   #. If the external address is in the form of an IP address, select :guilabel:`IP` and enter the IP address in either the :guilabel:`IPv4` or :guilabel:`IPv6` field. For our work, this will usually be an :guilabel:`IPv4` address.

   #. :guilabel:`Add` a :guilabel:`Source Region` each for :guilabel:`US
      (United States)` and :guilabel:`CA (Canada)`. Set the priority for each
      region to :guilabel:`Highest`.

      .. figure:: img/portal/external-gateway.png
         :scale: 50

   #. Select :guilabel:`OK` to save the external gateway.

   #. Navigate to the :guilabel:`App` tab. In the :guilabel:`App Configurations` section, set :guilabel:`Connect Method` to :guilabel:`Pre-logon then On-demand`.
      
      .. figure:: img/portal/agent-config-app.png


   #. Navigate to the :guilabel:`HIP Data Collection` tab. Clear :guilabel:`Collect HIP Data`.

      .. figure:: img/portal/agent-config-hip.png

   #. Select :guilabel:`OK` to save the agent configuation.

#. Select :guilabel:`OK` to save the portal configuration.
