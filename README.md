# Single-Cell Transcriptomic Profiling of Tissue-Specific Senescence

**Author:** Jungjin Kim  
**Institution:** Denison University  

## Overview
This repository contains an independent "dry lab" computational biology pipeline designed to isolate and identify the molecular signatures of aging in specific murine tissues. 

The primary objective of this project is to process raw single-cell RNA sequencing (scRNA-seq) data to identify novel transcriptional targets associated with the **Senescence-Associated Secretory Phenotype (SASP)**, providing data-driven candidates for potential CRISPR interference (CRISPRi) or senolytic therapies.

## Datasets
* **Source:** Tabula Muris Senis (The Murine Single-Cell Aging Atlas)
* **Tissue Analyzed:** Bladder (Urothelial Cells)
* **Cohorts:** 3-month (Young) vs. 24-month (Old)

## Methodology & Computational Pipeline
The analysis is executed in Python using a custom bioinformatics workflow:
1. **Data Ingestion & QC:** Raw `.h5ad` matrices are loaded and filtered.
2. **Dimensionality Reduction:** Data is normalized (`target_sum=1e4`), log-transformed, and visualized using UMAP to track the physical divergence of cellular transcriptomes across lifespans.
3. **Differential Gene Expression (DGE):** Wilcoxon rank-sum testing isolates statistically significant upregulated genes driving the aging phenotype.
4. **Pathway Enrichment Analysis:** The `gseapy` library cross-references DGE outputs with the Gene Ontology (GO) Biological Process database to map systemic cellular breakdown.

## Key Findings (Bladder Urothelial Aging)
The pipeline successfully isolated known master-regulators of cellular senescence from the raw transcriptomic data, with high statistical significance:
* **AP-1 Complex Activation:** Dramatic upregulation of `Jund` ($p < 10^{-98}$), a primary transcription factor responsible for driving SASP inflammatory cytokine production (e.g., IL-6).
* **LncRNA Dysregulation:** Significant spikes in `Malat1`, an RNA scaffold associated with oxidative stress and senescence.
* **Ribosomal Hyperactivation:** Pathway enrichment confirmed a massive upregulation in **Ribosomal Small Subunit Biogenesis** and **Cytoplasmic Translation**, perfectly mirroring the cellular hypertrophy and hyper-secretion characteristic of the SASP.

## Tech Stack
* `Python 3.10`
* `Scanpy` (Single-cell processing toolkit)
* `AnnData` (Genomic data structures)
* `GSEApy` (Pathway enrichment)
* `Pandas` & `Matplotlib`
