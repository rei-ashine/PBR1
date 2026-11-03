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

The repository contains input and output files of the tools used in the study.
The only Python files are UCSF Chimera session files
(`data/Chimera/MatchMaker/*/Sessions/*.py`), which can be opened in UCSF Chimera.
There are no standalone analysis scripts.

## Workflow
1. **Sequence search**: BLASTp search for PBR1 (`data/BLAST/`, `data/FASTA/`)
2. **Alignment**: Clustal Omega alignment of PBR1 with the FKS1 chain
   (1,3-beta-glucan synthase component) of PDB 7YUY and 8JZN
   (`data/FASTA/For_ClustalOmega/`, `data/ClustalOmega/`).
   In UCSF Chimera, the FKS1 regions aligned with PBR1 were cut out of the template
   structures (`data/PDB/`) as fragment structures (`data/Chimera/ClustalOmega/`).
3. **Fragment modeling**: Robetta models of the FKS1 fragments
   (`data/Robetta/7yuy/`, `data/Robetta/8jzn/`)
4. **Fragment superposition**: UCSF Chimera MatchMaker superposition of the fragment models
   (`data/Chimera/MatchMaker/Training_data/`)
5. **PBR1 modeling**: Robetta models of PBR1 (407 residues) built from
   - the superposed fragment models (`data/Robetta/PBR1/`)
   - the AlphaFold model AF-P53878-F1 in `data/PDB/AlphaFold/` (`data/Robetta/AF-P53878-F1-model_v4/`)
6. **PBR1 model superposition**: UCSF Chimera MatchMaker.
   The `*_refine_20231225.pdb` files are the starting structures for MolDesk
   (`data/Chimera/MatchMaker/PBR1/`)
7. **Structure preparation and pocket search**: MolDesk
   - Add Hydrogens, Solvate, and Global Minimize: sessions in
     `data/MolDesk/Sessions/PBR1/PBR1_*_refine_20231225/`
   - Find Pocket: sessions in
     `data/MolDesk/Sessions/PBR1/PBR1_*_refine_20231225_GlobalMinimized_FoundPockets/`
   - Resulting structures: `data/MolDesk/PBR1/`
8. **Compound preparation**: FAD, FADH2, FMN, FMNH2, NAD, NADH, NADP, NADPH, and NMN
   (`data/Agents/`, `data/MolDesk/Agents/`)
9. **Docking**: MolDesk
   - Docking sessions: `data/MolDesk/Sessions/PBR1/MD/`. Each folder is named
     `<model>_<compound>_<pocket>`.
   - Resulting complexes: `data/MolDesk/Complex_*/`
10. **Interaction analysis**: PDBsum analysis of the 8JZN-based model with FADH2
    (`data/Chimera/For_PDBsum/`, `data/PDBsum/`)

## Directory Structure
```
data/
├── Agents/          # Compound structures (Original: source data, Chimera: MOL2, old: earlier versions)
├── BLAST/           # BLASTp search strategy
├── Bulletin/        # Data archive for sharing (20240111)
├── Chimera/
│   ├── ClustalOmega/  # FKS1 fragment structures cut out with Clustal Omega alignments in UCSF Chimera
│   ├── For_PDBsum/    # PDB file modified for PDBsum
│   └── MatchMaker/
│       ├── Training_data/  # Superposed FKS1 fragment models and Chimera session files
│       └── PBR1/           # Superposed PBR1 models (MolDesk starting structures) and Chimera session files
├── ClustalOmega/    # Clustal Omega results (Old1, Old2: earlier runs)
├── FASTA/           # Sequences of PBR1, 7YUY, and 8JZN
├── MolDesk/
│   ├── Agents/        # Compounds with corrected 3D structures
│   ├── Complex_7YUY/  # Complexes of the 7YUY-based model and compounds
│   ├── Complex_8JZN/  # Complexes of the 8JZN-based model and compounds
│   ├── Complex_AlphaFold/  # Complexes of the AlphaFold-based model and compounds
│   ├── PBR1/          # Energy-minimized models and pocket search results
│   └── Sessions/PBR1/
│       ├── PBR1_*/    # Structure preparation and pocket search sessions
│       └── MD/        # Docking sessions
├── PDB/             # Template structures (7YUY, 8JZN, AlphaFold model)
├── PDBsum/          # PDBsum reports
└── Robetta/
    ├── 7yuy/, 8jzn/   # FKS1 fragment models (EntireLength: models from the whole template,
    │                  #   Old: earlier PBR1 models from the whole template)
    ├── PBR1/          # PBR1 models built from the superposed fragment models
    └── AF-P53878-F1-model_v4/  # PBR1 model built from the AlphaFold model
```

[NOTE]: Three complexes in `data/MolDesk/Complex_*/` have no matching docking session
in `data/MolDesk/Sessions/PBR1/MD/`: the FAD and NAD complexes of the 7YUY-based model,
and the FAD complex of the AlphaFold-based model.

## Releases
- [v1.0.0](https://github.com/rei-ashine/PBR1/releases/tag/v1.0.0):
  Snapshot of all analysis data as of January 23, 2024

---
## Python Environment (optional)
`environment.yml` defines a conda environment (`pbr1`) with Python 3.9, NumPy, pandas,
SciPy, Matplotlib, seaborn, and Jupyter.
No file in this repository requires it.
It is provided for working with the data in Python or Jupyter Notebook.

Create the environment :
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

Add the virtual environment to the kernel of Jupyter Notebook :
```bash
ipython kernel install --user --name pbr1
```
Confirm that "pbr1" is included in "Available kernels" :
```bash
jupyter kernelspec list
```

## License
This repository is released under the [MIT License](LICENSE).
