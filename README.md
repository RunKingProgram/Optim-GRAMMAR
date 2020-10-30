# OptimGRAMMAR

## 1.Getting started

### 1.1	Downloading OptimGRAMMAR

GRL can be downloaded https://github.com/YuxinSong-prog/OptimGRAMMAR. It can be installed as a regular R package.

### 1.2	Installing OptimGRAMMAR

GRL links to R packages Rcpp, RcppEigen and RcppArmadillo, and also imports R packages BEDMatrix and data.table. These dependencies should be installed before installing OptimGRAMMAR. In addition, OptimGRAMMAR **requires PLINK2.0 Software (http://www.cog-genomics.org/plink/2.0/) with name “plink2.0” under your run directory**. Here is an example for installing OptimGRAMMAR and all its dependencies in an R session(assuming none of the R packages other than the default has been installed):

install.packages(c("BEDMatrix ", " data.table ", "Rcpp", " RcppEigen ", " RcppArmadillo "), repos = "https://cran.r-project.org/")<br>system(“R CMD install OptimGRAMMAR _1.0.tgz”)

## 2. Input

OptimGRAMMAR requires the phenotype and genotype files in an PLINK BED data frame which also called PLINK 1 binary file and the structure of these files is described in http://www.cog-genomics.org/plink/1.9/formats#bed. How to prepare these data are describe below.

### 2.1 Phenotype

Phenotype should place in the sixth column of “.fam” file. The missing phenotype value for quantitative traits is -9.

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
We provide two functions in OptimGRAMMAR: **Data** function for basic data management including extract phenotypic values, sampling markers, calculate allele frequencies and calculating GRM, saved in an external file, used for GBLUP method or the transformed GRM for large scale dataset and **optimGRAMMAR** function for association tests using optimGRAMMAR method, joint analysis based on the results of optimGRAMMAR, and outputting association result file then drawing Q-Q and Manhattan plot .

### 3.1 Data function
#### Usage
```
Data (filename, nsmar, msampling)
```
Arguments<br>
filename<br>    An object class of character: the filename before the suffix of plink files. The three plink file must have a same filename, for example, “filename.bed”, “filename.bim” and “filename.bam”.<br>
nsmar<br>     An optional numeric for the number of sampling markers. If this is unset, the “nsmar” default is 5,000.<br>
msampling<br>  logicals. If FLASE, entire markers will be used to calculate GRM. If this is unset or for large scale dataset, the “msampling” default is TURE.<br>

### 3.2 optimGRAMMAR function
#### Usage
```
optimGRAMMAR (Data, maxh2 = 0.5, opsm = 50000, ,Test = c("Separate","Joint") , Scan = c("Plink2","gcta"),QQ = T, Manh = T)
```

Arguments<br>
Data<br>        An object class of list from the 1st step.<br>
maxh2<br>       Upper limit of polygenic heritability, which is set by default at 0.5.<br>
opsm<br>        The total number of SNPs used for optimization, which is set by  default at 50000.<br>
AssoTst<br>     You can choose correlation analysis software “GCTA” or “PLINK2.0” as prefer, “PLINK2.0” by default.<br>
Test<br>        An optional for association test, a test at once or joint analysis. You can choose “Separate” for a 
            test at once and “Joint” for further joint analysis based on the result of “Separate”.<br>
QQ<br>          logicals. If TURE, Q-Q plot would be drawn.<br>
Manh<br>        logicals. If TURE, Q-Q plot would be drawn.<br>

## 4. Output
### 4.1 optimGRAMMAR result

The Grammar function generates a plink association text output file called “Grammar.PHENO1.glm.linear”. Here we show the header and the first five rows of the example output:<br>
```
#CHROM	POS	ID	REF	ALT	A1	TEST	OBS_CT	BETA	SE	T_STAT	P	ERRCODE
1	10390	S1_10390	G	A	A	ADD	2648	-0.00784112	0.238845	-0.0328293	0.973813	.
1	10590	S1_10590	T	A	A	ADD	2648	-0.202364	0.249746	-0.810281	0.417852	.
1	128373	S1_128373	C	T	T	ADD	2648	0.033819	0.124565	0.271498	0.78603	.
…
```
In addition to the above file, a QTN candidate file, named “QTNs”, with Bonferroni as the threshold is also output. If joint analysis, a file, named “jointQTNs”, will display candidate QTNs resulting from joint analysis, which is the same format as “QTNs”.






