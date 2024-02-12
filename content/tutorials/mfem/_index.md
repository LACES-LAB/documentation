---
title: MFEM
description: "MFEM Installation and Tutorials"
weight: 1
---

>[MFEM](mfem.org) is a free, lightweight, scalable C++ library for finite element methods.

### MFEM Installation
MFEM installation information can be found [here](https://mfem.org/building/). Follow the appropriate installation instructions according to your necessity.

More detailed guide can be found in this [README file](https://github.com/mfem/mfem/blob/master/INSTALL). This might be needed to build MFEM with custom options for example linking with other libraries.

#### Installation using cmake on SCOREC machines
1. Clone the mfem repository
```bash
git clone https://github.com/mfem/mfem.git
```
or get the tarball from [here](https://mfem.org/#:~:text=based%20on%20MFEM.-,Latest%20Release,-New%20features%20%E2%94%8A).

2. Load the necessary modules
```bash
module unuse /opt/scorec/spack/tmod/tinux—rhet7—x86_64/Core
module use /opt/scorec/spack/v0181_1/lmod/linux—rhe17—x86_64/Core
module use /opt/scorec/modules
module load gcc/11.2.0 mpich/4.0.2
module load cmake/3.20
```
3. Install `hypre` and `metis` using these instructions from [MFEM website](https://mfem.org/building/#:~:text=Build%20hypre%3A,instructions%20below.). They showed the installation process for `metis-4.0`
but I used `metis-5.1.0` and it worked fine.

4. Create a configuration file with the following content
```bash
cmake -S mfem-4.6 -B mfem-build \
  -DMETIS_DIR=metis-5.1.0 \
  -DMFEM_USE_MPI=ON \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DCMAKE_INSTALL_PREFIX=/lore/<your_username>/mFEM/install/mfem-mpi
```
change `<your_username>` to your username. It's preferable to use the `/lore` directory for installation.
Read more about storage management on SCOREC machines in the FAQ section.