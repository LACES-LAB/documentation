---
title: Sterllerator Related Tools
description: "Installation and Usage of Sterllerator Related Tools: Beams3D, BMW"
weight: 1
---
[This jupyter notebook](https://gist.github.com/Fuad-HH/fce7e3a7161920a0aaf1bec3825c5040) shows how to open the Beams3D and BMW output and plot the magnetic fields. It is found that both of them generates the same magnetic field.

## BMW
### Installation on SCOREC machines (rhel9)
**Note**: To find the RHEL version of the machine you are on, you can use the following command:
```bash
    cat /etc/redhat-release
```

This is the recommended way of BMW installation since most of the SCOREC machines are now RHEL9. This process only works on RHEL 9 machines of SCOREC and was tested on 13th June 2024. Some modules may change in the future.

1. Go to your intended installation directory with `cd` (`/lore/<username>/` recommended, see more details about space management [here](https://laces-lab.github.io/documentation/faqs/scorec_machine_space_management/)) and clone the repository:
```bash
    git clone https://github.com/ORNL-Fusion/Stellarator-Tools.git
```
2. Enter the directory and create a build directory:
```bash
    cd Stellarator-Tools
    mkdir build
    cd build
```
3. Load necessary modules: (ignore the warnings)
```bash
   module use /opt/scorec/spack/rhel9/v0201_4/lmod/linux-rhel9-x86_64/Core/
   module load gcc/12.3.0-iil3lno mpich/4.1.1-xpoyz4t cuda/12.1.1-zxa4msk
   module load cmake 
   module load netcdf-c netcdf-fortran openblas netlib-scalapack
```
4. Run cmake with the following command:
```bash
    cmake -B ./ -S ../ -DBUILD_BMW=ON -DBUILD_MAKEGRID=ON -DCMAKE_INSTALL_PREFIX=/lore/<username>/BMW
```
Change the installation directory as per your requirement.
5. Build and install:
```bash
    make -j4
    make install
```

6. To use the installed `xmbw` and `mgrid`, the shared library paths need to be updated. Execute the following export commands before using them.
```bash
    export LD_LIBRARY_PATH=$OPENBLAS_RHEL9_ROOT/lib:$LD_LIBRARY_PATH
    export LD_LIBRARY_PATH=$NETLIB_SCALAPACK_RHEL9_ROOT/lib:$LD_LIBRARY_PATH
    export LD_LIBRARY_PATH=$NETCDF_FORTRAN_RHEL9_ROOT/lib:$LD_LIBRARY_PATH
    export LD_LIBRARY_PATH=$NETCDF_C_RHEL9_ROOT/lib:$LD_LIBRARY_PATH
```

**Note:** Every time you want to use `xmbw` or `mgrid` on a new terminal, you need to export the shared library paths after loading the necessary modules(step 3).


### Installation on SCOREC machines (rhel7)
This GitHub reporsiory contains the source code and brief installation guide of BMW: [BMW](https://github.com/ORNL-Fusion/BMW).

_Note: Direct compilation did not work for me. I used [Stellarator-Tools](https://github.com/ORNL-Fusion/Stellarator-Tools) supplied by ORNL-Fusion._

1. Clone the repository:
```bash
    git clone https://github.com/ORNL-Fusion/Stellarator-Tools.git
```
2. Go the the directory and create a build directory:
```bash
    cd Stellarator-Tools
    mkdir build
    cd build
```
3. Load the necessary modules:
```bash
    module unuse /opt/scorec/spack/lmod/linux-rhel7-x86_64/Core
    module use /opt/scorec/spack/v0201_4/lmod/linux-rhel7-x86_64/Core
    module load gcc/11.2.0-zcqgw mpich/4.1.1-6p32n

    module load netcdf-c cmake netcdf-fortran openblas netlib-scalapack
```
4. Run cmake: **You can also follow the `ccmake` method from the repository README.** But I recommend the following:
```bash
     cmake -B ./build -S ./ -DBUILD_BMW=ON -DCMAKE_INSTALL_PREFIX=/lore/<yourUsername>/BMW
```
5. Build and install:
```bash
    make -j4 install
```
or 
```bash
    make -j4
```
This will create the `bmw` executable in the `bin` directory of the installation directory.


6. Update the shared libraries (`xbmw` will keep printing error messages until it finds all the
shared libraries): (_These directories may change depending on the modules loaded for installation_)
```bash
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/scorec/spack/v0201_4/install/linux-rhel7-x86_64/gcc-11.2.0/openblas-0.3.23-4kpgzbwtvvnf4m4f6rqvyclh2khpfepb/lib
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/scorec/spack/v0201_4/install/linux-rhel7-x86_64/gcc-11.2.0/netlib-scalapack-2.2.0-w3lmjdvbshpvqiihwxm2fygyjyzu275t/lib
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/scorec/spack/v0201_4/install/linux-rhel7-x86_64/gcc-11.2.0/netcdf-c-4.9.2-hzgyaz36ol6aqb4o3ne3xjabccpxjlo4/lib
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/scorec/spack/v0201_4/install/linux-rhel7-x86_64/gcc-11.2.0/netcdf-fortran-4.6.0-hwoxscrowy6gh75n5ypnlr3btfver36x/lib
```

### Usage of BMW: Run a case from [VMEC Equillibria](https://github.com/landreman/vmec_equilibria)
There can be two kinds of use cases for `bmw`: the coil generated magnetic filed is considered or
they are not considered. If you don't need the coil generated magnetic field, you just need the `wout_...nc` file and follow the steps below.

1. Go to the directory where you have the case files (e.g. `vmec_equillibria/NCSX/free_boundary_from_vmec_wiki`):
```bash
    cd vmec_equillibria/NCSX/free_boundary_from_vmec_wiki
```
You can create the `wout_...nc` file using `vmec` or use the provided `wout_...nc` file as the input to `bmw`.

2. Run `bmw`:
```bash
    /lore/<yourUsername>/BMW/bin/xbmw -num_r=100 -num_p=20 -num_z=100 -rmax=1.5 -rmin=0.9 -zmax=0.5 -zmin=-0.5 -woutf=wout_ncsx_c09r00_free_birth.nc -outf=bmw_ncsx_c09r00_out.nc
```
This will produce the `bmw_ncsx_c09r00_out.nc` file in the current directory.

4. To read the output file, you can use python and the `netCDF4` library. Here in this Jupyter Notebook file, I have plotted the magnetic field from the output file. [GitHub Gist for Analysis](https://gist.github.com/Fuad-HH/fce7e3a7161920a0aaf1bec3825c5040)

#### Using Coil Generated Magnetic Field
1. Check if the coils file given in the case directory. Generally, it's given and name as `coils.xxxxx`.
2. Change the `ier_flag` in the `wout_...nc` file to `0` before starting the `bmw` run. You can modify `.nc` files in python using the `netCDF4` library.
```python
    import netCDF4 as nc
    wout = nc.Dataset('wout_ncsx_c09r00_free_birth.nc', 'r')
    wout.variables['ier_flag'][:] = 0
    wout.close()
```
3. BMW only accepts coils file in `mgrid` format. So, convert the `coils.xxxxx` file to `mgrid` format using the following command:
```bash
    /lore/<yourUsername>/BMW/bin/mgrid < input_file.txt
```
To know how to create an input file for `mgrid`, check this STELLOPT [MAKEGRID Tutorial](https://princetonuniversity.github.io/STELLOPT/VMEC%20Free%20Boundary%20Run#:~:text=periodicity%20of%20three.-,Create%20the%20%E2%80%98mgrid%E2%80%99%20file,-First%20one%20must). Note that their binary name is `xgrid` but in the BMW installation, it's `mgrid`.

4. Run `bmw` with the `mgrid` file generated in the above step. In this case, you don't have to specify
the parameters for the grid since the grid is already provided by the `mgrid` file.
```bash
    /lore/<yourUsername>/BMW/bin/xbmw -woutf=wout_ncsx_c09r00_free_birth.nc -outf=bmw_ncsx_c09r00_out.nc -mgridf=mgrid_xxxx.nc
```

This will take a long time to run depending on the grid size. You can also do parallel run using `mpirun` and `-para` flag.

## Beams3D
### Installation on SCOREC Machines

**I am not able to compile the STELLOPT tool on scorec yet. The installation instructions given in the [STELLOPT README](https://github.com/PrincetonUniversity/STELLOPT) is not working.**

If you have access to the PPPL clusters (e.g. stellar), they have compiled STELLOPT tools. You can use them directly.
```bash
    ssh stellar-intel
    module use /home/caoxiang/module
    module load stellopt/intel 
``` 
Learn more about it [here](https://princetonuniversity.github.io/STELLOPT/STELLOPT%20Compilation%20at%20PPPL)

#### Using Docker Image
I used the docker image of STELOPT to run Beams3D where all the necessary tools are already installed. The docker image is available at [Docker Hub](https://hub.docker.com/r/zhucaoxiang/stellopt).

1. Get the docker image:
```bash
    docker pull zhucaoxiang/stellopt
```
2. Run the docker image depending on your OS. SCOREC does not support docker yet. So, I used my own computer. You may also want to run the docker as root user since the image doesn't support writing any file for non-root users.
```bash
    docker run -it -u root zhucaoxiang/stellopt
```
3. The NAG library is also needed to be installed but it is a proprietary software. A trial version(for 30 days) can be found [here](https://nag.com/nag-library/). Installation is very straightforward. Just follow the instructions given in the website.

According to their documentation, you can avoid NAG and use `LSODE` instead. Try changing the NAG flag to `F` in the `make_debian.inc` file as well as changing the `INTEGRATOR` flag to `LSODE`. If you succeed, please add in the documentation or create an issue.

4. After nag installation, add NAG to the environment using the following command:
```bash
    source /home/NAG/nll6i293bl/scripts/nagvars.sh int64 vendor dynamic
```
5. Then, follow the [Beams3D tutorial](https://princetonuniversity.github.io/STELLOPT/BEAMS3D%20NCSX%20Deposition%20Example.html) to run Beams3D. I used the following command after editing the input file.
```bash
    xbeams3d -vmec ncsx_c09r00_free_birth -coil coils.c09r00 -vessel NCSX_wall_nbiport_acc.dat -field
```
6. It will create a `.h5` file and it can be read by python. Magnetic field data is read in this [Jupyter Notebook](https://gist.github.com/Fuad-HH/fce7e3a7161920a0aaf1bec3825c5040)