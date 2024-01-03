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
