Code and analysis for Genome dynamics of <i>Vibrio mimicus</i> in cholera-endemic regions of Bangladesh

This document describes the command-line analyses performed as part of this study, with example code for each stage showing which flags were used. Sequencing reads from this study corresponding to these examples are found in DOI:10.6084/m9.figshare.32664414. The output files/directories generated with each command, highlighting expected output, and described in the comments accompanying each line of code. Comments are also included with approximate run times for key stages of the analyses.\
\
The software used, with corresponding versions, are listed below. Examples of how these software were installed can be found in the R Notebook also included in this repository. These analyses can be run on a local computer or on a compute cluster, and no non-standard hardware were used. No other custom software was developed for this study. \
\
Downstream data processing and visualisation was performed on RStudio (Rv4.5.0) as detailed in the RMarkdown file also included in this repository. 

Command line tools used were:

unicycler_0.5.0\
fastqc_0.12.1\
multiqc_1.17--pyhdfd78af_1\
kraken2_2.1.2\
quast_5.0.2-c1\
checkm2_1.0.1\
gtdbtk_2.3.0\
bakta_1.11.0\
panaroo_1.3.3\
eggnog-mapper_2.1.11\
twilight_1\
snp-sites_2.5.1\
iqtree_2.2.0\
fastBAPS_1.0.6\
BLAST_2.14.0\
abricate_1.0.1\
paml_4.10.9\
hamburger_1\
\
R packages used were:\
aletteer_1.7.0\
aplot_0.2.9\
ggnewscale_0.5.2\
ggtreeExtra_1.18.1\
phytools_2.5-2\
maps_3.4.3\
ape_5.8-1\
ggtree_3.16.3\
cowplot_1.2.0\
gggenomes_1.1.3\
lubridate_1.9.5\
forcats_1.0.1\
stringr_1.6.0\
dplyr_1.2.0\
purrr_1.2.1\
readr_2.2.0\
tidyr_1.3.2\
tibble_3.3.1\
ggplot2_3.5.2\
ggplot2_4.0.0\
tidyverse_2.0.0 \cf2  \
\
Example code used for the command-line analyses are below: \
\
# for read QC: \
`fastqc -o fastqc_output/ 48538_1#370_1.fastq 48538_1#370_2.fastq`\

# for combining QC output and generating interactive ooutput files \
`multiqc --outdir multiqc_output --interactive fastqc_output`\

# for taxonomic prediction from reads\
# using the kraken standard database
`kraken2 --db /data/pam/software/kraken2/standard/k2_standard_20250402/ --use-names --report 48538_1#370.kreport --output 48538_1#370.kraken 48538_1#370_1.fastq 48538_1#370_2.fastq`\
\

# for genome assembly \
`unicycler -1 48538_1#370_1.fastq.gz -2 48538_1#370_2.fastq.gz -o assembly_48538_1#370 --mode normal`\
\
# for investigating assembly QC 
`quast.py -o quast_output_48538_1#370  assembly_48538_1#370/assembly.fasta`\
\
`checkm2 predict -i assembly_48538_1#370/assembly.fasta -o checkm2_48538_1#370 -x .fasta -t 24`\
\
# for taxonomic assignment based on assembly \
`gtdbtk classify_wf --batchfile list_of_fastas.txt --out_dir gtdb_tax_out --mash_db mashdb`\
\
# for annotation of genome assemblies\
`bakta --output bakta_output_directory/bakta_48538_1#370 --prefix 48538_1#370 --compliant --skip-plot --threads 16 --keep-contig-headers assembly_48538_1#370/assembly.fasta`\
\
# for generating a pangenome with a core gene alignment \
`panaroo -t 16 -i gff3_fna_files.txt -o panaroo_mimicus --clean-mode strict --remove-invalid-genes -a core --merge_paralogs`\
# run time ~2.5 days with 60 max threads and 5Gb memory\
\
# for generating a maximum-likelihood phylogenetic tree based on SNPs \
# extract SNP sites only\
`snp-sites -o snp-sites.fasta panaroo_mimicus/core_gene_alignment_filtered.aln`\
# generate a maximum-likelihood tree with specified model and 1000 ultrafast boostraps \
`iqtree -s snp-sites.out --prefix iqtree_out -T AUTO -m GTR+F+R10 -B 1000`\
# run time ~5 days with 60 max threads and 20Gb memory \cf2 \

# for finding virulence/AMR genes in assemblies
# for virulence genes with VF database
`abricate --db vfdb --quiet assembly_48538_1#370/assembly.fasta`\
# for AMR genes with CAR database
`abricate --db card --quiet assembly_48538_1#370/assembly.fasta`
# codeml ctl file for running PAML to estimate dN/dS
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
