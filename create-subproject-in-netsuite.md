###############################
Create a Subproject in NetSuite
###############################

1. Log into NetSuite.

#. Go to :menuselection:`Lists --> Relationships --> Projects --> New`.

#. Set :guilabel:`Custom Form` to :guilabel:`CEG | Project`.

#. Enter a :guilabel:`Project Name` as

      :samp:`{SHORT_CODE} - {SUBPROJECT_NAME}`

   Replace:

   - :samp:`{SHORT_CODE}` with the project code of the parent project without the *CEG* prefix, for example: GRN02

   - :samp:`{SUBPROJECT_NAME}` with the name of the subproject in Title Case, for example: Elk Wind Support

#. Search for the :guilabel:`Customer` name.

#. Enter the :guilabel:`Project Site Location`. If it is at a single site, enter the site as

      :samp:`{CITY_NAME}, {STATE_CODE}`

   Replace:

   - :samp:`{CITY_NAME}` with the name of the nearest city in Title Case

   - :samp:`{STATE_CODE}` with the postal code for the state.

   For example: Greely, IA

   If the subproject is not for a specific site, enter the name of the country in which the work is being done, for example: United States

#. Set a :guilabel:`Start Date` for the subproject.

#. Select a :guilabel:`Project Manager` for the subproject.

#. Set :guilabel:`Will this project have a counterpart in the timesheet app?` to :guilabel:`Yes`.

#. Set :guilabel:`Will this project correspond to a project code or a project subcode?` to :guilabel:`Project Subcode`.

#. Set :guilabel:`Please enter the project code or subcode as it will appear in the timesheet` to the name of the subproject in Title Case.

#. Set :guilabel:`If subcode chosen: Which project is the parent project?` to the parent project.

#. Go to the :guilabel:`Financial` tab and set :guilabel:`Project expense type` to :guilabel:`Regular`.

#. Select :guilabel:`Save`.
