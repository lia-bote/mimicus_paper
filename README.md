# Genome dynamics of environmental <i>Vibrio mimicus</i> in cholera-endemic regions of Bangladesh

## Overview

This repository contains analysis scripts for the study 'Genome dynamics of environmental <i>Vibrio mimicus</i> in cholera-endemic regions of Bangladesh'. Sequencing reads from this study are deposited in DOI:10.6084/m9.figshare.32664414 and in BioProject PRJEB116021.

## Repository contents 
`example_command_line_analyses.txt`
> Sample command line scripts for analyses steps in this study. The output files generated with each command are described in the comments accompanying each line of code. Comments are also included with approximate run times for key stages of the analyses.

`codeml.ctl`
> Control file for dN/dS analysis implemented with CODEML.

`mimicus_paper_plotting.Rmd`
> Scripts for downstream data processing and visualisation, performed on RStudio (Rv4.5.0). 

## Software 
The software used, with corresponding versions, are listed below. 

Examples of how these software were installed can be found in the R Notebook also included in this repository. These analyses can be run on a local computer or on a compute cluster, and no non-standard hardware were used. No other custom software was developed for this study. 

### Command line tools:
* unicycler v0.5.0
* fastqc v0.12.1
* multiqc v1.17--pyhdfd78af_1
* kraken2 v2.1.2
* quast v5.0.2-c1
* checkm2 v1.0.1
* gtdbtk v2.3.0
* bakta v1.11.0
* panaroo v1.3.3
* eggnog-mapper v2.1.11
* twilight v1
* snp-sites v2.5.1
* iqtree v2.2.0
* fastBAPS v1.0.6
* BLAST v2.14.0
* abricate v1.0.1
* paml v4.10.9
* hamburger v1

### R packages:
* paletteer v1.7.0
* aplot v0.2.9
* ggnewscale v0.5.2
* ggtreeExtra v1.18.1
* phytools v2.5-2
* maps v3.4.3
* ape v5.8-1
* ggtree v3.16.3
* cowplot v1.2.0
* gggenomes v1.1.3
* lubridate v1.9.5
* forcats v1.0.1
* stringr v1.6.0
* dplyr v1.2.0
* purrr v1.2.1
* readr v2.2.0
* tidyr v1.3.2
* tibble v3.3.1
* ggplot2 v3.5.2
* ggplot2 v4.0.0
* tidyverse v2.0.0 
