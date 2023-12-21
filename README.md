# Navigating Spatial Transcriptomics: A Step-by-Step Guide with Visium 10XGenomics
## Introductory Concepts & Spatial Transcriptomics Background ##
Spatial transcriptomics is a cutting-edge technique that enhances traditional transcriptomics by adding a spatial dimension to gene expression analysis. Unlike conventional methods that can lose spatial context, spatial transcriptomics combines high-throughput RNA sequencing with histological imaging to map transcripts back to their original locations in a tissue sample. This is particularly useful in complex studies such as cancer research, where spatial organization of cells is crucial. Platforms like Visium 10X are commonly employed for this, offering high-resolution, genome-wide expression profiles. By leveraging this technique, researchers can gain unparalleled insights into tissue microenvironments, cell-cell interactions, and other aspects that necessitate a spatially resolved understanding of gene expression.

## Analytical Procedures: Detailed Steps for Analysis ##

In this process, the fundamental element of the analysis relies on the data format employed in the #SpatialExperiment (). Below, you can observe the data's structure, which will be utilized in different analyses. 
By using this class, we can store data at the point of analysis, such as data from sequencing platforms (e.g. 10x Genomics Visium) at the point of analysis.

![SpatialExperiment_Data_Structure](https://github.com/Pedramto89/Spatial-Transcriptomics-Data-Analysis/assets/85902042/a9848d3a-8cda-4708-b75b-2e9ac47cc791)

The entire pipeline and codes, due to be available in a separate R Markdown file, are currently delayed and will be revealed after the method's publication, in compliance with data privacy considerations. This delay is attributed to the development of novel approaches in cell type annotation for spatial transcriptomics data. These approaches are expected to introduce new perspectives in manual annotation and the combined use of machine learning algorithms, and their details will be shared post-publication to maintain data confidentiality.

#### 1- Load Data

Spatial transcriptomics data can be analyzed using multiple software packages available on the benchmark, including Seurat, Scanpy, and Giotto. In this workflow, instructions are based on the Seurat package in R. 
Initially, specifying the directory where the data resides is necessary for loading it via Seurat:

<pre>
```R
slice <- "PDAC-9137-A"
root_dir <- "~/Documents/Visium/outs/"
setwd(root_dir)

obj <- Load10X_Spatial(
  data.dir = root_dir,
  filename = "filtered_feature_bc_matrix.h5",
  assay = "Spatial",
  slice = "slice1",
  filter.matrix = TRUE,
  to.upper = FALSE,
  image = NULL
)
```
</pre>

#### 2- Quality Control

Following this, both the features and counts within the sample can be visualized to better understand the data and to eliminate mitochondrial genes.

<pre>
```R
plot1 <- VlnPlot(obj, features = "nCount_Spatial", pt.size = 0.1) + NoLegend()
plot2 <- SpatialFeaturePlot(obj, features = "nCount_Spatial") + theme(legend.position = "right")
wrap_plots(plot1, plot2)


# In the default setting, it's assumed that the sample is of human origin. To visualize the features and counts, this helps to get a grasp of the data and allows for the removal of mitochondrial genes. If dealing with a rat sample, uncomment and use the corresponding code.
  
obj[["percent.mt"]] <- PercentageFeatureSet(obj, pattern = "^MT-")

#obj[["percent.mt"]] <- PercentageFeatureSet(obj, pattern = "^Mt-")  # for rat
```
</pre>
  
#### 3- Normalization

In this spatial transcriptomics analysis, SCTransform is utilized as an advanced normalization method within Seurat, recognized for its superior capabilities in managing technical noise and biological variability compared to the NormalizeData function. Through regularized negative binomial regression, technical variance is effectively stabilized across features. Not only is correction for sequencing depth achieved, but the influence of unwanted technical factors is also mitigated, while biological heterogeneity is preserved. With the application of SCTransform, more accurate feature selection and enhanced detection of subtle biological signals are facilitated, providing a robust foundation for subsequent analyses such as clustering and differential expression studies.


#### 4- Feature Selection
#### 5- Dimensionality Reduction
#### 6- Clustering
#### 7- Spot Deconvolution
#### 8- Differential Expression
#### 9- Multiple Samples Integration
#### 10- Spatial Enrichment Analysis: Evaluating cell-to-cell proximity




## Supplementary Material: Additional Resources, Credits, and Citations ##





