# BioStudio method research: Bulk RNA-seq, scRNA-seq, Spatial transcriptomics

This document maps three key biology analysis methods to:
- who uses them,
- what they actually work on,
- which files are involved,
- how the method is usually executed,
- and why the workflow matters.

The goal is to make these methods easier to translate into realistic user workflows, product requirements, and analysis support features.

---

## 1. Bulk RNA-seq

### Working pipeline

Biological question and study design  
↓  
Sample collection and RNA extraction  
↓  
Library preparation and sequencing  
↓  
Raw read QC and alignment / quantification  
↓  
Count matrix generation and normalization  
↓  
Differential expression and pathway analysis  
↓  
Biological interpretation, validation planning, and report generation

### 1. Who are the users using this method?

- Transcriptomics scientist
- Disease biology scientist
- Translational scientist
- Biomarker discovery scientist
- Bioinformatics scientist supporting RNA studies
- Wet-lab biologist reviewing expression changes across conditions

### 2. What do they actually work on in this method?

- Comparing gene expression between conditions such as disease vs control, treated vs untreated, responder vs non-responder
- Identifying differentially expressed genes
- Investigating pathway activation or suppression
- Validating whether a biological perturbation changed transcriptional state
- Generating candidate biomarkers from tissue- or cohort-level expression profiles
- Summarizing sample-level molecular differences for downstream interpretation

### 3. Which files are included in this method?

Common input files:
- FASTQ files for raw sequencing reads
- Sample sheet / sample metadata table
- Reference genome files
- Gene annotation files such as GTF/GFF
- Alignment or quantification outputs such as BAM, counts matrix, transcript abundance tables

Common analysis files:
- Count matrix
- Normalized expression matrix
- Differential expression result table
- Pathway or enrichment result files
- QC metrics tables

Common support files:
- Study design document
- Contrast definition table
- Notebook or script files
- Figures and report outputs

### 4. How to do this method

Typical workflow:
1. Define the biological comparison and sample groups before sequencing.
2. Extract RNA, prepare libraries, and sequence the samples.
3. Run raw read QC to identify low-quality reads, adapter issues, or batch problems.
4. Align reads to a reference genome or perform transcript quantification.
5. Build a gene-by-sample count matrix.
6. Normalize counts and inspect sample relationships using PCA, clustering, or correlation plots.
7. Run differential expression analysis between predefined groups.
8. Perform enrichment or pathway analysis on significant gene sets.
9. Interpret the results in the context of phenotype, treatment, or disease biology.
10. Select findings for follow-up validation such as qPCR, protein assays, or functional experiments.

### 5. Why do they do this method?

Pain points:
- Raw RNA-seq processing has many steps and many intermediate files.
- Scientists often struggle to keep metadata, contrasts, and sample labels consistent.
- Reproducibility is hard when different people use different scripts or environments.
- Biologists often need interpretable outputs, not just count tables.

Insights gained:
- Which genes change between conditions
- Which pathways or biological programs are shifted
- Whether an intervention changed global transcriptional behavior
- Which candidate markers are worth follow-up validation

Why this matters for product design:
- Bulk RNA-seq workflows need clean metadata handling, reproducible processing, contrast definition, and outputs that are understandable to both bioinformaticians and bench scientists.

---

## 2. Single-cell RNA sequencing (scRNA-seq)

### Working pipeline

Biological question about cellular heterogeneity  
↓  
Single-cell suspension preparation and library generation  
↓  
Sequencing and matrix generation  
↓  
Cell-level QC, filtering, and normalization  
↓  
Dimensionality reduction and clustering  
↓  
Cell type annotation and marker discovery  
↓  
Comparative analysis, trajectory/interaction analysis, and interpretation

### 1. Who are the users using this method?

- Single-cell scientist
- Single-cell immunology scientist
- Tumor microenvironment scientist
- Cell atlas scientist
- Translational scientist working on cellular heterogeneity
- Computational biologist supporting single-cell studies

### 2. What do they actually work on in this method?

- Resolving cellular heterogeneity inside a tissue or sample set
- Identifying cell populations and subpopulations
- Annotating immune, stromal, malignant, or rare cell types
- Comparing cell state shifts across conditions
- Finding marker genes for clusters or cell states
- Studying lineage, differentiation, activation, or trajectory changes
- Measuring compositional changes between cohorts

### 3. Which files are included in this method?

Common input files:
- Raw FASTQ files from single-cell libraries
- Cell Ranger or equivalent output folders
- Filtered feature-barcode matrix
- Raw count matrix
- Cell metadata table
- Sample metadata table
- Reference transcriptome files

Common analysis files:
- AnnData `.h5ad`
- Seurat `.rds`
- Cluster assignment table
- Cell annotation table
- Marker gene tables
- Differential expression tables
- UMAP / t-SNE coordinate tables

Common support files:
- Doublet detection outputs
- QC threshold settings
- Notebook or script files
- Plot images and summary reports

### 4. How to do this method

Typical workflow:
1. Define the biological question, tissue source, and sampling design.
2. Generate a viable single-cell suspension or nuclei preparation.
3. Prepare single-cell libraries and sequence them.
4. Generate count matrices with platform-specific preprocessing tools.
5. Filter low-quality cells, doublets, and technical artifacts.
6. Normalize the data and select informative genes.
7. Run PCA/UMAP and cluster cells into populations.
8. Identify marker genes and annotate clusters into cell types or states.
9. Compare composition and expression across conditions or cohorts.
10. Optionally perform trajectory, pseudobulk, or cell-cell communication analysis.
11. Interpret the results with domain experts and plan orthogonal validation if needed.

### 5. Why do they do this method?

Pain points:
- Single-cell data is noisy, sparse, and parameter-sensitive.
- Cell annotation often requires many iterative decisions.
- Teams need to keep track of multiple versions of annotated objects.
- Results are hard to communicate if only matrices are available.

Insights gained:
- Which cell types exist in the sample
- Which rare or disease-relevant subpopulations emerge
- How cell states shift under treatment or disease
- Which markers best define meaningful biological groups

Why this matters for product design:
- scRNA-seq workflows are iterative and interpretation-heavy, so users need support for object versioning, annotation tracking, parameter transparency, and interactive visualization.

---

## 3. Spatial transcriptomics

### Working pipeline

Biological question about tissue architecture and localization  
↓  
Tissue section preparation, imaging, and assay capture  
↓  
Sequencing / signal extraction and spatial matrix generation  
↓  
Image alignment, QC, and region annotation  
↓  
Spatial expression analysis and neighborhood analysis  
↓  
Integration with pathology or single-cell references  
↓  
Biological interpretation of tissue organization and local interactions

### 1. Who are the users using this method?

- Spatial biology scientist
- Tissue biology scientist
- Tumor microenvironment scientist
- Translational pathology scientist
- Biomarker scientist studying tissue localization
- Computational scientist supporting spatial transcriptomics studies

### 2. What do they actually work on in this method?

- Understanding where cell types or gene programs are located inside tissue
- Comparing regions such as tumor core, invasive margin, stroma, or immune niches
- Linking tissue morphology with expression patterns
- Identifying spatially variable genes
- Studying cell neighborhoods and local interactions
- Interpreting microenvironment architecture in disease tissue

### 3. Which files are included in this method?

Common input files:
- Spatial count matrix
- Spot or cell barcode table
- Tissue image files
- Slide image metadata
- Spatial coordinates file
- Sample metadata table
- Region annotation masks or segmentation outputs

Common analysis files:
- Spatial object files such as `.h5ad`, `.rds`, or platform-specific outputs
- Region labels
- Cell type deconvolution outputs
- Spatially variable gene tables
- Neighborhood or proximity analysis tables
- Overlay plots and tissue maps

Common support files:
- Histology images
- Annotation files from pathologists or scientists
- Notebook or script files
- Figure panels and summary reports

### 4. How to do this method

Typical workflow:
1. Define the tissue-level biological question and select the appropriate assay/platform.
2. Prepare tissue sections and capture both morphology and molecular measurements.
3. Generate spatial count data together with coordinates and imaging assets.
4. Perform QC on tissue coverage, capture performance, and image alignment.
5. Map expression values onto tissue coordinates.
6. Annotate tissue regions manually or with pathology/computational support.
7. Identify spatially variable genes, region-specific programs, or neighborhood structures.
8. Integrate with single-cell references when finer cell type interpretation is needed.
9. Interpret how spatial organization relates to disease state, mechanism, or response.
10. Choose candidate regions, markers, or hypotheses for downstream validation.

### 5. Why do they do this method?

Pain points:
- Spatial analysis combines molecular data with image assets, which makes file handling more complex.
- Scientists need both quantitative outputs and interpretable tissue views.
- Region annotation and tissue interpretation are often iterative and collaborative.
- Spatial workflows are harder to standardize than bulk-only studies.

Insights gained:
- Where important genes or programs are expressed in tissue
- Which regions contain distinct biological states
- How tissue organization changes with disease or treatment
- Which local cell neighborhoods may explain mechanism or response

Why this matters for product design:
- Spatial transcriptomics requires coordinated handling of molecular data, large images, region annotations, and interpretation workflows across multiple collaborators.

---

## Cross-method comparison

| Method | Main biological resolution | Main analysis focus | Typical output |
| --- | --- | --- | --- |
| Bulk RNA-seq | Sample level | Differential expression across groups | DE genes, pathway results, sample-level plots |
| scRNA-seq | Single-cell level | Cell type/state heterogeneity | Clusters, annotations, markers, trajectory/cell-state outputs |
| Spatial transcriptomics | Tissue location level | Localization and neighborhood context | Tissue maps, regional programs, spatial interactions |

## Notes on terminology

- `Bulk RNA-seq` is the standard term.
- `scRNA-seq` is more standard than `Sc-RNA-seq`.
- `Spatial` is too broad by itself. For transcriptomics use cases, `Spatial transcriptomics` is the clearer term. If the scope later includes protein or multi-modal imaging assays, `Spatial omics` may be a better umbrella term.

#bioturing #biostudio #research #bulk-rnaseq #scrnaseq #spatial-transcriptomics #workflow #persona
