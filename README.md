
# PROJECT TITLE: Differential Gene Expression Analysis 

## PROJECT SUMMARY:
This project performs statistical differential expression analysis using real-world gene expression data from breast cancer tissue and paired adjacent normal tissue. The objective is to identify genes that are significantly expressed differently between the two conditions and visualize the differences using bioinformatics plots such as volcano plot, hierarchical clustering heatmap, and expression boxplots.

* * * * *

DATASET INFORMATION
-------------------

Source: Gene Expression Omnibus (NCBI GEO)\
Accession ID: GSE15852\
Platform: Affymetrix Human Genome U133A Array\
Samples: 86 total (43 breast cancer tissue, 43 adjacent normal tissue)\
Organism: Homo sapiens (human)

Dataset Type: Microarray gene expression matrix\
Data Files Used:
- Series matrix file (expression matrix)
- Metadata (sample annotations such as case vs normal)

* * * * *

PROJECT GOAL
------------

Identify genes that show statistically significant differential expression between breast cancer tissue and paired adjacent normal samples using statistical testing, false-discovery-rate correction, and biological interpretation.

No machine learning models are used; this project focuses on core data science responsibilities:

- Data acquisition
- Data preprocessing
- Statistical testing
- Feature identification
- Visualization and insight reporting

* * * * *

WORKFLOW / METHODOLOGY
----------------------

1.  DATA ACQUISITION

    -   Dataset downloaded from GEO using the GEOparse Python library.

    -   Expression matrix and metadata extracted into pandas DataFrames.

2.  PREPROCESSING

    -   Handled missing values using median imputation per probe.

    -   Log transformation applied: log2(value + 1)

    -   StandardScaler applied only for visualization (PCA, heatmap); statistical testing done on log2 values.

3.  STATISTICAL TESTING

    -   Independent t-test performed for each gene to compare mean expression between Cancer and Normal groups.

    -   Computed p-value and log2 fold change (Cancer minus Normal).

    -   p-value adjustment performed using Benjamini-Hochberg FDR correction (multiple testing correction).

4.  GENE ANNOTATION

    -   Affymetrix probe IDs mapped to official gene symbols using platform annotation table.

    -   In case of multiple probes mapping to the same gene, the probe with lowest adjusted p-value was retained.

5.  FEATURE SELECTION

    -   Significant genes defined using adjusted p-value (FDR) < 0.05.

    -   Top genes selected based on smallest adjusted p-value and highest magnitude log2 fold change.

6.  VISUALIZATION

    -   Volcano plot showing fold change vs. statistical significance.

    -   Boxplots comparing expression values of top genes across cancer vs. normal.

    -   Hierarchical heatmap (Top 50 genes) showing clustering pattern of samples.

* * * * *

KEY RESULTS
-----------

Significant genes identified after FDR correction.

Top statistically significant genes:

1.  ESR1 (Estrogen Receptor 1)
    - log2 Fold Change: +2.10
    - Adjusted p-value: 3.8 × 10⁻¹⁴

2.  COL11A1 (Collagen Type XI Alpha 1 Chain)
    - log2 Fold Change: +3.01
    - Adjusted p-value: 1.2 × 10⁻¹³

3.  MMP11 (Matrix Metallopeptidase 11)
    - log2 Fold Change: +4.10
    - Adjusted p-value: 2.9 × 10⁻¹²

These genes are widely cited in cancer literature and known to be associated with tumor invasiveness, estrogen signaling, and extracellular matrix remodeling.

* * * * *

VISUAL OUTPUTS
--------------

Generated plots:
- Volcano plot (highlights genes with largest fold change and smallest p-values)
- Boxplots (for the top most significant genes)
- Hierarchical clustering heatmap (Top 50 genes clearly separate cancer from normal samples)

* * * * *

TECH STACK
----------

Programming Environment: Python (Google Colab / Jupyter Notebook)

Libraries Used:
- GEOparse -- dataset acquisition via NCBI GEO
- NumPy, Pandas -- data wrangling and transformations
- SciPy -- statistical hypothesis testing (t-test)
- Statsmodels -- FDR multiple testing correction
- Scikit-learn -- scaling and PCA
- Matplotlib, Seaborn -- visualization

* * * * *

PROJECT STRUCTURE
-----------------

gene-expression-analysis-gse15852/\
│\
├── notebooks/\
│ gene_expression_analysis.ipynb\
├── data/\
│   GSE15852_final_significant_genes_with_symbols.csv\
|   GSE15852_family.soft.gz\
|   significant_genes_GSE15852.csv\
├── plots/\
│ volcano_plot.png\
│ heatmap_top50.png\
│ boxplots.png\
└── README (this file)

* * * * *

CONCLUSION
----------

- Gene expression profiles alone are sufficient to separate cancer from normal tissue.
- Statistically significant genes such as ESR1, COL11A1, and MMP11 match previously published breast cancer biomarker studies.
- This project demonstrates proficiency in preprocessing, statistical feature selection, and biological interpretation of high-dimensional gene expression data.

* * * * *

END OF FILE
===========
