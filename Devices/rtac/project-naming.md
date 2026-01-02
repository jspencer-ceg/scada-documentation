##############
Project naming
##############

Name RTAC projects consistently so that they stay ordered in the RTAC's project list window and so the ordering is maintained when you share RTAC projects with other engineers. Projects should first be ordered by project name, RTAC device number, date and then by the revision of the day.

Format
======

Use this format for an RTAC project name:

   :samp:`{PROJECT_NAME} {DEVICE_NUMBER} {YYYY}-{MM}-{DD} R{DAILY_REVISION_NUMBER} {COMMENT}`

Replace:

* :samp:`{PROJECT_NAME}` with the project's name in Title Case
* :samp:`{DEVICE_NUMBER}` with the device number for the RTAC. If the project file applies to two RTACs, such as in a redundancy scheme, you may use "or" to list both, for example, ``RTU-1 or RTU-2``.
* :samp:`{YYYY}` with the four-digit year
* :samp:`{MM}` with the two-digit month
* :samp:`{DD}` with the two-digit day
* :samp:`{DAILY_REVISION_NUMBER}` with the two-digit (zero-padded) revision number for the given date. This starts over at R01 every day. (R00 would be the starting point, which would be the last revision for the previous date.) This number is not a comprehensive versioning number; rather, it is a method to keep changes in order when there are multiple changes per day.
* :samp:`{COMMENT}` with an optional comment, in Sentence case. Use this to add any specific notes to a version that you may want to keep track of.

Use spaces, not underscores, to separate these elements.

For example, a project file for Fillmore Solar's RTU-1 would be:

   ``Fillmore Solar RTU-1 2025-01-28 R02``

Proper use of this scheme will result in a neatly sorted list, grouped by project, then RTAC, and then by date::

   Fillmore Solar RTU-1 2024-09-12 R01
   Fillmore Solar RTU-1 2024-09-12 R02
   Fillmore Solar RTU-1 2024-11-12 R01
   Fillmore Solar RTU-1 2025-01-28 R01
   Fillmore Solar RTU-1 2025-01-28 R02
   Hornshadow Solar PPC-1 2025-02-25 R01
   Hornshadow Solar PPC-1 2025-03-30 R01
   Hornshadow Solar RTU-1 2024-11-30 R01
   Hornshadow Solar RTU-1 2024-12-20 R01

When to start a new revision
============================

The following reasons are good times to start a new revision of an RTAC project:

* When you make significant changes to a project, and you want to be able to return to the previous project's state
* When you are making changes to an RTAC project that has been running on the RTAC for some time
* When you are working collaboratively with another engineer on the project and you need to make a change, so that the other engineer can see that a change was made from the change in project name.

Not every little change needs a new name for the project, such as when you are working on a file and actively troubleshooting.

The date that you use in the name can be flexible. It can either be the day that you are working on a change, or the day that you eventually upload the project to the RTAC. Oftentimes, you are uploading on the same day as a change, and so the difference is moot.


