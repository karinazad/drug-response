# Drug Response

Predicting cytotoxity of cancer drugs.

## Datasets

* Genomics of Drug Sensitivity in Cancer (GDSC) database provide gene expression, copy number variation and coding variants for s thousand of cancer cell lines. In this work, gene expression data are used. The datasets were obtained using PharmacoGx's R script: https://pharmacodb.ca/pharmacogx?pgx=1

* Broad-Novartis Cancer Cell Line Encyclopedia (CCLE) provides expression data for over 500 cancer cell lines which were treated with 24 different cancer drugs. Available at:

* CMAP L1000 is contains gene expression data of cancer cell lines before and after treatment. Such drug-induced petrubation data are available combinations of 978 genes and thousands of cancer drugs or other small molecules. Previously, this dataset is also known as Library of Integrated Network based Cellular Signatures (LINCS). Version Phase II is used here. Available at:

### Downloading the dataset



## Approach

Given high-dimensionality of both datasets which contain over 17,000 genes (features), an autoencoder was used to obtain the lower-dimensional latent space for gene expression patterns. 

