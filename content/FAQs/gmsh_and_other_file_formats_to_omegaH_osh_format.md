---
title: Convert Gmsh and other meshes to Omega_h OSH format
---

Common types of mesh files can be converted to Omega_h's OSH format using the omega_h utility programs. Find more details about the utility programs in the [Omega_h documentation](https://github.com/SCOREC/omega_h/files/8468421/omega_h.pdf). The following examples show how to convert Gmsh to OSH format.

### Convert Gmsh to OSH format
1. Find the utility programs in the SCOREC machines. You can find them in the following directories:
    - `/lore/hasanm4/Omega_H/bin/` (if it is not available, you can contact us or build it from the source code)
2. Add the directory to your `PATH` environment variable. For example, if you are using bash, you can execute the following command:
    ```bash
    export PATH=/lore/hasanm4/Omega_H/bin/:$PATH
    ```
3. Add the directory to your `LD_LIBRARY_PATH` environment variable using the following command:
    ```bash
    export LD_LIBRARY_PATH=/lore/hasanm4/Omega_H/lib64/:$LD_LIBRARY_PATH
    ```
4. Gmsh is also needed to convert the mesh to Omega_h format. Get the Gmsh executable using the following command:
    ```bash
    export PATH=/lore/hasanm4/Gmsh/bin/:$PATH
    export LD_LIBRARY_PATH=/lore/hasanm4/Gmsh/lib64/:$LD_LIBRARY_PATH
    ```
5. Now the environment should be ready for the conversion. If you have `.geo` mesh script file, you can convert it to `.msh` file using the following command:
    ```bash
    gmsh -3 -format msh2 -order 1 -o mesh.msh mesh.geo
    ```
    (**it must be of order 1** and here mesh format 2 is shown since it was used for with MFEM and MFEM only supports mesh format 2)
    _(consult the Gmsh documentation for more details about the command line options)_

**Important notes:** Omega_h supports both 2D and 3D meshes with triangles and tetrahedra. **It does not support quadrilaterals, prisms, and hexahedra.** (_omega_h can only accept linear simplices and hypercubes from Gmsh_) Make sure that the mesh is composed of linear triangles and tetrahedra. [Gmsh documentation](https://gmsh.info/doc/texinfo/gmsh.html#MSH-file-format:~:text=In%20the%20format%20description%20above%2C%20elementType%20is) has more details about the element types.

6. Now the mesh is ready to be converted to OSH format. Use the following command to convert the mesh to OSH format:
    ```bash
    gmsh2osh mesh.msh mesh.osh
    ```