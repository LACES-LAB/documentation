---
title: Meshing Instructions for Hip Model
---

1. **Importing Geometry:**
   - Open SimModeler
   - If the file is in parasolid format, go to **File → Import Geometry**. For files in .obj or .stl format, choose **Import Discrete Data**.


2. **Preparing for meshing:**
   - Navigate to the **Modeling** tab, choose **Delete Parts**, and select the screws.
   - In the **Meshing** tab, click on **Generate Mesh**. Uncheck "Structured Mesh" and proceed. Upon successful generation, view the mesh by selecting **Show Mesh**, which creates an `.sms` file. (Remember to return to the `.smd` file for generating a new mesh if required.)


3. **Refining Mesh:**
   - Use **Mesh Attributes** located on the right-hand side of the screen.
   - The following chart represents some suggested Mesh Attributes and corresponding values:
        | Type                       | Sub-Type                    | Value   |
        |----------------------------|-----------------------------|---------|
        | Mesh Size                  | Absolute                    | 0.001   |
        | Mesh Curvature Refinement  | Absolute                    | 0.005   |
        | Volume Shape Metric        | Aspect Ratio                | 3.0     |
        | Allow Refinement For Shape | Relative                    | 0.0001  |
   - After making refinements, regenerate the mesh to incorporate the changes.


4. **Quality Check:**
   - Assess the quality of the mesh by going to the `.sms` file and navigating to the **Display Tab**.
   - Click **Mesh Stats** and scrutinize the Aspect Ratio.


5. **Exporting Mesh:**
   - To export the mesh, navigate to **File > Export Mesh**. 
   - Save the file if not done previously. 
   - Choose the export format as **Abaqus 3D** `(.inp)`.


6. **Meshing Screws Separately:**
   - Follow the same steps as for the bone meshing process for the screws.
