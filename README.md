# DEPM Project

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![R Markdown](https://img.shields.io/badge/Built%20with-R%20Markdown-276DC3)](Project.Rmd)
[![Cancer Type](https://img.shields.io/badge/TCGA-KIRP-blue)](Project.Rmd)

A university bioinformatics project focused on **Kidney Renal Papillary Cell Carcinoma (KIRP)** using TCGA data. The workflow combines differential expression, gene co-expression analysis, differential network analysis, patient similarity networks, and similarity network fusion to study tumor biology and patient stratification.

## Overview

This repository contains an end-to-end **R Markdown** analysis centered on TCGA-KIRP RNA-seq and mutation data. The main workflow is implemented in `Project.Rmd` and can render to both **HTML** and **PDF** outputs.

The analysis covers:
- Differentially expressed genes (DEGs) between tumor and normal samples
- Cancer and normal gene co-expression networks
- Differential co-expression network analysis
- Patient similarity networks (PSN)
- Similarity Network Fusion (SNF) using expression and mutation data
- Optional enrichment analysis and survival/community characterization

## Repository structure

- `Project.Rmd` — main analysis workflow and source of truth for the project
- `Presentation.pdf` — presentation slides summarizing the project
- `Report.pdf` — the official paper written from the project results
- `LICENSE` — MIT license

## What the workflow does

The R Markdown document defines the project in five major stages:

1. **Data acquisition and preprocessing**  
   Downloads TCGA-KIRP RNA-seq tumor and normal samples from GDC using `TCGAbiolinks`, prepares `SummarizedExperiment` objects, aligns paired patients, filters genes, and normalizes counts with `DESeq2`.

2. **Differential expression analysis**  
   Computes log2 fold changes, paired statistical tests, FDR correction, and generates a volcano plot to identify significant DEGs.

3. **Network analysis**  
   Builds cancer and normal co-expression networks, studies degree distributions, identifies hubs, compares hub centrality, and constructs a differential co-expression network.

4. **Patient similarity analysis**  
   Builds a PSN from tumor expression data, detects communities, and compares tumor and normal patient similarity structure.

5. **Multi-omics integration**  
   Downloads mutation data, builds mutation matrices, fuses expression and mutation similarities using `SNFtool`, and studies patient communities in the fused network.

Optional sections extend the analysis with:
- GO and KEGG enrichment analysis
- Pathway visualization
- Tumor-only community characterization
- Survival analysis by SNF community

## Getting started

### Prerequisites

You will need:
- **R** (recommended recent version)
- **RStudio** or another environment that can render R Markdown
- A LaTeX installation if you want to render PDF output (`xelatex` is configured in `Project.Rmd`)
- Internet access to download TCGA/GDC datasets

### Required R packages

The workflow loads the following packages directly in `Project.Rmd`:

```r
library(BiocGenerics)
library(DESeq2)
library(psych)
library(NetworkToolbox)
library(ggplot2)
library(GGally)
library(sna)
library(network)
library(TCGAbiolinks)
library(GenomicRanges)
library(SummarizedExperiment)
library(DT)
library(igraph)
library(maftools)
library(cowplot)
library(SNFtool)
library(reshape2)
library(poweRlaw)
library(dplyr)
library(ggraph)
```

Optional sections additionally use:

```r
library(clusterProfiler)
library(org.Hs.eg.db)
library(enrichplot)
library(pathview)
library(stringr)
library(survival)
library(survminer)
library(tidyr)
library(limma)
```

### Installation

Clone the repository:

```bash
git clone https://github.com/azzadom/DEPM-Project.git
cd DEPM-Project
```

Install CRAN packages:

```r
install.packages(c(
  "psych", "NetworkToolbox", "ggplot2", "GGally", "sna", "network",
  "DT", "igraph", "maftools", "cowplot", "SNFtool", "reshape2",
  "poweRlaw", "dplyr", "ggraph", "clusterProfiler", "enrichplot",
  "pathview", "stringr", "survival", "survminer", "tidyr", "limma"
))
```

Install Bioconductor dependencies:

```r
if (!requireNamespace("BiocManager", quietly = TRUE)) {
  install.packages("BiocManager")
}

BiocManager::install(c(
  "BiocGenerics", "DESeq2", "TCGAbiolinks", "GenomicRanges",
  "SummarizedExperiment", "org.Hs.eg.db"
))
```

### Run the analysis

Render the main notebook:

```r
rmarkdown::render("Project.Rmd", output_format = "html_document")
rmarkdown::render("Project.Rmd", output_format = "pdf_document")
```

Or open `Project.Rmd` in RStudio and use **Knit**.

### Usage notes

- The workflow downloads data from the Genomic Data Commons into a local `GDCdata` directory.
- Some sections are computationally intensive and may take a long time to run.
- Several chunks are written as analysis notes, so you may want to execute the notebook section by section the first time.
- PDF rendering requires a working LaTeX engine compatible with `xelatex`.

## Contributing

This repository primarily archives a **university project** and its final materials. Contributions are therefore expected to be limited, but improvements to documentation, reproducibility, or clarity are still welcome.

## Maintainers and authors

This repository preserves a university project authored by:
- **Domenico Azzarito**
- **Federico Lattanzio**
- **Michele Pezza**

The repository is maintained on GitHub by **@azzadom**.

## License

This project is licensed under the **MIT License**. See `LICENSE` for details.
