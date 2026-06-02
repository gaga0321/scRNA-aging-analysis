# Tissue-Specific Senescence: Single-Cell Transcriptomic Pipeline

**Author:** Jungjin Kim  
**Institution:** Denison University  

This is a dry-lab computational biology pipeline built to isolate and map the molecular signatures of aging in specific mouse tissues. The core focus is processing raw single-cell RNA sequencing (scRNA-seq) data to pinpoint novel transcriptional targets linked to the **Senescence-Associated Secretory Phenotype (SASP)**—ultimately flagging data-driven candidates for CRISPRi or senolytic therapeutic research.

## The Data
* **Source:** Tabula Muris Senis (The Murine Single-Cell Aging Atlas)
* **Tissue Focus:** Bladder (Urothelial Cells)
* **Cohorts:** 3-month (Young) vs. 24-month (Old)

## Pipeline Architecture
I structured the analysis as a modular Python workflow rather than relying on black-box tools, ensuring full control over the filtering and normalization steps:

1. **QC & Data Ingestion:** Loading raw `.h5ad` matrices, filtering out low-quality cells, and establishing baseline thresholds.
2. **Normalization & Dimensionality Reduction:** Scaling count matrices (`target_sum=1e4`), log-transforming, and generating UMAP embeddings to track how cell transcriptomes physically diverge across the lifespan.
3. **Differential Gene Expression (DGE):** Utilizing Wilcoxon rank-sum testing to pull out statistically significant genes driving the aging phenotype.
4. **Pathway Enrichment Analysis:** Feeding DGE outputs into `gseapy` to cross-reference hits with the Gene Ontology (GO) Biological Process database, mapping out systemic cellular degradation.

## Key Insights (Bladder Urothelial Aging)
The pipeline successfully isolated several known master-regulators of cellular senescence directly from the raw transcriptomic data, validating the workflow's sensitivity:

* **AP-1 Complex Activation:** Observed a sharp upregulation of `Jund` (p < 1e-98), a major transcription factor responsible for driving inflammatory SASP cytokines like IL-6.
* **LncRNA Dysregulation:** Caught significant spikes in `Malat1` within the old cohort, linking the dataset directly to oxidative stress and structural aging pathways.
* **Ribosomal Hyperactivation:** Pathway enrichment flagged a massive increase in **Ribosomal Small Subunit Biogenesis** and **Cytoplasmic Translation**. This perfectly captures the cellular hypertrophy and hyper-secretion that defines the SASP profile.

## Tech Stack
* **Language:** Python 3.10
* **Core Single-Cell Analysis:** `Scanpy`, `AnnData`
* **Functional Annotation:** `GSEApy`
* **Data & Plotting:** `Pandas`, `Matplotlib`
