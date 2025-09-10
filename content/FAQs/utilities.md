---
title: Preinstalled Utilities
description: Different utilities are already installed on SCOREC systems for convenience.
weight: 1
---
{{% alert title="May be outdated" %}}
This document can be outdated and may not reflect the current state of the system. Please contact if needed.
{{% /alert %}}

# `htop`
`htop` is an interactive process viewer for Unix systems. Some may need it due to its advanced mouse support, visual indicators, and other features over the traditional `top` command. It can be found in 
```bash
/users/hasanm4/lore.scorec.rpi.edu/sourcestoInstall/htop/install/bin/htop
```
The following can be added to `.bashrc` for easier access:
```bash
alias htop='LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/scorec/spack/rhel9/v0201_4/install/linux-rhel9-x86_64/gcc-12.3.0/ncurses-6.4-m4ky27paykdimx3aboabuqsdf52dpxhm/lib /users/hasanm4/lore.scorec.rpi.edu/sourcestoInstall/htop/install/bin/htop'
```

