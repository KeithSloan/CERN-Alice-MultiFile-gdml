# CERN-Alice-MultiFile-gdml

One of the aims of this exercise/project is to provide a testing/proving ground for the the FreeCAD GDML workbench

https://github.com/KeithSloan/GDML. 

At present the workbench struggles with large GDML files, this is down to two reasons

1. Software Bugs
2. Slowness of the Python code.

In an attempt to address these isssues the Workbench offers a facility to **scan** rather than import a GDML file.

The scan just parses the file for first level GDML Volumes (Base Volumes) which it then indicates as **NOT Expanded**.
The workbench then offers two facilites to select an individual  **NOT Expanded** Volume and expand it.
Having expanded an individual Volume, if one then selects the root/world volume ( First / highlest level App::Part in FreeCAD ) and invoke the standard FreeCAD export facility, one then can create a GDML file for just the selected expanded volume. This can either be a single GDML file if the file extension used is lower case **gdml** or a multi files version. If an upper case **GDML** file extension is used then the path name without the **GDML** is used to create a directory which includes a gdml file that has includes for individual XML files for the various sections of a GDML file namely

* Constants
* Defines
* Materials
* Solids
* Structure

One can then deleted the expanded Volume and repeat the exercise for another base GDML Volume (First level FreeCAD App::Part) 

In addition it is possible to select the root/world volume and use the standard FreeCAD facility to export a STEP file version.

The idea being that having created such directories, then it should not be too arduous to create a gdml file that would recombine base volumes.
i.e. a GDML file with includes for the common sections and a number of individual files (Solids and Structure).

Obviously a combination of all base voumes would still be an issue for the Workbench, but should be loadable into Geant4. For ROOT that does
not support imbeded GDML files, then one should be able to use the supplied standalone python utility **CombineGDML.py** ( in the Workbenches **Utils** directory)
to process the Multi-file GDML version and produce a single file GDML version.

At the present time it is bugs in the workbench handling of GDML assemblies that is holding up this project/exercise

The plan is also to add the facility to the workbench to import XML files with solids and structure definitions so that one could work on the GDML
of a Base Volume whilst also having neighbouring base volumes loaded.
