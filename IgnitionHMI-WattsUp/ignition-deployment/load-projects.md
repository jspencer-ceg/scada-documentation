#############
Load Projects
#############

The Golden GWBK contains some projects, but they are not kept up to date with latest changes in dev, and there are additional projects that are not included, but are required for Watts Up to function correctly.
This procedure walks through the process of copying the projects from the dev server to the remote server.

Download Latest Projects
========================
#. Log in to the Dev Gateway (hosted on *Ignition-DESKTOP-D5IQNS2* ``172.23.216.107``).
#. Navigate to :menuselection:`Config --> Projects` where you will see a list of all the projects.
#. Export the required projects via :menuselection:`More --> Export` on the right side of the project list. The required projects are:
    
    * MultiXref
    * background
    * ceg_ppc
    * ceg_utils
    * perspective_common
    * site_constants
    * spreadsheet-import-tool
    * tag_events
    * universe

Load Latest Projects
====================
#. On the remote/site host, navigate to the same :menuselection:`Config --> Projects` location from the previous section.
#. At the bottom of the list, click :guilabel:`Import project...`.
#. Choose :guilabel:`Browse...` and select the project that you downloaded in the previous step.
#. Make sure the :guilabel:`Project Name` matches the original name, and check the box for :guilabel:`Allow Overwrite`.
#. Click :guilabel:`Import` and the project should successfully load.
#. To the right of the new project, click :guilabel:`Edit` and set the following:

    #. User Source: ``default``
    #. Default Database: ``LocalIgnitionDB``
    #. Default Tag Provider: ``{SiteNameSolar}``

#. Do this for all of the above listed projects and any additional projects that may be required at a site.

Establish Connection to Dev Server
==================================
#. Log in to the Dev Gateway.
#. Navigate to :menuselection:`Config --> Tags --> Realtime`
#. Select ``Create new Realtime Tag Provider`` and choose ``Remote Tag Provider``
#. Type the Ignition server name, like ``WTL-SRV-3``
#. Fill out the settings like another existing site.
    #. Main > Name: ``Prod_SiteNameSolar``
    #. Remote Gateway > Gateway: ``<Ignition server name>``
    #. Remote Gateway > Provider: ``SiteNameSolar``
#. Log in to the remote Gateway.
#. Navigate to :menuselection:`Config --> Networking --> Gateway Network --> Outgoing Connections`.
#. Find the faulted **outgoing** connection to the Staging Environment and approve it.
#. Back on the Dev Gateway, navigate to :menuselection:`Config --> Networking --> Gateway Network --> Incoming Connections`.
#. Approve the **incoming** connection.
#. Observe the successful outgoing connection on the remote Gateway.
#. Finally, launch the Dev Designer and select the tag provider to see the tags.


Note that these connections will attempt to establish upon restore.

