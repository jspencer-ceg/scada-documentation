#############################
Generate a server certificate
#############################

Once you have generated a root certificate, you can create server certificates to authenticate the user interface and the GlobalProtect portal. You first create the certificate and then use the root certificate to sign it.

Create two certificates: One for GlobalProtect and one for the management interface. If the firewalls are in an HA pair, you will need to create a management certificate on each firewall because the management certificates do not get synchronized between the two firewalls. GlobalProtect certificates are synchronized. Follow the steps below for each certificate.

Step 1.
=======

Select :menuselection:`Device --> Certificate Management --> Certificates --> Device Certificates`.

Step 2.
=======

Select :guilabel:`Generate`.

Step 3.
=======

Select :guilabel:`Local` as the :guilabel:`Certificate Type`.

Step 4.
=======

Enter a :guilabel:`Certificate Name`:

* For a GlobalProtect certificate: :samp:`{PROJECT_NAME} GlobalProtect`
* For a management certificate: :samp:`{PROJECT_NAME} {DEVICE_NUM} Management`

Replace:

* :samp:`{PROJECT_NAME}` with the name of the project in Title Case.
* :samp:`{DEVICE_NUM}` with the device number of the firewall if the firewall is in an HA pair. If the firewall is not in an HA pair, the device number can be omitted.

Step 5.
=======

In the :guilabel:`Common Name` field, enter the same name as the :guilabel:`Certificate Name`.

Step 6.
=======

In the :guilabel:`Signed By` field, select the root CA certificate that will issue (sign) the certificate. This would be the one that you just created.

Step 7.
=======

Leave :guilabel:`Block Private Key Export` and :guilabel:`Certificate Authority` unselected.

Step 8.
=======

Leave :guilabel:`OCSP Responder` blank.

Step 9.
=======

Select the following :guilabel:`Cryptographic Settings`:

    :Algorithm: ``RSA``
    :Number of Bits: ``4096``
    :Digest: ``sha256``
    :Expiration (days): ``730`` (two years, which is a `Mac requirement <https://support.apple.com/en-us/103769>`_ to be under 825 days).

Step 10.
========

Click :guilabel:`Add` to select the following :guilabel:`Certificate Attributes`:

Country = "C" from "Subject" field
   ``US``
State = "ST" from "Subject" field
   Enter the full name of the state in Title Case.
Locality = "L" from "Subject" field
   Enter the full name of the nearest city in Title Case.
Organization = "O" from "Subject" field
   Enter the name of the project's owner.
IP = "IP Address" from Subject Alternative Name (SAN) field
   Create one of these entries for each IP address that will be used to access either a GlobalProtect portal or a management interface:

   * For a GlobalProtect certificate, create an entry for each public IP address.
   * For a Management certificate, create an entry for each public IP address and for the management interface IP address of the firewall you are working on. In an HA pair, each firewall will have its own certificate and will have its own management IP address, but the public IP addresses will be the same for both.

Step 11.
========

Select :guilabel:`Generate`. A modal will tell you that the certificate and key pair was successfully generated. Select :guilabel:`OK` and then select :guilabel:`Commit`.
