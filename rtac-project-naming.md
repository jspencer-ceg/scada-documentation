###################
Project description
###################

Use the Project Description field in an AcSELerator RTAC project to keep track of a revision history. The first line of the project description is displayed with each project in the AcSELerator RTAC project list window. If you keep the notes for the latest revision in the first line of the Project Description field, you will always be able to see the latest revision when viewing a list of RTAC projects.

Location
========

The Project Description field is found in the tab for the root object in the project tree in the :guilabel:`Project` pane that is shown on the left side of the RTAC project window. The root object will have a name that matches that of the AcSELerator RTAC project's name.

Format
======

Use this format for each revision note in the Project Description field:

   :samp:`{YYYY}-{MM}-{DD} R{DAILY_REVISION_NUMBER} - {INITIALS} ({COMPANY_NAME}): {COMMENT}`

Replace:

* :samp:`{YYYY}` with the four-digit year
* :samp:`{MM}` with the two-digit month
* :samp:`{DD}` with the two-digit day
* :samp:`{DAILY_REVISION_NUMBER}` with the two-digit (zero-padded) revision number for the given date. This starts over at R01 every day. (R00 would be the starting point, which would be the last revision for the previous date.) This number is not a comprehensive versioning number; rather, it is a method to keep changes in order when there are multiple changes per day.
* :samp:`{INITIALS}` with your initials. Use your middle initial if you share first and last initals with someone else in the company.
* :samp:`{COMPANY_NAME}` with the name of your company, for example, ``CEG``
* :samp:`{COMMENT}` with a comment describing the revision in Sentence case. If this is a single sentence, a period is not needed at the end. If there are multiple sentences, use a period to terminate each sentence.


The date and daily revision number shown must match the date and daily revision number shown in the project name.

Revision notes shall be sorted in reverse chronological order—always put the latest revision note on the first line.

A project description with revision history should look something like this::

   2025-04-26 R01 - NTM (CEG): Restored Xcel RTU connection
   2024-04-16 R01 - NTM (CEG): Added logic to force Vestas PPC to RTU control. Changed time zone to Central Standard Time with DST enabled.
   2024-03-15 R01 - NTM (CEG): Added met tower (ENV) points. Updated mappings of phase angles to use CEG_CMV_TO_MV_ANG.
   2023-12-08 R01 - JM (CEG): Added Power Factors list
