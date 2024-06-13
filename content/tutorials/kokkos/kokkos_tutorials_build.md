---
title: Building kokkos-tutorials 
---
The following instructions is for building a new Kokkos library for each exercise. For more details, check [Kokkos Tutorials](https://github.com/kokkos/kokkos-tutorials).

1. **Clone the Kokkos Tutorials Repository**: The tutorials for the Kokkos C++ programming. You can clone the tutorials with the following command.
```bash
git clone https://github.com/kokkos/kokkos-tutorials.git
```
2. **Load required modules**: Kokkos tutorials requires  compiler and make to build. Load the following modules. (*Note: The modules are as per rhel9 machines. You can't use it on rhel7 machines.*)
```bash
module use /opt/scorec/spack/rhel9/v0201_4/lmod/linux-rhel9-x86_64/Core/
module load gcc/12.3.0-iil3lno mpich/4.1.1-xpoyz4t cuda/12.1.1-zxa4msk
```
3. **Find the GPU architecture of your machine**: To find out the GPU architecture of your machine, [follow this](https://laces-lab.github.io/documentation/faqs/find_gpu_arc/).

4. **Build with make**: Inside kokkos-tutorials folder, go to `Exercises` folder.In each exercise folder, there is a makefile to build each exercise. Open the Makefile and make the following changes.
```bash
KOKKOS_PATH = /path/to/kokkos 
KOKKOS_DEVICES = "<your GPU language>"
KOKKOS_ARCH = "<your GPU Architecture>"
```
For example,
 ```bash
KOKKOS_PATH = /lore/<username>/Kokkos/kokkos`
KOKKOS_DEVICES = "Cuda"
KOKKOS_ARCH = "Ada89"
```
After making changes, run the command `make -j8`

5. **Run the executable**: Once configuring and building the exercise, run an exexutable. ```bash
./<executable>
 ``` 
