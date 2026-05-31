# Bulk RNA-seq: P53 Activation in Acute Myeloid Leukaemia

## Biological question

Acute Myeloid Leukaemia (AML) is driven in part by the suppression of P53, a tumour suppressor that normally prevents cancer cells from replicating. Two therapeutic strategies aim to reactivate P53: MDM2 inhibitors, which block the protein that degrades P53, and BET inhibitors, which reduce expression of genes that suppress P53 activity.

This analysis asks: what genes and pathways are affected by each drug individually, and does the combination of both treatments produce a transcriptional response that is distinct from either drug alone?

---

## Data

- **Source:** Public dataset (GEO)
- **Sample type:** AML stem cells from patient samples
- **Experimental groups:** 4 groups
  - Untreated (DMSO control)
  - MDM2 inhibitor treated
  - BET inhibitor treated
  - MDM2 + BET inhibitor combination treated
- **Comparisons:** 3 differential expression tables
  - MDM2 inhibitor vs untreated
  - BET inhibitor vs untreated
  - Combination vs untreated

---

## Analysis overview

1. Quality control and normalisation of raw count data
2. Differential expression analysis using DESeq2
3. Multi-group differential expression (MDE) analysis across all four groups
4. Pathway enrichment analysis using clusterProfiler
5. K-means clustering to identify transcriptional signatures
6. Visualisation including volcano plots, heatmaps, Euler diagrams, and chromosomal distribution plots

---

## Repository structure

```
Bulk-RNA-seq-Acute-Myeloid-Leukemia/
├── Bulk_RNAseq_AML.R          # Main analysis pipeline
├── BETI_DMSO_AML.R            # BET inhibitor vs untreated comparison
├── MDM2I_DMSO_AML.R           # MDM2 inhibitor vs untreated comparison
├── COMBO_DMSO.R               # Combination treatment vs untreated comparison
├── MDE_analysis.R             # Multi-group differential expression analysis
└── My DE functions.R          # Reusable custom functions for DE analysis
```

---

## Key tools and packages

- **R** with Bioconductor
- DESeq2 for differential expression
- clusterProfiler for pathway enrichment
- ggplot2 for visualisation

---

## Results

![Figure 1. RNA-seq analysis of treatment conditions compared to DMSO controls. (A) PCA of normalized expression data coloured by treatment group. (B) Density plots of log10-transformed expression values across all 12 samples. (C) Sample correlation heatmap showing pairwise Spearman correlation coefficients. (D-F) Volcano plots for each treatment comparison with top differentially expressed genes labelled. (G-I) Heatmaps of scaled expression values for significant genes in each comparison.](images/image.png)

---

## Key findings

**MDM2 inhibition alone produced a limited but targeted transcriptional response**, with only 21 differentially expressed genes. Despite the small number, apoptotic signalling pathways were significantly enriched and key P53 target genes including CDKN1A and BAX were upregulated, suggesting partial P53 reactivation. The limited response likely reflects a known resistance mechanism in AML stem cells.

**BET inhibition drove widespread transcriptional remodelling**, with over 1,200 differentially expressed genes distributed across all chromosomes. Downregulated genes were enriched for DNA replication and RNA processing pathways, consistent with suppression of MYC-driven proliferative programmes. Notable downregulated genes included CTSG, TUBA1B and LYZ.

**The combination treatment produced the largest and most distinct transcriptional response**, with over 1,400 differentially expressed genes and the strongest upregulation of P53 target genes including CDKN1A, BAX, BBC3, PMAIP1 and NOXA. An Euler diagram showed that the combination shared 1,010 differentially expressed genes with BETi but only 11 with MDM2i, identifying BET inhibition as the dominant driver of the combination effect.

**K-means clustering identified three transcriptional signatures:**
- Signature 1: genes with stable expression across all conditions
- Signature 2: genes activated by BETi and combination, enriched for autophagy pathways
- Signature 3: genes suppressed by BETi and combination, enriched for DNA replication and ribosome biogenesis, consistent with suppression of AML stem cell self-renewal

These findings support combination BETi and MDM2i as a therapeutic strategy in AML, providing a transcriptional framework for understanding the synergy between the two drug classes.

---

## Notes

This dataset involves 4 experimental groups and 3 differential expression comparisons, making it a more complex multi-group RNA-seq analysis than a standard two-group design. The custom functions in `My DE functions.R` were written to handle this structure efficiently and are reusable across similar multi-group datasets.
