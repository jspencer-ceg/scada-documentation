################################
Work with connection directories
################################

There are two types of connections that you use when you use AcSELerator RTAC:

- When you first log into the software, you log into a project database. Usually, this is a database that is stored on your local hard drive, but it is possible to log into databases that are stored on other computers on the network.
- Connections to RTACs to send settings and to go online.

AcSELerator RTAC can save directories of connections for each of these types of connections. You can back up these directories and use them with another AcSELerator RTAC installation.

********************************************
Save an AcSELerator RTAC database connection
********************************************

To save a database connection, enter a :guilabel:`Connection Name` along with the :guilabel:`Server` address, :guilabel:`Database` name, :guilabel:`Port` number, and :guilabel:`User Name`. This information will be saved after you select :guilabel:`Login`.

   .. image:: img/connections/acrtac-save-database-connection.png
      :scale: 50 %
      :align: center

***********************
Save an RTAC connection
***********************

To save an RTAC connection, enter a :guilabel:`Connection Name` along with the :guilabel:`RTAC Address`, :guilabel:`User Name`, and :guilabel:`Port`. This information will be saved after you select :guilabel:`Login`.

For :guilabel:`Connection Name`, use a name in the form:

   :samp:`{SITE_NAME} {DEV_NUM}`

Replace the following:

   - :samp:`{SITE_NAME}`: name of the project in title case
   - :samp:`{DEV_NUM}`: the device number of the RTAC, including any hyphens

   .. image:: img/connections/acrtac-save-rtac-connection.png
      :scale: 50 %
      :align: center

*******************
Back up a directory
*******************

1. Exit AcSELerator RTAC.

#. In :guilabel:`File Explorer`, go to ``%LocalAppData%\SEL\AcSELerator\RTAC\Connections``.

#. This folder contains at least two files:

   - ``RTAC.csv``: Contains a directory of connections to AcSELerator RTAC databases.
   - ``SEL3530.csv``: Contains a directory of connections to RTACs.

   Select the files you want to back up and save them to your backup location.

******************
Import a directory
******************

1. Exit AcSELerator RTAC.

#. In :guilabel:`File Explorer`, go to ``%LocalAppData%\SEL\AcSELerator\RTAC\Connections``.

#. Copy the directory files that you wish to import into this folder, overwriting the files that are already there.

.. warning ::

   If the existing files already contain connection information, you will lose this data if you overwrite those files.

