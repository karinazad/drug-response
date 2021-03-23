# Drug Response

Predicting cytotoxity of cancer drugs.

## Datasets

* Broad-Novartis Cancer Cell Line Encyclopedia (CCLE) provides expression data for cancer cell lines which were treated with different cancer drugs. It is composed of 41,814 genomic features and 24 compounds profiled on 504 cell lines. The datasets were obtained using PharmacoGx https://pharmacodb.ca/pharmacogx?pgx=1.

The CCLE dataset was accessed using the following R script:

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

## Data Processing

The above described studies provide statistics of the dose-response curves to compound sensitivity values. Here, a summarized sensitivty value Act Area – the area above the fitted dose response curve (1/AUC) is used here along with IC50 – the concentration at which the compound reaches 50% reduction in cell viability, and EC50 – the concentration at which the compound reaches 50% of its maximum reduction in cell viability. Mutation data was summarized to binary gene-level variables represented as 0 (wild type) and 1 (mutation). Tumor types were one-hot encoded. 



## Approach

Given high-dimensionality of the datasets which contain expression profile for over 18,000 genes, an autoencoder was used to obtain the lower-dimensional latent space for gene expression patterns. 


