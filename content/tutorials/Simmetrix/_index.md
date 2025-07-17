---
title: Simmetrix
description: "Simmetrix related workflow and tools"
weight: 1
---

## simmetrixModel2Parasolid
[simmetrixModel2Parasolid](https://github.com/LACES-LAB/simmetrixModel2Parasolid) is tool to convert native Simmetrix models (.smd files) to Parasolid (.x_t files). It uses the Simmetrix Parasolid interface. To use on SCOREC rhel9 machines, load the modules:

```bash
module use /opt/scorec/spack/rhel9/v0201_4/lmod/linux-rhel9-x86_64/Core/
module load gcc/12.3.0-iil3lno mpich/4.1.1-xpoyz4t cuda/12.1.1-zxa4msk
module load module load simmetrix-simmodsuite/2025.0-241016dev-vafjs2q
```
and then run the tool:
```bash
 /lore/hasanm4/wsources/simModel2parasolid/build/simModel2parasolid simModelName.smd parasolidName.x_t
```