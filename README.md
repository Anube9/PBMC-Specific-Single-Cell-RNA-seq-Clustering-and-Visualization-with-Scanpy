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
## DATA DESCRIPTION 
Dataset (with intronic reads) a single cell expression dataset by Cell Ranger 6.1.2 version is taken from the 10x genomics database. Human peripheral blood mononuclear cells (PBMCs) were obtained by 10x Genomics from AllCells from a healthy female donor aged 25-30 years.
Out of 16,000 cells (11,984 cells recovered) as described in the Chromium Single Cell 3' Reagent Kits User Guide (v3.1 Chemistry Dual Index) (CG000315 Rev C) using the Chromium X. The reads are sequenced on an Illumina NovaSeq 6000 to a read depth of approximately 40,000 mean reads per cell.
## DATA ANALYSIS
# Data Pre-processing:
Data is retrieved from unzipped files and processed by identifying high fraction genes, filtering out cells with less than 3 detected genes, removing mitochondrial genes, and storing the count matrix as AnnData. <br>
<img width="467" alt="Screenshot 2024-03-22 at 6 03 33 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/d51a7b62-eeed-47ec-a41d-aea725b00ce0"> <br>
The above image shows the genes that yield the highest fraction of counts in every single cell, across all cells.<br>
<img width="716" alt="Screenshot 2024-03-24 at 1 17 44 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/96b40448-f34e-4538-a08b-46db66dff75d"><br>
This violin plot of the number of genes expressed in the count matrix, total counts, and the percentage of the mitochondrial genes in the cell.<br> 
<img width="679" alt="Screenshot 2024-03-24 at 1 20 14 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/65ad8744-1725-4eda-af1e-b4becbe6c7d9"><br>
This Scatter plot shows the distribution of total gene counts in the cell’s vs mitochondrial genes and genes by counts.<br>
# Normalization and Feature selection
Total count normalization is performed to ensure uniform counts across cells.<br>
Data is log normalized and highly variable genes are identified using PCA.<br>
<img width="475" alt="Screenshot 2024-03-24 at 1 25 56 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/ad27d638-a729-45b0-a644-e160f8f9ac43"><br>
The above figure shows the distribution of the highly variable genes before and after data normalization.<br>
<img width="304" alt="Screenshot 2024-03-24 at 2 18 08 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/1ede091b-0291-4537-ba62-fe483a118b8b"><br>
This shows the variance of each PC in the data set is visualized to Consider these for further analysis.<br>
# Dimensionality Reduction:
PCA is performed to reduce data dimensionality while retaining dataset variability.
Principal components (PCs) contributing to dataset variance are selected.
<img width="905" alt="Screenshot 2024-03-24 at 2 20 20 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/6b51c0c1-7e13-480c-8ffa-18b0aabf7aa3"><br>
The graph embedding is visualized in two dimensions using UMAP of the highly expressed genes in the first three PCs.<br>
# Embedding and Visualization:
Neighborhood graph is computed and embedded in two dimensions using UMAP.
UMAP is preferred over tSNE for visualizing similar cell types.
Clustering is done using Leiden algorithm on the neighborhood graph to identify cell clusters.
<img width="958" alt="Screenshot 2024-03-24 at 2 22 06 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/58086696-b09f-48b5-84e2-9348983ec950"><br>
The graph embeddings of the scaled and normalized data<br>
# Differential Gene Expression Analysis:
Statistical tests (t-test, Wilcoxon rank-sum test, and logistic regression) are performed to identify marker genes.<br>
Marker genes and literature are used to determine cell types and annotate clusters.<br>
![Unknown](https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/303d2905-afd3-4395-8070-02e70d42792d)<br>
Analysis of highly differential genes in all the 11 clusters using t-test
# Visualization:
Various visualization methods are employed to represent genes and clusters.<br>
<img width="267" alt="Screenshot 2024-03-24 at 2 23 26 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/70b7b94e-53eb-4f99-ba66-7b0e55c84d3f"><br>
11 clusters resulted from the Leiden clustering depending on the marker genes<br>
<img width="393" alt="Screenshot 2024-03-24 at 2 23 36 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/aa4c7bf8-dee0-4544-842c-a8ba3163a916"><br>
The cell type annotation of the clusters is based on the cell type. The clusters were merged into 9 clusters as two of the genes belonged to the B-cells and germ cells.<br>
<img width="510" alt="Screenshot 2024-03-24 at 2 32 39 PM" src="https://github.com/Anube9/PBMC-Specific-Single-Cell-RNA-seq-Clustering-and-Visualization-with-Scanpy/assets/112353734/8bd8d031-62d4-4945-a483-06f6b881c3fc"><br>
The dot plot shows the expression of the marker genes in each cluster.<br>
## RESULTS
The analysis of this dataset resulted in an AnnData matrix with 11984 observations and 36601 genes. In the data preprocessing 32 cells were filtered out which have less than 200 genes and 9238 genes that are present in less than 3 cells are filtered out. After performing the data scaling further analysis was done with 964 observations and 3553 genes. The loadings of the three PCs are visualized to see the expressed gene for each PC and embeddings are visualized using UMAP. After the application of Leiden 11 clusters were found. Further analysis was done, and marker genes were identified as FHIT, FOXP1, CD8B, PITPNC1, ITGB1, NKG7, CD74, ANXA1, S100A9, RTKN2, PPBP.

