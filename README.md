#Genome dynamics of environmental <i>Vibrio mimicus</i> in cholera-endemic regions of Bangladesh

##Overview

This repository contains analysis scripts for the study 'Genome dynamics of environmental <i>Vibrio mimicus</i> in cholera-endemic regions of Bangladesh'. Sequencing reads from this study corresponding to these examples are found in DOI:10.6084/m9.figshare.32664414 and in BioProject PRJEB116021.


The output files/directories generated with each command, highlighting expected output, and described in the comments accompanying each line of code. Comments are also included with approximate run times for key stages of the analyses.

The software used, with corresponding versions, are listed below. Examples of how these software were installed can be found in the R Notebook also included in this repository. These analyses can be run on a local computer or on a compute cluster, and no non-standard hardware were used. No other custom software was developed for this study. 

Downstream data processing and visualisation was performed on RStudio (Rv4.5.0) as detailed in the RMarkdown file also included in this repository. 

Command line tools used were:

unicycler_0.5.0
fastqc_0.12.1
multiqc_1.17--pyhdfd78af_1
kraken2_2.1.2
quast_5.0.2-c1
checkm2_1.0.1
gtdbtk_2.3.0
bakta_1.11.0
panaroo_1.3.3
eggnog-mapper_2.1.11
twilight_1
snp-sites_2.5.1
iqtree_2.2.0
fastBAPS_1.0.6
BLAST_2.14.0
abricate_1.0.1
paml_4.10.9
hamburger_1

R packages used were:
aletteer_1.7.0
aplot_0.2.9
ggnewscale_0.5.2
ggtreeExtra_1.18.1
phytools_2.5-2
maps_3.4.3
ape_5.8-1
ggtree_3.16.3
cowplot_1.2.0
gggenomes_1.1.3
lubridate_1.9.5
forcats_1.0.1
stringr_1.6.0
dplyr_1.2.0
purrr_1.2.1
readr_2.2.0
tidyr_1.3.2
tibble_3.3.1
ggplot2_3.5.2
ggplot2_4.0.0
tidyverse_2.0.0 


#### codeml ctl file for running PAML to estimate dN/dS
`seqfile = clustalw_nuc_aln.fasta            * Path to the alignment file
     treefile = tcpA_codon_rename_no_len.tree           * Path to the tree file
      outfile = out_sites.txt            * Path to the output file
        noisy = 3              * How much rubbish on the screen
      verbose = 1              * More or less detailed report
      seqtype = 1              * Data type
        ndata = 1           * Number of data sets or loci
        icode = 0              * Genetic code 
    cleandata = 0              * Remove sites with ambiguity data?               
        model = 0         * Models for ω varying across lineages
          NSsites = 0 1 2 7 8        * Models for ω varying across sites
    CodonFreq = 7        * Codon frequencies
          estFreq = 0        * Use observed freqs or estimate freqs by ML
        clock = 0          * Clock model
    fix_omega = 0         * Estimate or fix omega
        omega = 0.5        * Initial or fixed omega`
