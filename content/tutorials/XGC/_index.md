---
title: XGC
description: Installation and usage of XGC
weight: 1
---
{{% alert title="What is XGC?" %}}
XGC is a gyrokinetic particle-in-cell code, which specializes in the simulation of the edge region of magnetically confined thermonuclear fusion plasma. The simulation domain can include the magnetic separatrix, magnetic axis and the biased material wall. XGC can run in total-delta-f, and conventional delta-f mode. The ion species are always gyrokinetic always except for ETG simulation. Electrons can be adiabatic, massless fluid, driftkinetic, or gyrokinetic (for ETG only).
{{% /alert %}}

XGC is a private repository. Ask Princeton Plasma Physics Laboratory (PPPL) for access to the repository. The documentation can be found here: [XGC Documentation](https://xgc.pppl.gov/html/index.html)


## Installation on SCOREC RHEL9
The master (latest commit `5d2cb943a`) or `d2neutral` can be installed with [`spack`](https://spack.readthedocs.io/en/latest/) using the following packages:

```yaml
# This is a Spack Environment file.
#
# It describes a set of packages to be installed, along with
# configuration settings.
spack:
  # add package specs to the `specs` list
  specs:
  - kokkos@4+openmp+serial
  - cabana@0.7.0
  - fftw
  - netlib-lapack
  - googletest
  - libszip
  - hdf5+hl+mpi
  - netcdf-c+mpi
  - netcdf-fortran
  - catch2
  - kokkos-kernels
  - cmake
  - adios2@2.8.0
  - python@3.9
  - petsc@3.15.0+fortran+metis+scalapack ^python@3.9
  view: true
  concretizer:
    unify: true
```

with this compiler configuration:
```yaml
packages:
  cuda:
    externals:
    - spec: cuda@12.1.105
      prefix: /opt/scorec/spack/rhel9/v0201_4/install/linux-rhel9-x86_64/gcc-12.3.0/cuda-12.1.1-zxa4mskqvbkiefzkvnuatlq7skxjnzt6
    buildable: false
  mpich:
    externals:
    - spec: mpich@4.1.1+hydra+libxml2+romio~verbs+wrapperrpath device=ch4 netmod=ofi pmi=pmi
      prefix: /opt/scorec/spack/rhel9/v0201_4/install/linux-rhel9-x86_64/gcc-12.3.0/mpich-4.1.1-xpoyz4tqgfxtrm6m7qq67q4ccp5pnlre
    buildable: false
  gcc:
    externals:
    - spec: gcc@12.3.0 languages:='c,c++,fortran'
      prefix: /opt/scorec/spack/rhel9/v0201_4/install/linux-rhel9-x86_64/gcc-7.4.0/gcc-12.3.0-iil3lnovyknyxf7pec36wljem3fntjd5
      extra_attributes:
        compilers:
          c: /opt/scorec/spack/rhel9/v0201_4/install/linux-rhel9-x86_64/gcc-7.4.0/gcc-12.3.0-iil3lnovyknyxf7pec36wljem3fntjd5/bin/gcc
          cxx: /opt/scorec/spack/rhel9/v0201_4/install/linux-rhel9-x86_64/gcc-7.4.0/gcc-12.3.0-iil3lnovyknyxf7pec36wljem3fntjd5/bin/g++
          fortran: /opt/scorec/spack/rhel9/v0201_4/install/linux-rhel9-x86_64/gcc-7.4.0/gcc-12.3.0-iil3lnovyknyxf7pec36wljem3fntjd5/bin/gfortran
```

Run `spack concretize -f` and `spack install` to install the packages. Now, before installing XGC, the following changes have to be made to the source code:

Following the XGC convention, a file called `CMake/find_dependencies_scorecrh9-spack.cmake`
should be created with the following content:

```cmake
find_package(FFTW3 REQUIRED)
find_package(PETSC REQUIRED)
find_package(LAPACK REQUIRED)
```

To properly install, these files had to be modified too and they are not added to a pull request yet.

1. In `XGC_core/cpp/file_reader.hpp` add the following line:
```cpp
#include <iostream>
```
2. In `libs/camtimers/CMakeLists.txt` replace the following lines:
```cmake
install (FILES ${CMAKE_BINARY_DIR}/perf_mod.mod DESTINATION include)
install (FILES ${CMAKE_BINARY_DIR}/perf_utils.mod DESTINATION include)
```
with these lines:
```cmake
install(FILES ${CMAKE_BINARY_DIR}/libs/camtimers/perf_mod.mod DESTINATION include)
install (FILES ${CMAKE_BINARY_DIR}/libs/camtimers/perf_utils.mod DESTINATION include)
```

Now, to install XGC, activate the spack environment, load the necessary packages and run the following commands:

```bash
export XGC_PLATFORM=scorecrh9-spack

cmake -S . -B build \
  -DCMAKE_Fortran_FLAGS="-fallow-argument-mismatch" \
  -DCMAKE_BUILD_TYPE=RelwithDebInfo \
  -DCMAKE_INSTALL_PREFIX=build/install \
  -DCMAKE_CXX_COMPILER=$MPICXX \
  -DCMAKE_C_COMPILER=$MPICC \
  -DCMAKE_Fortran_COMPILER=$MPIFC
```

{{% alert title="Tips" %}}
If you want to avoid spack totally, all the dependencies have to be manually installed following the versions mentioned in the spack
environment file above.
{{% /alert %}}