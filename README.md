# DEPM Project

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![R Markdown](https://img.shields.io/badge/Built%20with-R%20Markdown-276DC3)](Project.Rmd)
[![Cancer Type](https://img.shields.io/badge/TCGA-KIRP-blue)](Project.Rmd)

A bioinformatics project that analyzes **Kidney Renal Papillary Cell Carcinoma (KIRP)** using TCGA data. The workflow combines differential expression, gene co-expression analysis, differential network analysis, patient similarity networks, and similarity network fusion to study tumor biology and patient stratification.

## Overview

This repository contains an end-to-end **R Markdown** analysis centered on TCGA-KIRP RNA-seq and mutation data. The main workflow is implemented in `Project.Rmd` and can render to both **HTML** and **PDF** outputs.

The analysis covers:
- Differentially expressed genes (DEGs) between tumor and normal samples
- Cancer and normal gene co-expression networks
- Differential co-expression network analysis
- Patient similarity networks (PSN)
- Similarity Network Fusion (SNF) using expression and mutation data
- Optional enrichment analysis and survival/community characterization

## Why this project is useful

- Provides a reproducible, notebook-style workflow for a precision medicine case study
- Demonstrates how to use TCGA/GDC data programmatically from R
- Combines transcriptomic, mutational, network, and clustering analyses in one place
- Produces publication-style visualizations for biological interpretation
- Useful as both a research reference and a learning resource for biomedical data analysis

## Repository structure

- `Project.Rmd` — main analysis workflow and source of truth for the project
- `Presentation.pdf` — presentation slides summarizing the project
- `Report.pdf` — rendered report/documentation for the analysis
- `images/` — project figures and supporting images used by the report
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

## Example workflow

A typical workflow for a developer or researcher is:

1. Install the required R and Bioconductor packages
2. Render `Project.Rmd`
3. Review the DEG results and volcano plot
4. Inspect co-expression and differential network outputs
5. Explore PSN/SNF community assignments and downstream biological interpretation

## Outputs

Depending on which sections you run, the project can produce:
- Rendered HTML/PDF reports from `Project.Rmd`
- DEG tables and volcano plots
- Co-expression and differential network statistics
- PSN and SNF community plots
- Enrichment visualizations and pathway figures

The repository already includes `Report.pdf` and `Presentation.pdf` as reference outputs.

## Help and support

If you need help getting started:
- Read the workflow source in `Project.Rmd`
- Review the generated project report in `Report.pdf`
- Check the presentation overview in `Presentation.pdf`
- Consult package documentation for `TCGAbiolinks`, `DESeq2`, and `SNFtool`

Because this repository does not currently expose GitHub Issues, the best support path is to contact the maintainer through the repository owner profile.

## Contributing

Contributions are welcome.

Suggested process:
1. Fork the repository
2. Create a feature branch
3. Make focused, well-documented changes
4. Re-render outputs if your changes affect analysis results or figures
5. Open a pull request with a clear summary of what changed and why

When contributing, prefer:
- small, reviewable commits
- clear explanations for analytical choices
- reproducible code and explicit package requirements
- preserving generated outputs only when they are intentionally updated

If a dedicated `CONTRIBUTING.md` file is added later, prefer that document for detailed contribution guidance.

## Maintainers and authors

This project is maintained in this fork by **@azzadom**.

The R Markdown subtitle credits the project authors as:
- Domenico Azzarito
- Federico Lattanzio
- Michele Pezza

This repository is a fork of `michelepezza99/Precision-Medicine-Project---TCGA-KIRP-cancer`.

## License

This project is licensed under the **MIT License**. See `LICENSE` for details.
