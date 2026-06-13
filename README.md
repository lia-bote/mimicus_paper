{\rtf1\ansi\ansicpg1252\cocoartf2870
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fnil\fcharset0 Menlo-Bold;\f1\fnil\fcharset0 Menlo-BoldItalic;\f2\fnil\fcharset0 Menlo-Regular;
\f3\fnil\fcharset0 .AppleSystemUIFontMonospaced-Regular;}
{\colortbl;\red255\green255\blue255;\red0\green0\blue0;\red255\green255\blue255;\red85\green142\blue40;
\red0\green0\blue255;\red0\green0\blue255;\red45\green101\blue22;\red45\green101\blue22;\red85\green142\blue40;
\red217\green11\blue5;\red217\green11\blue5;\red236\green244\blue251;\red236\green244\blue251;}
{\*\expandedcolortbl;;\cssrgb\c0\c0\c0;\cssrgb\c100000\c100000\c100000;\cssrgb\c39975\c61335\c20601;
\cssrgb\c0\c0\c100000;\cssrgb\c1680\c19835\c100000;\cssrgb\c21961\c46275\c11373;\cssrgb\c21961\c46275\c11373;\cssrgb\c39975\c61335\c20601;
\cssrgb\c88946\c14202\c0;\cssrgb\c88946\c14202\c0;\cssrgb\c94118\c96471\c98824;\cssrgb\c94118\c96471\c98824;}
\paperw11900\paperh16840\margl1440\margr1440\vieww14600\viewh15200\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\b\fs28 \cf2 Code and analysis for `\expnd0\expndtw0\kerning0
Genome dynamics of 
\f1\i Vibrio mimicus
\f0\i0  in cholera-endemic regions of Bangladesh`\
\

\f2\b0 This document describes the command-line analyses performed as part of this study, with example code for each stage showing which flags were used. Sequencing reads from this study corresponding to these examples are found in DOI:10.6084/m9.figshare.32664414. The output files/directories generated with each command, highlighting expected output, are \cf4 coloured in green\cf2  and described in the comments accompanying each line of code. Comments are also included with approximate run times for key stages of the analyses.\
\
The software used, with corresponding versions, are listed below. Examples of how these software were installed can be found in the R Notebook also included in this repository. These analyses can be run on a local computer or on a compute cluster, and no non-standard hardware were used. No other custom software was developed for this study. \
\
\pard\pardeftab720\partightenfactor0
\cf2 Downstream data processing and visualisation was performed on RStudio (Rv4.5.0) as detailed in the RMarkdown file also included in this repository. \kerning1\expnd0\expndtw0 \
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf2 \

\f0\b Command line tools used were:\

\f2\b0 \cf6 \CocoaLigature0 unicycler_0.5.0\
\expnd0\expndtw0\kerning0
\CocoaLigature1 fastqc_0.12.1\
multiqc_1.17--pyhdfd78af_1\
kraken2_2.1.2\
\pard\pardeftab720\partightenfactor0
\cf6 quast_5.0.2-c1\
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
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0
\cf2 \kerning1\expnd0\expndtw0 \

\f0\b R packages used were:\

\f2\b0 \cf6 paletteer_1.7.0\
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

\f0\b Example code used for the command-line analyses are below: \
\
# for read QC: \
\pard\pardeftab720\partightenfactor0

\f2\b0 \cf6 \expnd0\expndtw0\kerning0
`fastqc\cf2  \cf4 -o fastqc_output/\cf2  \kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\expnd0\expndtw0\kerning0
\CocoaLigature1 _1.fastq \kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\expnd0\expndtw0\kerning0
\CocoaLigature1 _2.fastq`\
\
\pard\pardeftab720\partightenfactor0

\f0\b \cf2 # for combining QC output \
\pard\pardeftab720\partightenfactor0

\f2\b0 \cf6 `multiqc\cf2  \cf4 --outdir multiqc_output\cf2  --interactive fastqc_output`\
\
\pard\pardeftab720\partightenfactor0

\f0\b \cf2 # for taxonomic prediction from reads\
# using the kraken standard database
\f2\b0 \
\pard\pardeftab720\partightenfactor0
\cf6 `kraken2\cf2  --db /data/pam/software/kraken2/standard/k2_standard_20250402/ --use-names --report \kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\expnd0\expndtw0\kerning0
\CocoaLigature1 .kreport \cf4 --output \kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\expnd0\expndtw0\kerning0
\CocoaLigature1 .kraken\cf2  \kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\expnd0\expndtw0\kerning0
\CocoaLigature1 _1.fastq \kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\expnd0\expndtw0\kerning0
\CocoaLigature1 _2.fastq`\
\
\pard\pardeftab720\partightenfactor0

\f0\b \cf2 # for genome assembly \

\f2\b0 \cf5 `unicycler \cf2 -1 \kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\expnd0\expndtw0\kerning0
\CocoaLigature1 _1.fastq.gz -2 \kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\expnd0\expndtw0\kerning0
\CocoaLigature1 _2.fastq.gz \cf4 -o assembly_\kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\cf2 \expnd0\expndtw0\kerning0
\CocoaLigature1  --mode normal`\
\
\pard\pardeftab720\partightenfactor0

\f0\b \cf2 # for investigating assembly QC 
\f2\b0 \cf7 \
\pard\pardeftab720\partightenfactor0
\cf5 `quast.py \cf4 -o quast_output_\kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\cf2 \expnd0\expndtw0\kerning0
\CocoaLigature1  \'a0assembly_\kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370/assembly.fasta`\
\
\pard\pardeftab720\partightenfactor0
\cf6 `checkm2 predict \cf2 -i \expnd0\expndtw0\kerning0
\CocoaLigature1 assembly_\kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370/assembly.fasta \cf4 -o checkm2_48538_1#370 \cf2 -x .fasta -t 24`\
\

\f0\b # for taxonomic assignment based on assembly \
\pard\pardeftab720\partightenfactor0

\f2\b0 \cf5 \expnd0\expndtw0\kerning0
\CocoaLigature1 `gtdbtk classify_wf \cf2 --batchfile list_of_fastas.txt \cf4 --out_dir gtdb_tax_out\cf2  --mash_db mashdb`\
\

\f0\b # for annotation of genome assemblies\

\f2\b0 \cf5 `bakta \cf4 --output bakta_output_directory/bakta_\kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\cf2 \expnd0\expndtw0\kerning0
\CocoaLigature1  --prefix \kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370\expnd0\expndtw0\kerning0
\CocoaLigature1  --compliant --skip-plot --threads 16 --keep-contig-headers assembly_\kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370/assembly\expnd0\expndtw0\kerning0
\CocoaLigature1 .fasta`\
\
\pard\pardeftab720\partightenfactor0

\f0\b \cf2 # for generating a pangenome with a core gene alignment \
\pard\pardeftab720\partightenfactor0

\f2\b0 \cf5 \outl0\strokewidth0 \strokec5 `panaroo \cf2 -t 16 -i \strokec8 gff3_fna_files.txt\strokec5  \cf9 -o \strokec8 panaroo_mimicus\cf2 \strokec5  --clean-mode strict --remove-invalid-genes -a core --merge_paralogs`\
\pard\pardeftab720\partightenfactor0
\cf10 \outl0\strokewidth0 # run time ~2.5 days with 60 max threads and 5Gb memory \cf2 \outl0\strokewidth0 \strokec5 \
\pard\pardeftab720\partightenfactor0
\cf2 \

\f0\b # for generating a maximum-likelihood phylogenetic tree based on SNPs \
# extract SNP sites only\

\f2\b0 \cf5 `snp-sites \cf9 -o \strokec8 snp-sites.fasta \cf2 panaroo_mimicus/\strokec5 core_gene_alignment_filtered.aln`\

\f0\b # generate a maximum-likelihood tree with specified model and 1000 ultrafast boostraps
\f2\b0 \
\cf5 `iqtree \cf2 -s \strokec8 snp-sites.out\strokec5  --prefix \strokec8 iqtree_out\strokec5  -T AUTO -m GTR+F+R10 -B 1000`\
\cf11 # run time ~5 days with 60 max threads and 20Gb memory \cf2 \

\f0\b \
# for finding virulence/AMR genes in assemblies
\f2\b0  \

\f0\b # for virulence genes with VF database
\f2\b0 \
\pard\pardeftab720\partightenfactor0

\f3\fs27\fsmilli13600 \cf2 \strokec12 `abricate --db vfdb --quiet 
\f2\fs28 \cf2 \outl0\strokewidth0 assembly_\kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370/assembly\expnd0\expndtw0\kerning0
\CocoaLigature1 .fasta`\
\pard\pardeftab720\partightenfactor0

\f0\b \cf2 # for AMR genes with CAR database
\f2\b0 \
\pard\pardeftab720\partightenfactor0

\f3\fs27\fsmilli13600 \cf2 `abricate --db card --quiet 
\f2\fs28 assembly_\kerning1\expnd0\expndtw0 \CocoaLigature0 48538_1#370/assembly\expnd0\expndtw0\kerning0
\CocoaLigature1 .fasta`
\f3\fs27\fsmilli13600 \cf2 \outl0\strokewidth0 \strokec12 \
\pard\pardeftab720\partightenfactor0

\f2\fs28 \cf0 \strokec5 \

\f0\b # codeml ctl file for running PAML to estimate dN/dS
\f2\b0 \
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\pardirnatural\partightenfactor0
\cf0 \kerning1\expnd0\expndtw0 \CocoaLigature0 \outl0\strokewidth0       seqfile = clustalw_nuc_aln.fasta            * Path to the alignment file\
     treefile = tcpA_codon_rename_no_len.tree           * Path to the tree file\
      outfile = out_sites.txt            * Path to the output file\
   \
        noisy = 3              * How much rubbish on the screen\
      verbose = 1              * More or less detailed report\
\
      seqtype = 1              * Data type\
        ndata = 1           * Number of data sets or loci\
        icode = 0              * Genetic code \
    cleandata = 0              * Remove sites with ambiguity data?\
                \
        model = 0         * Models for \uc0\u969  varying across lineages\
          NSsites = 0 1 2 7 8        * Models for \uc0\u969  varying across sites\
    CodonFreq = 7        * Codon frequencies\
          estFreq = 0        * Use observed freqs or estimate freqs by ML\
        clock = 0          * Clock model\
    fix_omega = 0         * Estimate or fix omega\
        omega = 0.5        * Initial or fixed omega}