##############################
Ignition Development Practices
##############################

Each site is unique and requires some work to tailor our HMI accordingly. The oneline diagram screen is crucial for site operators to monitor substation status and control equipment. This page will detail how to set up a oneline diagram for a new site.

Standard Processes
===============

Using the Dev Server
--------------------
The Dev server is intended to give Ignition engineers a sandbox environment for Perspective development. It is hosted in the CEG office and has Ignition installed without a license. 

    +-----------------------------+----------------------------------------+
    | Server Name                 | Gateway                                | 
    +=============================+========================================+
    | Ignition-DESKTOP-D5IQNS2    | ``172.23.216.107:8088/web/home?0``     |
    +-----------------------------+----------------------------------------+

We can use the Dev server as a remote Designer with tags from a specific site. This is necessary to develop and test HMI screens with tag data for a site. But by default, most sites will not accept tag editing & writing values from remote Designers. Follow these steps to set it up:

#. Log in to the Gateway for the Dev server.
#. Navigate to ``Config > Projects``.
#. Set the default tag provider to the desired site for all projects.
#. Launch the Designer for the Dev server.
#. Set the tag provider to the desired site.

Now you will have a sandbox environment for the desired production site. However, you should still be careful making changes, since the Dev server is the source of truth for future deployments.

Deploying Changes to Production Sites
-------------------------------------
#. Open the Dev Designer and locate your Perspective resources to deploy.
#. Open the Designer for the production site.
#. Copy and paste the Perspective resource into the prod site Designer.
#. Refresh the MultiXRef cache at ``<site URL>/data/perspective/client/MultiXref``
#. Verify everything is working on the site HMI.

Note that any tag changes should follow the procedures outlined in :doc:`./create-tags`.

Changing Default Resources
--------------------------
.. todo:: Fill in this section with a process to update views, components, etc. on the dev server and deploy to existing sites.