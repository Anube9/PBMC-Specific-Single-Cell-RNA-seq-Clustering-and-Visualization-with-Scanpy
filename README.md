## PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy

This project used the SCANPY Python library to cluster and visualize single-cell RNA sequencing (scRNA-seq) data from peripheral blood mononuclear cells (PBMCs). Key steps included data preprocessing, dimensionality reduction via PCA, neighborhood graph construction and UMAP visualization, cell clustering using the Leiden algorithm, and marker gene identification to annotate the cell types.
##  Installations
```
pip install SCANPY
pip install NumPy
pip install Pandas
pip install Matplotlib
pip install AnnDATA
pip install leidnalg
pip install Seaborn3

```
SCANPY is a python based single cell analysis package. This proposed framework integrates complex analysis workflows into a single dashboard that enables multidimensional data exploration, deep learning classification and prediction, and built-in visualization through Python scripts.
Scanpy uses a data form called ANNDATA for the analysis. An ANNDATA object represents a data matrix with annotations. It gives access to machine-learning tools to easily extract information without occupying much memory. It is similar to R’s EXPRESSIONSET but supports sparse data and saves data on a disc in HDF5-based format, which is not dependent on the platform, framework, and language. This allows operating on an ANNDATA object without fully loading it into memory. Its graph of neighborhood relations among data points is better than the popular package SCIKIT-LEARN
##  DATA DESCRIPTION 
Dataset (with intronic reads) a single cell expression dataset by Cell Ranger 6.1.2 version is taken from the 10x genomics database. Human peripheral blood mononuclear cells (PBMCs) were obtained by 10x Genomics from AllCells from a healthy female donor aged 25-30 years.
Out of 16,000 cells (11,984 cells recovered) as described in the Chromium Single Cell 3' Reagent Kits User Guide (v3.1 Chemistry Dual Index) (CG000315 Rev C) using the Chromium X. The reads are sequenced on an Illumina NovaSeq 6000 to a read depth of approximately 40,000 mean reads per cell.
## DATA ANALYSIS
# Data Pre-processing:
Data is retrieved from unzipped files and processed by identifying high fraction genes, filtering out cells with less than 3 detected genes, removing mitochondrial genes, and storing the count matrix as AnnData. <br>
!<img width="467" alt="Screenshot 2024-03-22 at 6 03 33 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/d51a7b62-eeed-47ec-a41d-aea725b00ce0"> <br>
shows the genes that yield the highest fraction of counts in every single cell, across all cells.<br>
!<img width="477" alt="Screenshot 2024-03-24 at 11 16 01 AM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/d8793038-1f5e-438d-94f0-1673a8e8cc11"> <br>
A violin plot of the number of genes expressed in the count matrix, total counts, and the percentage of the mitochondrial genes in the cell.<br>
# Normalization and Feature selection
Total count normalization is performed to ensure uniform counts across cells.
Data is log normalized and highly variable genes are identified using PCA.
# Dimensionality Reduction:
PCA is performed to reduce data dimensionality while retaining dataset variability.
Principal components (PCs) contributing to dataset variance are selected.
# Embedding and Visualization:
Neighborhood graph is computed and embedded in two dimensions using UMAP.
UMAP is preferred over tSNE for visualizing similar cell types.
Clustering is done using Leiden algorithm on the neighborhood graph to identify cell clusters.
# Differential Gene Expression Analysis:
Statistical tests (t-test, Wilcoxon rank-sum test, and logistic regression) are performed to identify marker genes.
Marker genes and literature are used to determine cell types and annotate clusters.
# Visualization:
Various visualization methods are employed to represent genes and clusters.

## RESULTS
The analysis of this dataset resulted in an AnnData matrix with 11984 observations and 36601 genes. In the data preprocessing 32 cells were filtered out which have less than 200 genes and 9238 genes that are present in less than 3 cells are filtered out. After performing the data scaling further analysis was done with 964 observations and 3553 genes. The loadings of the three PCs are visualized to see the expressed gene for each PC and embeddings are visualized using UMAP. After the application of Leiden 11 clusters were found. Further analysis was done, and marker genes were identified as FHIT, FOXP1, CD8B, PITPNC1, ITGB1, NKG7, CD74, ANXA1, S100A9, RTKN2, PPBP.

