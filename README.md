# HCMV RNA-seq Analysis Pipeline

## Overview

This repository contains a snakemake-based pipeline for RNA-Seq analysis of Human Cytomegalovirus (HCMV) transcriptomes to quantify expression, identify differentially expressed genes across two timepoints (2dpi vs 6dpi), assemble viral reads, and determine strain similarity using BLASTn.

All the results are summarized in a single output file called **`Ofosu_PipelineReport.txt`**

## What the pipeline does

## For each sample, the pipeline performs the following steps:

---
-   Extracts coding sequences (CDS) sequences from the HCMV reference genome
-   Builds a kallisto transcriptome index
-   Quantifies transcript expression using kallisto
-   Runs sleuth differential expression analysis (R script)
-   Builds a Bowtie2 genome index
-   Maps reads to the HCMV genome
-   Counts reads before and after mapping
-   Assembles RNA reads using SPAdes
-   Extracts the longest contig from each assembly
-   Runs BLASTN of the longest contig against a Betaherpesvirinae nucleotide database 
---

## Dependencies

The following tools and softwares must be installed and available:

-   snakemake 7.32.4 (<https://snakemake.readthedocs.io/en/v7.32.0/getting_started/installation.html>)
-   Python 3.12.3 (<https://www.python.org/downloads/release/python-3123/>)
-   R 4.5.2 (<https://cran.r-project.org/bin/windows/base/>)
-   kallisto 0.51.1 (<https://pachterlab.github.io/kallisto/download>)
-   bowtie2 2.5.2 (<https://anaconda.org/bioconda/bowtie2>)
-   sleuth (<https://pachterlab.github.io/sleuth/download>)
-   spades v3.15.5 (<https://github.com/ablab/spades/releases>)
-   conda (<https://anaconda.org/anaconda/conda>)

## Repository Structure

---
├─ \~/HCMV/
\|──BLAST/
\|──genome
\|── genome.ndb
\|──genome.nhr
\|──genome.nin
\|──genome.not
\|──genome.nsq
\|──genome.ntf
\|──genome.nto

\|──GCF_000845245.1/
\|──genomic.fna
\|──genomic.gff

\|──README.md/

\|──SCRIPTS/
\|──count_reads.sh
\|──extract_cds.py
\|──longest_contig.py
\|──sleuth_analysis.R

\|──SNAKEMAKE/
\|──Snakefile

\|──TESTS/
\|──SRR5660030_1.fastq
\|──SRR5660030_2.fastq
\|──SRR5660033_1.fastq
\|──SRR5660033_2.fastq
\|──SRR5660044_1.fastq
\|──SRR5660044_2.fastq
\|──SRR5660045_1.fastq
\|──SRR5660045_2.fastq
---

## Downloading the repository

Clone this repository into your **home directory** before running the pipeline.

`      
cd ~
`

From your home directory, run:

`git clone https://github.com/bofosu01/RNA_Seq_Analysis.git`

Move into the directory containing the Snakefile

`cd HCMV/SNAKEMAKE`

## How to run the pipeline

### Dry run Check that everything is connected correctly

`snakemake --dry-run`

### Run the pipeline

`snakemake --cores 4`
