---
title: Sterllerator Related Tools
description: "Installation and Usage of Sterllerator Related Tools: Beams3D, BMW"
weight: 1
---

## BMW
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

### Usage of BMW: Run a case from [VMEC Equillibria](https://github.com/landreman/vmec_equilibria)

1. Update the shared libraries (`xbmw` will keep printing error messages until it finds all the
shared libraries): (_These directories may change depending on the modules loaded for installation_)
```bash
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/scorec/spack/v0201_4/install/linux-rhel7-x86_64/gcc-11.2.0/openblas-0.3.23-4kpgzbwtvvnf4m4f6rqvyclh2khpfepb/lib
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/scorec/spack/v0201_4/install/linux-rhel7-x86_64/gcc-11.2.0/netlib-scalapack-2.2.0-w3lmjdvbshpvqiihwxm2fygyjyzu275t/lib
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/scorec/spack/v0201_4/install/linux-rhel7-x86_64/gcc-11.2.0/netcdf-c-4.9.2-hzgyaz36ol6aqb4o3ne3xjabccpxjlo4/lib
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/scorec/spack/v0201_4/install/linux-rhel7-x86_64/gcc-11.2.0/netcdf-fortran-4.6.0-hwoxscrowy6gh75n5ypnlr3btfver36x/lib
```
2. Go to the directory where you have the case files (e.g. `vmec_equillibria/NCSX/free_boundary_from_vmec_wiki`):
```bash
    cd vmec_equillibria/NCSX/free_boundary_from_vmec_wiki
```
You can create the `wout_...nc` file using `vmec` or use the provided `wout_...nc` file as the input to `bmw`.

3. Run `bmw`:
```bash
    /lore/<yourUsername>/BMW/bin/xbmw -num_r=100 -num_p=20 -num_z=100 -rmax=1.5 -rmin=0.9 -zmax=0.5 -zmin=-0.5 -woutf=wout_ncsx_c09r00_free_birth.nc -outf=bmw_ncsx_c09r00_out.nc
```
This will produce the `bmw_ncsx_c09r00_out.nc` file in the current directory.

4. To read the output file, you can use python and the `netCDF4` library. Here in this Jupyter Notebook file, I have plotted the magnetic field from the output file. [GitHub Gist for Analysis](https://gist.github.com/Fuad-HH/fce7e3a7161920a0aaf1bec3825c5040)

## Beams3D
### Installation on SCOREC machines (rhel7)

**I am not able to compile the STELLOPT tool on scorec. The installation instructions given in the [STELLOPT README](https://github.com/PrincetonUniversity/STELLOPT) is not working.**
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
4. After nag installation, add NAG to the environment using the following command:
```bash
    source /home/NAG/nll6i293bl/scripts/nagvars.sh int64 vendor dynamic
```
5. Then, follow the [Beams3D tutorial](https://princetonuniversity.github.io/STELLOPT/BEAMS3D%20NCSX%20Deposition%20Example.html) to run Beams3D. I used the following command after editing the input file.
```bash
    xbeams3d -vmec ncsx_c09r00_free_birth -coil coils.c09r00 -vessel NCSX_wall_nbiport_acc.dat -depo
```
6. It will create a `.h5` file and it can be read by python. Magnetic field data is read in this [Jupyter Notebook](https://gist.github.com/Fuad-HH/fce7e3a7161920a0aaf1bec3825c5040)