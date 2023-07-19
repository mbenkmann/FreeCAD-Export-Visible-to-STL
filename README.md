# <img src="https://github.com/mbenkmann/FreeCAD-Export-Visible-to-STL/blob/master/icons/Stl.svg" style="width:1em; vertical-align:middle"> FreeCAD-Export-Visible-to-STL  

Tesselates all visible objects, combines them into a single mesh and exports it as `<documentname>.stl`, where `<documentname>`
is the name of the source document, or `"unnamed.stl"` if the document has not been saved, yet. After the export the macro
can optionally run an external program, e.g. a slicer for 3D printing.

This macro supports `App::Link` objects, including those that link to external documents.

This macro does *NOT* modify the source document in any way, not even temporarily. The tesselation parameters for
deviation in particular are *NOT* temporarily written into the objects' `View`, unlike another STL export macro I've seen.

# Configuration parameters

The macro can be configured via `Tools/Edit Preferences.../BaseApp/Preferences/ExportSTL`. This parameter group will appear
after you run the macro once (even without an open document).

The following parameters are supported:

### AlwaysExportIntoThisDirectory (string)

If this parameter is empty, the exported .stl file will be written to the same directory that contains the source
document (or the current working directory of FreeCAD, in the case of "unnamed.stl").

If this parameter is non-empty, it is treated as a directory path that all exported .stl files will be written to,
regardless of where their source documents are located. This option is particularly useful for people who use the .stl files
only temporarily (e.g. for 3D printing) and don't want to keep them. In this case you would set this parameter to the
path of a temporary or cache directory.

### CommandAfterExport (string)

If this parameter is non-empty, it will be executed as a shell command after the export. You can use this to launch a slicer,
for instance. If the parameter includes the word `STLFILE` (in all caps) anywhere, all such occurences will be replaced
with the path of the exported file. If the parameter does not include `STLFILE`, the path of the exported file will be
appended to the end of the command, separated by a space.

**Note:** Be sure to obey the syntax rules for a shell command, e.g. with respect to spaces, quotes, backslashes etc.

### LinearDeflectionMillimeters (float)

This corresponds to the setting `Surface deviation` when you do a manual tesselation on the `Mesh Design` workbench using
`Create mesh from shape...` with the `Standard` algorithm. It is specified in millimeters.

### AngularDeflectionDegrees (float)

This corresponds to the setting `Angular deviation` when you do a manual tesselation on the `Mesh Design` workbench using
`Create mesh from shape...` with the `Standard` algorithm. It is specified in degrees (NOT radians!).

