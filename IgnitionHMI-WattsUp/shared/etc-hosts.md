#####################
Update ``/etc/hosts``
#####################

The ``hosts`` file is a plain text file that maps IP addresses to hostnames or domain names. The ``hosts`` file acts as a local DNS service for your computer. It overrides the mappings from the DNS server that your computer is connected to. You can use the ``hosts`` file to manually link a domain name to an IP address. 

Create Local Host File
======================
The IP Schedule spreadsheet for the project is capable of generating the ``hosts`` file with minimal data input.
For a given project, there are a number of devices that the host machines will need to connect to.
These connections are configured with domain names instead of IPs in order to standardize and simplify networking across sites.
Each site varies in regards to which devices are in the ``hosts`` file, but a good starting place is to populate domain names for each:

* RTU
* PPC
* SRV
* TRK
* ENV
* 30bat
* Any device that starts with 16 e.g. 16ESM
* CLK

Steps
-----
#. The IP Schedule should be located at :samp:`Z:\\CEG\\PROJECTS\\Other Projects\\<PROJECT>\\Design Documents and Data\\SCADA\\Network\\`.
#. In the :guilabel:`Internal` sheet, populate the :guilabel:`/etc/hosts slug` column for each endpoint that Ignition/SQL will talk to. This should automatically populate the :guilabel:`Hosts File` sheet with the desired data.
#. Save the file according to versioning standards.

Update Local Host File
======================
#. The file lives at ``C:\Windows\System32\drivers\etc\hosts`` but this file is usually protected from being edited without elevated priveleges.
#. To edit this file with elevated priveleges, run Notepad or another text editor as Administrator.
#. From the text editor, open the `/etc/hosts` file.
#. Copy the data from the spreadsheet and save. Example:

.. image:: ../img/hosts-example.png

At this point, you can move on to commissioning the servers, and the connection between the database and gateway should work.
After creating the UDTs and tags, Ignition should be able to connect to the devices and poll for data. If this is not the case, revisit the IP schedule and check the IP addresses and corresponding domain names exist in your ``hosts`` file and match the Ignition config.
