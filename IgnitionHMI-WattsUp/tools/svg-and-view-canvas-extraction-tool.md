###################################
SVG and View Canvas Extraction Tool
###################################


Purpose
=======

This tool supports our diagram-building workflow, where view canvas instances and SVG elements are stored within memory document tags.

* The input for this tool is a view, such as a coordinate view, with a single SVG and multiple regular embedded views.
* 

Tabs
====

1. Raw View JSON
   As retrieved from the filesystem
1. Extracted SVG
   The "elements" and "position" keys needed to drive a document tag for SvgSource.
1. Extracted Canvas
   The "instances" array need to drive a live document tag.  Simply converting embedded views into canvas instances format.
1. Worksheet Canvas
   The extract canvas JSON with the substitutions of `%(UdtInstancePath)s` or similar to make that JSON appropriate for use in the deployment worksheets.

The missing tab of the tool is the controls for loading an actual pair of document tags, in the folder chosen in the right-hand tree view.
