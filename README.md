# OptimGRAMMAR

## 1.Getting started

### 1.1	Downloading OptimGRAMMAR

OptimGRAMMAR can be downloaded from https://github.com/YuxinSong-prog/OptimGRAMMAR. It can be installed as a regular R package.

### 1.2	Installing OptimGRAMMAR

OptimGRAMMAR links to R packages Rcpp, RcppEigen, RcppArmadillo, BEDMatrix and data.table. These dependencies should be installed before installing OptimGRAMMAR. In addition, OptimGRAMMAR **requires PLINK2.0 Software (http://www.cog-genomics.org/plink/2.0/) with name “plink2.0” under your working directory**. Here is an example for installing OptimGRAMMAR and all its dependencies in an R session(assuming none of the R packages other than the default has been installed):
```
install.packages(c("BEDMatrix ", " data.table ", "Rcpp", " RcppEigen ", " RcppArmadillo "), repos = "https://cran.r-project.org/")
system(“R CMD install OptimGRAMMAR _1.0.tgz”)
```
## 2. Input

OptimGRAMMAR requires the phenotype and genotype files in PLINK BED data frame which also called PLINK 1 binary file and the structure of these files is described in http://www.cog-genomics.org/plink/1.9/formats#bed. How to prepare these data are describe below.

### 2.1 Phenotype

Phenotype should place in the sixth column of “.fam” file. 

### 2.2 Genotypes

OptimGRAMMAR can only take genotype files in “.bed” and “.bim” format.

## 3. Running OptimGRAMMAR
If OptimGRAMMAR has been successfully installed, you can load it in an R session using:<br>
```
library(OptimGRAMMAR)
```
and then loading "BEDMatrix "and " data.table " <br>
```
library(BEDMatrix)
library(data.table)
```
We provide two functions in OptimGRAMMAR: **Data** function for basic data management including extract phenotypic values, sampling markers, calculating allele frequencies and GRM and **optimGRAMMAR** function for association tests using optimGRAMMAR method, joint analysis based on the results of optimGRAMMAR, and outputting association result files.

### 3.1 Data function
#### Usage
```
Data (filename, nsmar, msampling)
```
#### Arguments
#### filename
An object class of character: the filename of PLINK BED files. The three PLINK files must have the same filename, for example, “filename.bed”, “filename.bim” and “filename.bam”.
#### nsmar
An optional numeric for the number of sampling markers. If this is unset, the “nsmar” default is 5,000.
#### msampling
logicals. If FLASE, entire markers will be used to calculate GRM. If this is unset or for large scale dataset, the “msampling” default is TURE.<br>

### 3.2 optimGRAMMAR function
#### Usage
```
optimGRAMMAR (Data, maxh2 = 0.5, opsm = 50000, ,Test = c("Separate","Joint") , Scan = c("Plink2","gcta"),QQ = T, Manh = T)
```

#### Arguments
#### Data
An object class of list generated from the **Data** function.
#### maxh2
Upper limit of polygenic heritability, which is set by default at 0.5.
#### opsm
The total number of SNPs used for optimization, which is set by  default at 50000.
#### AssoTst
You can choose correlation analysis software “GCTA” or “PLINK2.0” as prefer, “PLINK2.0” by default.
#### Test
An optional for association test, a test at once or the joint analysis. You can choose “Separate” for a test at once and “Joint” for further joint analysis based on the result of “Separate”.
#### QQ
logicals. If TURE, Q-Q plot would be drawn.
#### Manh
logicals. If TURE, Q-Q plot would be drawn.

## 4. Output

The **optimGRAMMAR** function generates a plink association text output file called “Grammar.PHENO1.glm.linear”. Here we show the header and the first 3 rows of the example output:<br>

CHROM|	POS|	ID|	REF|	ALT|	A1|	TEST|	OBS_CT|	BETA|	SE|	T_STAT|	P|	ERRCODE
---- | ----- | ------ | ------| ------| ------| ------| ------| ------| ------| ------| ------| ------
1|	10390|	S1_10390	|G|	A|	A|	ADD|	2648|	-0.00784112|	0.238845|	-0.0328293	|0.973813|	|.
1|	10590|	S1_10590	|T|	A|	A|	ADD|	2648|	-0.202364|	0.249746|	-0.810281	|0.417852|	|.
1|	128373|	S1_128373|	C|	T|	T|	ADD|	2648|	0.033819|	0.124565|	0.271498	|0.78603|	|.
…

In addition to the above file, a QTN candidate file, named “QTNs”, with Bonferroni as the threshold is also output. If joint analysis, a file, named “jointQTNs”, will display candidate QTNs resulting from joint analysis, which is the same format as “QTNs”.

## 5. Example
```
library(optimGRAMMAR)
library(BEDMatrix)
library(data.table)
setwd("./example")
plinkfilename <- "geno"
gdata <- Data(plinkfilename)
optimGRAMMAR (gdata)
```

