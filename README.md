# Alzheimer's Disease Gene Expression Analysis

## Project Overview
This project analyzes gene expression data from patients at different stages of Alzheimer's disease. The primary objective is to identify genes that are significantly differentially expressed between different disease stages using a T-test. The final results include lists of significantly altered genes and pathway enrichment analysis to understand biological processes relevant to Alzheimer's progression.

## Objectives
The goal of this analysis is to compare gene expression data across different disease stages:
- **Incipient vs. Moderate Group:** Comparing gene expression data for patients in the incipient stage against those in the moderate stage.
- **Moderate vs. Severe Group:** Comparing gene expression data for patients in the moderate stage against those in the severe stage.

A T-test is used to determine whether the mean gene expression values significantly differ between the baseline and comparison groups. For the first comparison (Incipient vs Moderate) I am using Incipient as my baseline group and Moderate as my comparison group. For the second comparison, I am using the Moderate group as my baseline group and Severe as my comparison group. 

In theory, the t-test will essentially help me either reject or fail to reject the null hypothesis, which in this case would be that both groups (base and comparison) have the same mean, meaning that there is no difference in terms of gene expression between the group of patients in the baseline and comparison groups of each analysis. 

The significantly altered genes are then used for downstream enrichment analysis to identify relevant biological pathways.


## Vision: 
With the short list of pathways at hand, I should be able to do a domain-level research on those pathways to figure out if something can be a significant contribution for understanding of the disease, or that may eventually lead to better treatment possibilities. 

## Methodology
The analysis follows these main steps:

1. **Data Validation & Preprocessing**
   - Ensure correct structure (patients as rows, genes as columns)
   - Identify and subset patient groups based on `DISEASE_STATUS`
   - Normalize and format gene expression data

2. **T-Test Analysis**
   - Prepare matched subsets of clinical and gene expression data
   - Define baseline and comparison groups
   - Run T-tests using `fnTTest.R`
   - Identify genes with significant differential expression (p ≤ 0.01)

3. **Result Analysis & Enrichment Analysis**
   - Extract top 20 significantly altered genes
   - Perform pathway enrichment analysis using EnrichR database and package in R
   - Save results in CSV and multi-tab Excel formats
   - Perform exploratory domain level research on top pathways (see presentation for final findings)

## Repository Structure

```
📂 Differential-Gene-Expression-Analysis-of-Alzheimers-Disease-Patients-
├── 📂 IncipientvsModerate  
│   # Analysis of Incipient vs Moderate Group
│
│   ├── 📂 input  
│   │   # Input Data - some files are copied from the output folder to be read for the enrichment analysis
│   │   ├── 2023-EnrichR-Databases.txt
│   │   ├── Blalock_clin_final.csv
│   │   ├── GSE62232_Blalock_geneexp_final.tsv
│   │   ├── Moderate_Incipient_SigDiffExpressedGenes.csv
│   │   ├── Moderate_Incipient_Ttest_Shortlisted.csv
│   │   ├── TTest__Moderate_(Comp).vs_Incipient_(Base).TTest.csv
│
│   ├── 📂 output  
│   │   # Final output files
│   │   ├── Moderate_Incipient_DEGs.csv
│   │   ├── Moderate_Incipient_EnrichR.xlsx
│   │   ├── TTest__Moderate_(Comp).vs_Incipient_(Base).TTest.csv
│
│   ├── 📂 sanity  
│   │   # Files produced to sanity check data between and before analysis
│   │   ├── ClinBaseIDs.tsv
│   │   ├── ClinCompIDs.tsv
│   │   ├── GeneExpBaseIDs.tsv
│   │   ├── GeneExpCompIDs.tsv
│
│   ├── 📂 src  
│   │   # Reproducible source code with comments for this analysis. Contains baseline vs comparison group analysis and enrichment analysis files
│   │   ├── EnrichAnalysis_IncipientvsModerate.pdf
│   │   ├── EnrichAnalysis_IncipientvsModerate.Rmd
│   │   ├── fnTTest.R
│   │   ├── functionEnrichment.R
│   │   ├── GroupCompAnalysis_IncipientvsModerate.pdf
│   │   ├── GroupCompAnalysis_IncipientvsModerate.Rmd
│
├── 📂 ModeratevsSevere  
│   # Analysis of Moderate vs Severe Group
│
│   ├── 📂 input  
│   │   # Contains raw input files for analysis, and also outputs of step 1 to be used in step 2
│   │   ├── 2023-EnrichR-Databases.txt  # List of databases used for enrichment analysis
│   │   ├── Blalock_clin_final.csv      # Clinical data related to the study
│   │   ├── GSE62232_Blalock_geneexp_final.tsv  # Gene expression dataset
│   │   ├── Severe_Moderate_Ttest_Shortlisted.csv  # Shortlisted significant genes from T-test
│
│   ├── 📂 output  
│   │   # Contains results and processed files
│   │   ├── Severe_Moderate_DEGs.csv  # List of differentially expressed genes
│   │   ├── Severe_Moderate_EnrichR.xlsx  # Enrichment analysis results
│   │   ├── TTest__Severe_(Comp).vs._Moderate_(Base).TTest.csv  # Full T-test results
│
│   ├── 📂 sanity  
│   │   # Contains sanity check files (e.g., IDs used for analysis)
│   │   ├── ClinBaseIDs.tsv      # Clinical IDs for the baseline (moderate group)
│   │   ├── ClinCompIDs.tsv      # Clinical IDs for the comparison (severe group)
│   │   ├── GeneExpBaseIDs.tsv   # Gene expression IDs for the baseline (moderate group)
│   │   ├── GeneExpCompIDs.tsv   # Gene expression IDs for the comparison (severe group)
│
│   ├── 📂 src  
│   │   # Source scripts and documentation for the analysis
│   │   ├── EnrichAnalysis_ModeratevsSevere.pdf  # PDF report of the enrichment analysis
│   │   ├── EnrichAnalysis_ModeratevsSevere.Rmd  # R Markdown script for enrichment analysis
│   │   ├── fnTTest.R  # R function for performing T-tests
│   │   ├── functionEnrichment.R  # R function for enrichment analysis
│   │   ├── GroupCompAnalysis_ModeratevsSevere.nb.html  # HTML report for group comparison analysis
│   │   ├── GroupCompAnalysis_ModeratevsSevere.Rmd  # R Markdown script for group comparison analysis
│
├── README.md  # Project documentation file
├── AlzheimersDiseasePathwaysofInterest.pdf  # Project Presentation and Insights from Analysis

```

## How to Use
### 1. Clone the Repository
To use this project, clone the repository using the following command:
```bash
git clone git@github.com:Tzeene1459/Differential-Gene-Expression-Analysis-of-Alzheimers-Disease-Patients-.git
cd Differential-Gene-Expression-Analysis-of-Alzheimers-Disease-Patients-
```

### 2. Set Up Your Environment
Ensure you have R installed along with required packages:
```r
install.packages(c("tidyverse", "ggplot2", "EnrichR", "readr", "dplyr"))
```

### 3. Run the Analysis
- Execute the scripts in the following order for the Incipient vs Moderate Group:
```r
source("src/GroupCompAnalysis_IncipientvsModerate.Rmd")
source("src/EnrichAnalysis_IncipientvsModerate.Rmd")
```
- Execute the scripts in the following order for the Moderate vs Severe Group:
```r
source("src/GroupCompAnalysis_ModeratevsSevere.Rmd")
source("src/EnrichAnalysis_ModeratevsSevere.Rmd")
```

## Results Interpretation
- The **T-test results** identify genes with significant differential expression.
- The **Enrichment Analysis** provides insights into biological pathways affected in different disease stages.
- Please view the pdf presentation titled "AlzheimersDiseasePathwaysofInterest.pdf" for final findings and insights on the top pathways shortlisted. 

## Contribution
Feel free to contribute by submitting pull requests or opening issues to improve the analysis.

## Author
Tazeen Shaukat 

