<!-- badges: start -->
[![R-CMD-check](https://github.com/campbio/scruff/workflows/R-CMD-check/badge.svg)](https://github.com/campbio/scruff/actions)
<!-- badges: end -->

# scruff: Single Cell RNA-Seq UMI Filtering Facilitator

[**scruff**](https://doi.org/10.1186/s12859-019-2797-2) (**S**ingle **C**ell **R**NA-Seq **U**MI **F**iltering **F**acilitator) is a package for processing single cell RNA-seq (scRNA-seq) FASTQ reads generated by CEL-Seq and CEL-Seq2 protocols. It demultiplexes scRNA-seq FASTQ files, aligns reads to reference genome using [Rsubread](https://doi.org/10.1093/nar/gkz114), and generates UMI filtered count matrix.

## Workflow
<p align="center"><img src="https://github.com/campbio/scruff/raw/master/data-raw/figure/20190312_scruff_workflow.png" height="900"></p>

To install the latest stable release of `scruff` from [Bioconductor](http://bioconductor.org/packages/scruff/):
```
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("scruff")
```

To install the development version of `scruff` from GitHub using `devtools`:
```
library(devtools)
install_github("campbio/scruff")
```

## Package User Guide

An introduction to `scruff` package is available [here](http://bioconductor.org/packages/release/bioc/vignettes/scruff/inst/doc/scruff.html).

## Speed

<p align="center"><img src="https://github.com/campbio/scruff/raw/master/data-raw/figure/20190312_scruff_figure_5.png" height="400"></p>

Run time benchmarks for selected scRNA-seq preprocessing packages. FASTQ files from the example dataset [(Van den Brink et al. 2017)](https://www.nature.com/articles/nmeth.4437) were subsampled to have a total read number of 0.1, 0.5, 1.0, 5.0, and 10.0 million. Each of the subsampled datasets was processed by [celseq2](https://github.com/yanailab/celseq2), [scPipe](https://doi.org/10.1371/journal.pcbi.1006361), and **scruff**. All 3 packages were parallelized with 16 cores. The job was run on a cluster node with 2 eight-core 2.6 GHz Intel Xeon E5-2670 CPUs and 256 GB memory. For the subsampled dataset with 10 million reads, scruff took 34.9 minutes to finish while celseq2 and scPipe took 143.2 and 69.0 minutes.

## Example QC plots

The following selected QC plots are generated using data from [(Van den Brink et al. 2017)](https://www.nature.com/articles/nmeth.4437) and **scruff** package. Metrics and QC plots reported by **scruff** includes total number of reads, number of reads mapped to reference genome, number of reads mapped to genes, fraction of mapped reads to total reads, fraction of reads mapped to genes to reads mapped to genome, fraction of reads mapped to genes to total number of reads, total number of transcripts, number of mitochondrial transcripts, fraction of mitochondrial transcripts, number of transcribed genes, fraction of protein coding genes, fraction of protein coding transcripts, median and average number of reads per corrected and uncorrected UMI counts, and the number of detected genes divided by total number of reads sequenced per million.

![scruff total_reads](https://github.com/campbio/scruff/raw/master/data-raw/figure/20180907_vdb_newplots_ercc_edit_Page_01.png)

![scruff aligned_reads_fraction](https://github.com/campbio/scruff/raw/master/data-raw/figure/20180907_vdb_newplots_ercc_edit_Page_04.png)

These are boxplots with overlaid points. Each point represents a well (unique cell barcode) and is colored by the number of cells sorted in the well by FACS. Each boxplot denotes a different experiment (i.e. plate). Sample *mouse c library 2* have similar number of total reads but much less fraction of aligned reads compared to other experiments, showing its poor quality.

## Read alignment visualization colored by UMI

![read_alignment_UMI](https://github.com/campbio/scruff/raw/master/data-raw/figure/20190124_scruff_figure_3.png)

**scruff** package provides functions to visualize gene isoforms and UMI tagged read alignments at specified genomic coordinates. 125 reads were mapped to the gene Fos in cell 30 of mouse b library 1 from the example CEL-Seq dataset [(Van den Brink et al. 2017)](https://www.nature.com/articles/nmeth.4437). Upper panel shows the visualization of read alignments. Reads are represented by arrows and are colored by their UMIs. The direction of the arrow represents the mapping strand of the read. Lower panel shows the visualization of gene isoforms. Gene isoforms are labeled by their transcript names. Grey rectangles represent exons.

## QC plots for 10X Genomics data

![read_alignment_UMI](https://github.com/campbio/scruff/raw/master/data-raw/figure/20181221_scruff_figure_4.png)

**scruff** provides function to visualize read alignment quality of BAM files processed by Cell Ranger. BAM files for 6 PBMC datasets ([3K](https://support.10xgenomics.com/single-cell-gene-expression/datasets/1.1.0/pbmc3k), [6K](https://support.10xgenomics.com/single-cell-gene-expression/datasets/1.1.0/pbmc6k), [4K](https://support.10xgenomics.com/single-cell-gene-expression/datasets/2.1.0/pbmc4k), [8K](https://support.10xgenomics.com/single-cell-gene-expression/datasets/2.1.0/pbmc8k), [1K](https://support.10xgenomics.com/single-cell-gene-expression/datasets/3.0.0/pbmc_1k_v3), [10K](https://support.10xgenomics.com/single-cell-gene-expression/datasets/3.0.0/pbmc_10k_v3)) were downloaded from 10X Genomics website and processed by **scruff** to obtain (a) the number of reads aligned to reference genome, (b) the number of reads mapped to genes, and (c) the fraction of reads mapped to genes out of total number of aligned reads.

## How to cite [**scruff**](https://doi.org/10.1186/s12859-019-2797-2)
- Wang Z, Hu J, Johnson WE, Campbell JD. scruff: an R/Bioconductor package for preprocessing single-cell RNA-sequencing data. BMC bioinformatics. 2019;20(1):222.
