## Alternate OpenSCAD Importer

### NOTICES

Functions such as PrismaticToroid require facilities in the FreeCAD version 0.20 of Part

## Installation

It can be installed via the [Addon Manager](https://github.com/FreeCAD/FreeCAD-addons) (from Tools menu)


## Alternative Installation

Clone into FreeCAD's Mod directory see https://wiki.freecadweb.org/Installing_more_workbenches

   * Change to FreeCAD Mod directory
   * **git clone https://github.com/KeithSloan/OpenSCAD_Alt_Import.git**

* Start/Restart FreeCAD

## Now supports 

* Importing SCAD files as FreeCAD Objects.
* Edit SCADObjects with an external editor

The idea to allow hybrid development ( FreeCAD and OpenSCAD )

### External Editor
  
  For a number of years OpenSCAD has supported an [External Editor](https://en.wikibooks.org/wiki/OpenSCAD_User_Manual/Using_an_external_Editor_with_OpenSCAD)
  
  To use an external editor for SCADObjects
  
  You need to add a parameter to the OpenSCAD workbench
  
      FreeCAD | Tools | Edit parameters
  
      Group : Base App
          Preferences
             Mod
                OpenSCAD
                    externalEditor
                        Text : <path to editor > 
                        e.g. Text /usr/loacl/bin/code

### Use

With the workbench installed when opening a CSG or SCAD File with 


        FreeCAD | File | Open 

the user will be prompted with which importer to use.

![Image 20-02-2023 at 14 29](https://user-images.githubusercontent.com/2291247/220134298-944e8fe6-4ac6-4db7-b072-fe257e0b0905.jpg)

  * SCAD (ImportCSG)                : Uses OpenSCAD to convert SCAD file to CSG and then import as FreeCAD Brep Objects
  * SCADFileObject (ImportFileSCAD) : Imports as a FreeCAD SCADObject. Source remains the original file.
  * SCADObject (ImportSCAD)         : File is copied into FreeCAD and saved with FreeCAD file.
                        
  ### ImportCSG - Import CSG or SCAD file
  
  ### Changes from standard Importer

* **Minkowski** for two objects are colour coded red & green
              rather than use the OpenSCAD binary to produce a meshed minkowski.
              The idea being that a FreeCAD user can then make changes to the indicated objects
              i.e. Add fillets etc to the Red object before deleting the green object.

* **Hull** A limited number of hull requests are converted to BREP equivalents
              
              - Collinear cylinders & cones
              - Two Spheres
              - Two Parallel Cylinders of equal length, orthogonaly displaced.
               
           others are dealt with as per standard importer i.e passed to OpenSCAD
           executable to create a Mesh
           
          
  
  ### SCADFileObject
  
  Created from imported File - Only file reference is saved with the FreeCAD Document
  
  **Properties**
  
  ![Image 20-02-2023 at 14 47](https://user-images.githubusercontent.com/2291247/220137934-2fa7cfc5-23aa-4e03-9130-b9ba89fb133c.jpg)
  
  * edit        : Toggling will invoke the external editor.
  * execute     : Will process the SCAD source ( Object or File ) to create a the Objects Shape.
  * message     : Any error messages from OpenSCAD.
  * mode        : Brep or Mesh.
  * timeout     : time out value for operations passed to OpenSCAD.
  * source      : Source file name
  * source File : Path to source file (ImportFileSCAD)
  
  #### Brep Mode
  
  OpenSCAD is used to create a CSG version that is then imported into a Work document as FreeCAD Objects.
  The Work document is processed to create/update the SCADObjects Shape as a Single Part::Compound
  
  *Brep Propertries*
  
  * fnmax     : Sets the fnmax parameter for the CSG import of this Object
  * keep_work : Option to save or close the Work document
  
  #### Mesh Mode
  
  OpenSCAD is used to create a STL version that is imported to create/update the SCADObjects Shape.
  
  *Mesh Properties*
  
  * mesh_recombine : For future option
    
  ### SCADObjects
  
  Created from imported file - Saved using JSON with the FreeCAD document
  
  For creating FreeCAD objects from SCAD source. 
  Should avoid SCAD files that depend on other files i.e. Have use or include statements.
  
  **Properties** : See SCADFileObjects properties.
  
  ### Using SCADObjects and OpenSCAD external editor.
  
  Using a combination of an external editor for SCADObjects and having OpenSCAD set up for a external editor allows.
  
  * One to edit the source for FreeCAD OpenSCAD objects
  * Preview any changes in a OpenSCAD Preview window
  * When happy with source definition
  
    * Save SCAD Source file
    * Toggle SCADObjects - execute property to have changes brought into FreeCAD

Example Screenshot.
![Image 20-02-2023 at 14 02](https://user-images.githubusercontent.com/2291247/220147105-8689b944-315c-47cc-92f7-c3806b088177.jpg)

                      
### Thanks to FreeCAD Users

* wmayer
* chennes
* edwilliams16
