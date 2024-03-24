---
title: Building Kokkos with CMake on SCOREC (rhel9) machines
---

1. **Clone the Kokkos Repository**: Create a new directory called Kokkos and clone Kokkos repository from GitHUb in that directory. You can do this using Git:
```bash
git clone https://github.com/kokkos/kokkos.git
```
2. **Load required modules**: Kokkos requires  compiler and cmake to build. Load the following modules. (*Note: The modules are as per rhel9 machines. You can't use it on rhel7 machines.*)
```bash
module use /opt/scorec/spack/rhel9/v0201_4/lmod/linux-rhel9-x86_64/Core/
module load gcc/12.3.0-iil3lno mpich/4.1.1-xpoyz4t cuda/12.1.1-zxa4msk
module load cmake/3.20.0
```
 
3. **Configure with CMake**: Create a new file config.sh (you can name anything)  in a source directory. Inside config.sh, add the following CMake instructions:
 ```bash
cmake -S . \
      -B build \
      -DCMAKE_CXX_COMPILER=g++ \
      -DBUILD_SHARED_LIBS=ON \
      -DCMAKE_INSTALL_PREFIX=/lore/<username>/Kokkos/Install \
      -DKokkos_ENABLE_OPENMP=ON  
```

4. **Build and Install**: Run the config.sh file with the command `. config.sh` and go to the `build` directory (`cd build`). Run the command `make install`.

5. **Add in your environment variable**: Add the executable to the `LD_LIBRARY_PATH`environment variable. Use the following command to add to the environment variable.
 ```bash
export LD_LIBRARY_PATH=/lore/<username>/Kokkos/Install/lib64:$LD_LIBRARY_PATH
```
