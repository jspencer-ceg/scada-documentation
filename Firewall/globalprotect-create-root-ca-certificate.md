########################################
Create a self-signed root CA certificate
########################################

A self-signed root certificate authority (CA) certificate is the top-most certificate in a certificate chain. A firewall can use this certificate to automatically issue certificates for other uses. For example, the firewall issues certificates for SSL/TLS decryption and for satellites in a GlobalProtect large-scale VPN.

When establishing a secure connection with the firewall, the remote client must trust the root CA that issued the certificate. Otherwise, the client browser will display a warning that the certificate is invalid and might (depending on security settings) block the connection. To prevent this, after generating the self-signed root CA certificate, import it into the client systems.

Step 1.
=======

Navigate to :menuselection:`Device --> Certificate Management --> Certificates --> Device Certificates`.

Step 2.
=======

Select :guilabel:`Generate`.

Step 3.
=======

Select :guilabel:`Local` (default) as the :guilabel:`Certificate Type`.

Step 4.
=======

Enter a :guilabel:`Certificate Name`:

   :samp:`{PROJECT_NAME} Root CA`

Replace :samp:`{PROJECT_NAME}` with the name of the project in Title Case.

Step 5.
=======

In the :guilabel:`Common Name` field, enter the same name as the :guilabel:`Certificate Name`.

Step 6.
=======

Leave the :guilabel:`Signed By` field blank to designate the certificate as self-signed.

Step 7.
=======

Select the :guilabel:`Certificate Authority` check box.

Step 8.
=======

Leave the :guilabel:`OCSP Responder` field blank; revocation status verification doesn't apply to root CA certificates.

Step 9.
=======

Select the following :guilabel:`Cryptographic Settings`:

    :Algorithm: ``RSA``
    :Number of Bits: ``4096``
    :Digest: ``sha256``
    :Expiration (days): ``3653`` (just over ten years)

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

Step 11.
========

Select :guilabel:`Generate`. A modal will tell you that the certificate and key pair was successfully generated. Select :guilabel:`OK` and then select :guilabel:`Commit`.

Step 12.
========

1. Select the root CA certificate and select :guilabel:`Export Certificate`. Leave :guilabel:`Export Private Key` unselected and choose :guilabel:`OK`. The file will download.
#. Create a document item in 1Password and add the certificate as an attachment. Name the 1Password item:

      :samp:`{PROJECT_NAME} Root CA`

   Replace :samp:`{PROJECT_NAME}` with the name of the project in Title Case. Tag the item with the project's tag, which should also be the name of the project in Title Case. Save the item in the :guilabel:`Shared` vault.


Each user of GlobalProtect will need to install this certificate in the certificate
store of their computer. As part of that process, they must trust the
certificate so that their computer will trust the GlobalProtect server
certificate that will be created in the next step.
