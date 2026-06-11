# HIPC scRNA-seq Annotation Benchmark Challenge — Team 11

Fred Hutchinson Cancer Center

## Overview

This repository contains the cell type annotation pipeline and submission files for the HIPC scRNA-seq Annotation Benchmark Challenge. We annotated 8 assigned studies across infection and vaccination cohorts using an automated pipeline based on CellTypist with manual validation.
```
## Repository Structure


├── HIPC_annotation_pipeline.ipynb   # Full reproducible pipeline
├── Annotations/                     # Per-study annotation TSVs
├── HIPC_cell_markers.xlsx           # Marker genes used for validation
├── Validation_marker_genes.pdf      # Marker gene plots
└── README.md
```

## Studies Annotated

| Study | Cohort | Cells | Notes |
|---|---|---|---|
| infection_study_01 | Infection | 59,446 | COVID/Flu/healthy PBMCs |
| infection_study_02 | Infection | 54,797 | 3 infection arms |
| infection_study_06 | Infection | 835,861 | Whole blood; Ensembl ID conversion |
| vaccination_study_01 | Vaccination | 297,000 | 1 vaccine arm |
| vaccination_study_02 | Vaccination | 102,000 | 3 vaccine arms |
| vaccination_study_03 | Vaccination | 10,043 | Loaded from MTX; myeloid-enriched |
| vaccination_study_07 | Vaccination | 54,000 | Pre-filtered upstream |
| vaccination_study_09 | Vaccination | 140,000 | CITE-seq; RNA only |

## Pipeline Summary

1. QC filtering (200–6,000 genes, total counts <50k, MT <15%)
2. Normalization (10,000 counts/cell, log1p)
3. HVG selection (top 2,000, batch_key=study_id)
4. PCA (50 components)
5. Harmony batch correction (study_id)
6. Leiden clustering (resolution=0.3)
7. Doublet detection (Scrublet)
8. CellTypist annotation (Immune_All_Low.pkl, majority_voting=True)
9. Label mapping to challenge ontology
10. Manual cluster fixes based on marker gene validation

## Software

Python 3.11.3, scanpy 1.9.8, celltypist, harmonypy, scrublet, mygene, anndata

## Notes

File paths in the notebook are specific to the Fred Hutch HPC cluster and will need to be updated for local execution.
```
