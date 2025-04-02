---
title: Tools
description: "Tools used in LACES projects"
weight: 1
---

# CPU Memory Usage Tracking tools
## `heaptrack`
It provides efficient, time resolved memory usage, leaks, allocations, flamegraphs, etc. for large applications - *even with release compilation*. It has a nice gui which opens automatically (if the AppImage is used, otherwise install and run `heaptrack_gui`) when there's display connected. `heaptrack_gui` is also available on ubuntu apt repository and be installed easily by doing (may need sudo):
```bash
apt install heaptrack_gui
```

 Portable version can be found here in [KDE Download Page](https://download.kde.org/Attic/heaptrack/1.5.0/). This AppImage worked on both Ubuntu 24.04LTE and **Perlmutter**. Find more details here: https://milianw.de/blog/heaptrack-a-heap-memory-profiler-for-linux.html

 Another advantage is that even if the application crashes, it stills saves the data upto that point.

## `valgrind --tool=massif`
Well known tool for memory profiling. It takes long time for large applications since it slows down the application significantly. Official documentation can be found here: https://valgrind.org/docs/manual/ms-manual.html. It also has a GUI called `massif-visualizer`.

## Linaro-MAP
Generic profiling tool. Find more details here: https://www.linaroforge.com/linaro-map/. Tried to use it for a large application, but it needs debug symbols as well as *gets stuck at some point and produces no output*.

## `gperftools` / `pprof`
I didn't use it but listing as an available option.

# GPU or General Kokkos Memory Usage Tracking tools

Kokkos provides a set of tools to track memory usage. Find details [here](https://github.com/kokkos/kokkos-tools/wiki/MemoryHighWater#:~:text=KernelSampler-,Memory%20Analysis,-MemoryHighWater). Don't forget to compile `Kokkos` with `Kokkos_ENABLE_LIBDL=ON` flag before using these tools.

# Performance Profiling tools
## HPCToolkit
Find details and usage here: https://hpctoolkit.org/. It is available in perlmutter through:
```bash
module load spack
spack env activate gcc
spack load hpctoolkit
```

## TAU
[TAU](https://www.cs.uoregon.edu/research/tau/home.php) is also avaiable in perlmutter through the gcc spack environemt. It has higher overhead and I don't have much experience with it.

## Linaro-Forge
[Available in perlmutter](https://docs.nersc.gov/tools/performance/performancereports/#loading-the-forge-module). Find details here: https://www.linaroforge.com/. Has a nice GUI. I never used it but listing as an option.


# Remote GUI Connection
## NERSC/Perlmutter Machines
- Through [ThinLinc](https://docs.nersc.gov/connect/thinlinc/). It also works with their `sshproxy` allowing to connect without password.

## SCOREC Machines
- Though Web Interface of Blue and Orange Portals.
- Through aperture machines. See instructions [here](https://laces-lab.github.io/documentation/faqs/connec_aperture/).