---
title: CAD Modeling Instructions for Pelvic Hip Fracture
---

*Note: Ensure that you follow the steps faithfully to avoid issues and achieve desired results*

## Step 1: Opening and Preprocessing in Autodesk Meshmixer
1. Open `M11_cg_bone_lpelvis.obj` in Autodesk Meshmixer.
2. Select the entire geometry.
3. Navigate to **Edit > Remesh** to reduce the chance of overlapping during offsetting.
4. Accept the Remesh operation.
5. Continue with **Edit > Extrude > Offset** +1.77 mm (direction: normal).
6. Select the geometry again and perform **Edit > Remesh** (optional but beneficial).

## Step 2: Exporting and Transferring to Siemens NX
1. Export the model as an `.obj` file.
2. Transfer the file to Siemens NX on SCOREC computers using WinSCP or hard drive.
3. Save and close the file to individually save convergent bodies as separate `.prt` files.

## Step 3: Performing Subtractions in Siemens NX
1. Open one file and import the second (outer and inner).
2. Navigate to **File > Start > Modeling**.
3. Select the outer part and use the Subtract operation with settings:
   - Subtract Tool from Target. Keep Tool operation.*
4. Repeat the subtraction with the sacrum until a full shell model is created.

## Step 4: Processing the Sacrum Shell
1. To remove the right half of the sacrum: Place a **Datum CSYS** in the middle of the sacrum shell using **Home > Datum CSYS** and position the datum such that there is left-right symmetry.
2. Trim the body using **Trim Body** command after selecting the appropriate plane. You may have to select the **Reverse Direction** option to leave the desired left half remaining.
    - It is advised to trim the cancellous and cortical parts separately.
3. Save as a `.prt`.

## Step 5: Facet Cleanup and Hole Insertion
1. In NX, **Open** the cartilage (`m11_cg_jnt_lsi.obj`) and save it as a part file.
2. Create a new model in Siemens NX and ensure that units are in mm.
2. Import the Sacrum, Cartilage, and Pelvis parts.
2. Use **Facet > Cleanup Facet Body** to clean mesh.
3. Delete all minor extra parts that may appear. 
5. Add a fracture to the sacrum (Note: trim body command would be more efficient, but has proven to be problematic with regard to the meshing)
   -	First, duplicate the entire geometry as it currently exists and make sure its copy is superimposed upon the original
   -	Create another **Datum CSYS**, place it where shear would occur
   -	Create a sketch of a large square of arbitrary size, as long as it encompasses the geometry
   -	Extrude it in one direction (right if observing from the front) such that it covers half of the sacrum and all of the pelvis
   -	Use the subtract command to subtract the box from the part of the bone (choose one of the superimposed copies) which it overlaps 
   -	Repeat the process for the other half, this time deleting from the other superimposed half
   -	This will leave you with one right side and one left side, leaving you with the geometry you had after Step 4, but with a “fracture”
4. Insert a hole:
   - Place a **Datum CSYS** and then **Create Sketch on Plane**.
   - Draw a rectangle going into/through sacrum (~100mm length, 3.66 – 3.67mm radius).
   - **Revolve** the rectangle
   - Select the cylinder and use **Facet Body from Body** to make the new cylinder convergent.
   - Use **Subtract Tool** to remove the cylinder from the bone model (one part at a time).
   - Repeat for the second hole, which should *not* be parallel to the first.

## Step 6: Inserting Screw and Final Steps
1. Open the screw (`screw-7-74.prt`) and remove the Split Bodies and Datum Planes.
2. Import the updated screw part using **Assemblies > Add Component**.
2. Align the screw to the hole using Assembly constraints (**Touch Align** the centerlines first and then use **Distance Align**).
3. Save the entire model as a `.prt` file.
4. Export the final model as a Parasolid binary file  `.x_b`

