# kmerPyramid

R package to visualize the acgt or k-mer distribution between samples.

<p align="center">
  <img src="img/kmerPlot.png" width="300">
  <img src="img/animated_pyramide.gif" width="300">
</p>

## Table of Contents
1. [Installation](#installation)
2. [Examples](#examples)
3. [Tutorial](#tutorial)

## Installation

Get the released version from CRAN:

```R
## not available yet
## install.packages("kmerPyramid")
```

Or the development version from github:

```R
# install.packages("devtools")
devtools::install_github("jkruppa/kmerPyramid")
```

## Examples

### acgt pyramid 3D

```R
library(kmerPyramid)

data(viralExampleSeqs)
 
kmer_distr <- get_kmer_distribution(viralExampleSeqs, k = 1)
 
pyramid_3d(kmer_distr,
           cex = 2,
           color = "blue")
 
ids <- names(viralExampleSeqs)
 
pyramid_3d(kmer_distr,
           ids = ids,
           cex = 2,
           color = "blue",
           identify = TRUE)
 
data(viralExampleCodingSeq)
 
kmer_distr <- get_kmer_distribution(viralExampleCodingSeq, k = 1)
text_ids <- ifelse(names(viralExampleCodingSeq) == "non_coding", "x", "o")
color_ids <- ifelse(names(viralExampleCodingSeq) == "non_coding", "black", "red")
 
pyramid_3d(kmer_distr,
           cex = 1,
           text = text_ids,
           color = color_ids)
 
ids <- names(viralExampleCodingSeq)

pyramid_3d(kmer_distr,
           ids = ids,
           cex = 1,
           text = text_ids,
           color = color_ids,
           identify = TRUE)
```

<p align="center">
  <img src="img/pyramid_3d_example0.PNG" width="300">
</p>

### k-mer pyramid 3D with sliding window

```R
library(kmerPyramid)

data(viralExampleSeqs)

viral_window_list <- get_pca_window_list(viralExampleSeqs, window = 2)

pyramid_3d_window(viral_window_list[1],
                  color = "red")
```
<p align="center">
  <img src="img/pyramid_3d_example1.PNG" width="300">
</p>

```R
pyramid_3d_window(viral_window_list[1],
                  color = "red",
                  identify = TRUE)
```
<p align="center">
  <img src="img/pyramid_3d_example2.PNG" width="300">
</p>

```R
pyramid_3d_window(viral_window_list[c(3,5)],
                  difference = TRUE)
```
<p align="center">
  <img src="img/pyramid_3d_example3.PNG" width="300">
</p>

```R
pyramid_3d_window(viral_window_list[c(3,5)],
                  difference = TRUE,
                  identify = TRUE)
```
<p align="center">
  <img src="img/pyramid_3d_example4.PNG" width="400">
</p>

```R
pyramid_3d_window(viral_window_list[c(3,5)],
                  difference = TRUE,
                  bw = TRUE,
                  bw.cex = 75,
                  identify = TRUE)
```

<p align="center">
  <img src="img/pyramid_3d_example5.PNG" width="400">
</p>

## Tutorial

We obtain a single random fasta file with three virus sequences under /data/virus.fa. This file can be directly loaded into R by using the package Biostrings. The apckage should be installed automatically by the kmerPyramid package. If not please follow the instructions under https://bioconductor.org/packages/release/bioc/html/Biostrings.html. 

```R
library(Biostrings)
sequence <- readDNAStringSet("https://raw.githubusercontent.com/jkruppa/kmerPyramid/master/data/virus.fa")
```

```R
library(Biostrings)
sequence <- readDNAStringSet("C:/path/to/my/fasta/my_fasta_file.txt")
```
