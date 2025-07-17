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

## Convert Parasolid to Simmetrix
To convert Parasolid files (`.x_t`, which can be also exported from NX parts) to Simmetrix models (`.smd`):

1. Load the required modules:
```bash
module use /opt/scorec/spack/rhel9/v0201_4/lmod/linux-rhel9-x86_64/Core/
module load module load simmetrix-simmodsuite/2025.0-241016dev-vafjs2q
module load pumi/develop-simmodsuite-2025.1-250507dev-int32-shared-g2attww
module load simmetrix/simModeler
```
2. Open `simmodeler` GUI and import the Parasolid file. Go to `Prepare` tab and select `Create Model` or `Make Model` or `Create Nonmanifold Model` depending on the version. Make sure to select `Nonmanifold`. Now, save the model as `.smd` file. This will create a new Parasolid file `model-nat.x_t` in the same directory.
3. To use this model in simmetrix tools, it needs to be translated to a Simmetrix native model. For that, run the following command:
```bash
simTranslate model-nat.x_t model.smd model-translated.smd
```
and use the `model-translated.smd` file in the simmetrix tools.