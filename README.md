# PBR1
Author: rei-ashine<br>
DATE: Dec. 21st, 2023 (last updated: Nov. 2nd, 2026)<br>

---
## Overview
This repository contains the data from an in silico study of PBR1
(NCBI RefSeq NP_014218.2, UniProt P53878), a putative oxidoreductase
of *Saccharomyces cerevisiae*.
The structure of PBR1 was modeled, and flavin and nicotinamide cofactors
were docked into the predicted pockets.

The repository contains data files only. It does not contain analysis scripts.

## Workflow
1. **Sequence search**: BLASTp search for PBR1 (`data/BLAST/`, `data/FASTA/`)
2. **Alignment**: Clustal Omega alignment of PBR1 with 1,3-beta-glucan synthase component FKS1
   (PDB 7YUY and 8JZN) (`data/ClustalOmega/`, `data/Chimera/ClustalOmega/`)
3. **Modeling**: Robetta models of PBR1 built using 7YUY, 8JZN, and the AlphaFold model
   (AF-P53878-F1) as references (`data/PDB/`, `data/Robetta/`)
4. **Superposition**: UCSF Chimera MatchMaker (`data/Chimera/MatchMaker/`)
5. **Energy minimization and pocket search**: MolDesk (`data/MolDesk/PBR1/`)
6. **Compound preparation**: FAD, FADH2, FMN, FMNH2, NAD, NADH, NADP, NADPH, and NMN
   (`data/Agents/`, `data/MolDesk/Agents/`)
7. **Docking**: MolDesk (`data/MolDesk/Complex_*/`, `data/MolDesk/Sessions/`)
8. **Interaction analysis**: PDBsum (`data/Chimera/For_PDBsum/`, `data/PDBsum/`)

## Directory Structure
```
data/
├── Agents/          # Compound structures (Original: source data, Chimera: MOL2, old: earlier versions)
├── BLAST/           # BLASTp search strategy
├── Bulletin/        # Data archive for sharing (20240111)
├── Chimera/
│   ├── ClustalOmega/  # Clustal Omega results run on UCSF Chimera
│   ├── For_PDBsum/    # PDB file modified for PDBsum
│   └── MatchMaker/    # Superposed models and Chimera session files
├── ClustalOmega/    # Clustal Omega results (Old1, Old2: earlier runs)
├── FASTA/           # Sequences of PBR1, 7YUY, and 8JZN
├── MolDesk/
│   ├── Agents/        # Compounds with corrected 3D structures
│   ├── Complex_7YUY/  # Complexes of the 7YUY-based model and compounds
│   ├── Complex_8JZN/  # Complexes of the 8JZN-based model and compounds
│   ├── Complex_AlphaFold/  # Complexes of the AlphaFold-based model and compounds
│   ├── PBR1/          # Energy-minimized models and pocket search results
│   └── Sessions/      # MolDesk session files (calculation preparation and docking)
├── PDB/             # Template structures (7YUY, 8JZN, AlphaFold model)
├── PDBsum/          # PDBsum reports
└── Robetta/         # Robetta modeling results
```

[NOTE]: The docking calculations under `data/MolDesk/Sessions/PBR1/MD/` were run
to check the simulation setup. They are not final results.

## Releases
- [v1.0.0](https://github.com/rei-ashine/PBR1/releases/tag/v1.0.0):
  Snapshot of all analysis data as of January 23, 2024

---
## Installing Dependencies
All dependencies can be installed with conda.<br>
An environment screenshot is provided :
```bash
conda env create -f environment.yml
```
Once the environment is created,<br>
it can be used at any time (without having to download everything again) :
```bash
conda activate pbr1
```
Exit the running virtual environment :
```bash
conda deactivate
```
Delete the virtual environment :
```bash
conda remove -n pbr1 --all
```

## Setting up Jupyter Notebook
Add a virtual environment to the kernel of Jupyter Notebook :
```bash
ipython kernel install --user --name pbr1
```
Confirm that "pbr1" is included in "Available kernels" :
```bash
jupyter kernelspec list
```

## License
This repository is released under the [MIT License](LICENSE).
