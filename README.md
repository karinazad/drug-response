# Drug Response

Predicting cytotoxity of cancer drugs.

## Table of Content
- [Drug Response](#drug-response)
  * [Datasets](#datasets)
  * [Data Processing](#data-processing)
  * [Approach](#approach)
  * [Usage](#usage)
    + [Installation](#installation)
    + [Run examples](#run-examples)

## Datasets

* Broad-Novartis Cancer Cell Line Encyclopedia (CCLE) provides expression data for cancer cell lines which were treated with different cancer drugs. It is composed of 41,814 genomic features and 24 compounds profiled on 504 cell lines. The datasets were obtained using PharmacoGx https://pharmacodb.ca/pharmacogx?pgx=1. For the drug response target a binarized version of dose-response curves is used.

The CCLE dataset was accessed using the following R script. 

```
# Install PharmacoGx package via Bioconductor
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("PharmacoGx")
biocLite("PharmacoGx")

library(PharmacoGx)

# Download the object for CCLE 
CCLE <- downloadPSet(CCLE) 

# Extract the expression data
CCLE.expression <- summarizeMolecularProfiles(CCLE, mDataType="rna") 

# Run a linear model for univariate biomarker discovery 
CCLE.sensitivity.signatures <- drugSensitivitySig(CCLE, mDataType="rna", sensitivity.measure="auc_recomputed")
```

## Data Processing

The above described studies provide statistics of the dose-response curves to compound sensitivity values. Here, a summarized sensitivty value Act Area – the area above the fitted dose response curve (1/AUC) is used here along with IC50 – the concentration at which the compound reaches 50% reduction in cell viability, and EC50 – the concentration at which the compound reaches 50% of its maximum reduction in cell viability. Mutation data was summarized to binary gene-level variables represented as 0 (wild type) and 1 (mutation). Tumor types were one-hot encoded. 



## Approach

Given high-dimensionality of the datasets which contain expression profile for over 18,000 genes, an autoencoder was used to obtain the lower-dimensional latent space for gene expression patterns. 

<img src="https://miro.medium.com/max/926/1*1sfunl2TIRyaoKcQIEviPA.png">

## Usage

### Installation
To install the repo and get the requirements:
```
git clone https://github.com/karinazad/drug-response.git
cd drug-response
pip install -r requirements.txt
```
### Run examples
To run an example of drug-response prediction:

```
python src/drug-response/run.py
```
                                                                               




