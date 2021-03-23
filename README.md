# Drug Response

Predicting cytotoxity of cancer drugs.

## Datasets

* Genomics of Drug Sensitivity in Cancer (GDSC) database provide gene expression, copy number variation and coding variants for s thousand of cancer cell lines. In this work, gene expression data are used. 

* Broad-Novartis Cancer Cell Line Encyclopedia (CCLE) provides expression data for over 500 cancer cell lines which were treated with 24 different cancer drugs. The datasets were obtained using PharmacoGx's R script: https://pharmacodb.ca/pharmacogx?pgx=1

* CMAP L1000 is contains gene expression data of cancer cell lines before and after treatment. Such drug-induced petrubation data are available combinations of 978 genes and thousands of cancer drugs or other small molecules. Previously, this dataset is also known as Library of Integrated Network based Cellular Signatures (LINCS). Version Phase II is used here. Available at:

### Accessing the datasets
The CCLE dataset was accessed using the followin R script:

```
source("http://www.bioconductor.org/biocLite.R") 
biocLite("PharmacoGx")
library(PharmacoGx)

# Download the object for CCLE 
CCLE <- downloadPSet(CCLE) 

# Plot Drug Dose response curves, using the same names for compounds and cell lines as PharmacoDB 
drugDoseResponseCurve(CCLE, drug="paclitaxel", cell="MCF7") 

# Extract the expression data to a matrix 
CCLE.expression <- summarizeMolecularProfiles(CCLE, mDataType="rna") 

# Run a linear model for univariate biomarker discovery 
CCLE.sensitivity.signatures <- drugSensitivitySig(CCLE, mDataType="rna", sensitivity.measure="auc_recomputed")
```



## Approach

Given high-dimensionality of both datasets which contain over 17,000 genes (features), an autoencoder was used to obtain the lower-dimensional latent space for gene expression patterns. 

