# Tissue-Specific Senescence: Single-Cell Transcriptomic Analysis

**Author:** Jungjin Kim  
**Institution:** Denison University  

This project aims to identify the molecular signatures of aging in Bladder Urotherlial Cells in mice. Raw single-cell RNA sequencing data was processed to find transcriptional targets linked to the Senescence-Associated Secretory Phenotype (SASP). Ultimately, this identifies ideal candidates for therapeutic research such as CRISPRi.

## The Data
* **Source:** Tabula Muris Senis (The Murine Single-Cell Aging Atlas)
* **Tissue Focus:** Bladder Urothelial Cells
* **Cohorts:** 3-month (Young) vs. 24-month (Old)

## Implementation
1. **Data Ingestion:** Loading raw `.h5ad` matrices, filtering out low-quality cells, and establishing baseline thresholds.
2. **Normalization:** Scaling count matrices (`target_sum=1e4`), log-transforming, and generating UMAP embeddings to track how cell transcriptomes physically diverge across the lifespan.
3. **Differential Gene Expression (DGE):** Utilizing Wilcoxon rank-sum testing to pull out statistically significant genes driving the aging phenotype.
4. **Pathway Enrichment Analysis:** Feeding DGE outputs into `gseapy` to cross-reference hits with the Gene Ontology (GO) Biological Process database, mapping out systemic cellular degradation.

## Key Insights
The analysis isolated several known master-regulators of cellular senescence:

* **AP-1 Complex Activation:** Observed a sharp upregulation of `Jund` (p < 1e-98), a major transcription factor responsible for driving inflammatory SASP cytokines like IL-6.
* **LncRNA Dysregulation:** Caught significant spikes in `Malat1` within the old cohort, linking the dataset directly to oxidative stress and structural aging pathways.
* **Ribosomal Hyperactivation:** Pathway enrichment found a massive increase in **Ribosomal Small Subunit Biogenesis** and **Cytoplasmic Translation**.

## Tech Stack
* **Language:** Python 3.10
* **Single-Cell Analysis:** `Scanpy`, `AnnData`
* **Functional Annotation:** `GSEApy`
* **Data & Plotting:** `Pandas`, `Matplotlib`
