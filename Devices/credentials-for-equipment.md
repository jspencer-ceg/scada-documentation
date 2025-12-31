# Credentials for Equipment

User logins for applications hosted on different hardware will generally follow the same scheme. Except for Ignition, most devices make use of individual user accounts instead of shared accounts. Still, credentials are created with the following pattern:

    :Username: ``<first initial><last name>``
    :Password: ``<PROJ><equipment abbreviation>!``

``<PROJ>`` is the shortened project name, with only the first letter capitalized. It is found by referencing the drawings for the given project, stored at ``Z:\CEG\PROJECTS\Other Projects\<Project Code> <Project Name>\Drawings``. It is typically a four-letter abbreviation, but may be different for some sites. The drawings will be labeled like ``<PROJ>-CA-01`` and so forth.

In order to find the project code so you can locate the folder with the drawings, you can utilize the `Project Index <https://ceg-project-tracker-testing.herokuapp.com/index.php/projectindexnew>`_ and search using the common name.

    :Example: ``Garnet Mesa``
    :Project Code from Index: ``CEGPRIM37``
    :Project Code from Drawings: ``GARN``

The ``<equipment abbreviation>`` is the four-character code in the model name of the device. It can be found if you reference the drawings for site and locate the equipment being used. Here are a few common ones:

    * Onlogic K802
    * SEL-3355
    * SEL-3530


Password Examples
-----------------

    * GarnK802!
    * Iris3355!

Ignition Logins
---------------
Most Ignition deployments are hosted on Onlogic K802 servers, with some exceptions for old sites hosted on SEL-3355s. These users exist at every site with Ignition deployed. If ``K802`` does not work, try ``3355``. 

You should log in as the user with the least permissions for the work you need to complete.

+-------------+------------------+---------------+------------+-----------------+----------------+
| Username    | Password         | Role          | HMI Access | Enable Commands | Gateway Config |
+=============+==================+===============+============+=================+================+
| ceguser     | <PROJ>K802!      | ReadOnly      | X          |                 |                |
+-------------+------------------+---------------+------------+-----------------+----------------+
| cegoperator | <PROJ>K802!      | Operator      | X          | X               |                |
+-------------+------------------+---------------+------------+-----------------+----------------+
| cegadmin    | <PROJ>AdminK802! | Administrator | X          |                 | X              |
+-------------+------------------+---------------+------------+-----------------+----------------+


Default Credentials for Radian Generation
-----------------------------------------
When Radian Gen needs access a site, these default credentials should be used for all device logins:

    :Username: ``radiangen``
    :Password: ``DESRI-Radian-Default!192.168.xxx.0``

Where ``xxx`` is replaced with the site's octet.
