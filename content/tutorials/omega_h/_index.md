---
title: Omega_h
description: "Omega_h Installation and Usage"
weight: 1
---

>[Omega_h](https://github.com/SCOREC/omega_h) is a C++14 library that implements tetrahedron and triangle mesh adaptativity, with a focus on scalable HPC performance using (optionally) MPI and OpenMP or CUDA. It is intended to provided adaptive functionality to existing simulation codes.

This is a fork of the [original Omega_h repository](https://github.com/sandialabs/omega_h) of SANDIA Labs. The fork is maintained by the [SCOREC](https://www.scorec.rpi.edu/).

## Find Omega_h on SCOREC machines with CUDA and MPI enabled
1. Compiled without Gmsh: `/lore/mersoj/laces-software/build/PASCAL61/omega_h/install/`
`PASCAL61` is the GPU architecture. Find your GPU architecture with [this tutorial.]({{< ref "/FAQs/find_gpu_arc.md" >}})
2. Compiled with Gmsh: `/lore/hasanm4/Omega_H/`. And the Gmsh executable is in `/lore/hasanm4/Gmsh/`

Remember to add the shared libraries of `gmsh` and `omega_h` to your `LD_LIBRARY_PATH` environment variable if you are using the compiled version of Omega_h.

## Usage of Omega_h
1. Use as a library in PCMS or with any other codes. See pcms tutorial for an example.
2. Use to convert mesh files of other formats to Omega_h format. See [this tutorial]({{< ref "/FAQs/gmsh_and_other_file_formats_to_omegaH_osh_format.md" >}}) as a simple example.

## Compile Omega_h on SCOREC machines (rhel7)
1. Load the necessary modules:
```bash
# you may also need to remove all the previously loaded modules
#module purge
module unuse /opt/scorec/spack/tmod/tinux—rhet7—x86_64/Core
module use /opt/scorec/spack/v0181_1/lmod/linux—rhe17—x86_64/Core
module use /opt/scorec/modules
module load gcc/11.2.0 mpich/4.0.2
module load fftw/3.3.10
module load cuda/11.4
module load cmake/3.20
```
2. Clone the repository:
```bash
git clone https://github.com/SCOREC/omega_h.git
cd omega_h
```
3. Create a config file with the following content:
```bash
cmake -S . -B build \
 -DCMAKE_CXX_COMPILER=`which mpicxx` \
     -DCMAKE_C_COMPILER=`which mpicc` \
     -DCMAKE_INSTALL_PREFIX=/lore/<yourUsername>/Omega_H_OMP/ \
     -DGmsh_INCLUDE_DIRS=/lore/<yourUsername>/Gmsh/include/ \
     -DKokkos_DIR=/lore/<yourUsername>/Kokkos/kokkosInstall/lib64/cmake/Kokkos \
     -DCMAKE_BUILD_TYPE=Debug \
     -DOmega_h_DBG=OFF
```
**Important notes on the flags:** Change the `CMAKE_INSTALL_PREFIX` to your preferred directory. If you want to use Gmsh, change the `Gmsh_INCLUDE_DIRS` to the directory where you have Gmsh compiled and installed. If you don't, remove the line. If you want to use CUDA or OpenMP, change the `Kokkos_DIR` to the directory where you have Kokkos installed. _CUDA/OpenMP will depend on the Kokkos installation._ If you don't want to use CUDA or OpenMP, remove the line. If you want to compile in release mode, change the [`CMAKE_BUILD_TYPE`](https://cmake.org/cmake/help/latest/variable/CMAKE_BUILD_TYPE.html) to `Release` or `RelWithDebInfo`.

4. Build and install:
```bash
sh <yourConfigFile>
cd build
make -j8 install
```
 
