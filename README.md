# OptimGRAMMAR

## 1.Getting started

### 1.1	Downloading OptimGRAMMAR

GRL can be downloaded https://github.com/YuxinSong-prog/OptimGRAMMAR. It can be installed as a regular R package.

### 1.2	Installing OptimGRAMMAR

GRL links to R packages Rcpp, RcppEigen and RcppArmadillo, and also imports R packages BEDMatrix and data.table. These dependencies should be installed before installing OptimGRAMMAR. In addition, OptimGRAMMAR **requires PLINK2.0 Software (http://www.cog-genomics.org/plink/2.0/) with name “plink2.0” under your run directory**. Here is an example for installing OptimGRAMMAR and all its dependencies in an R session(assuming none of the R packages other than the default has been installed):

install.packages(c("BEDMatrix ", " data.table ", "Rcpp", " RcppEigen ", " RcppArmadillo "), repos = "https://cran.r-project.org/")<br>system(“R CMD install OptimGRAMMAR _1.0.tgz”)

## 2.Input

OptimGRAMMAR requires the phenotype and genotype files in an PLINK BED data frame which also called PLINK 1 binary file and the structure of these files is described in http://www.cog-genomics.org/plink/1.9/formats#bed. How to prepare these data are describe below.

### 2.1 Phenotype

Phenotype should place in the sixth column of “.fam” file. The missing phenotype value for quantitative traits is -9.

### 2.2 Genotypes

OptimGRAMMAR can only take genotype files in “.bed” and “.bim” format.

## 3.Running OptimGRAMMAR
If OptimGRAMMAR has been successfully installed, you can load it in an R session using:<br>
```
library(OptimGRAMMAR)
```
and then loading "BEDMatrix "and " data.table " <br>
```
library(BEDMatrix)
library(data.table)
```
