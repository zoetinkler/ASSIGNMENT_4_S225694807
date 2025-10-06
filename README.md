# ASSIGNMENT 4 - R Project

**Author:** Zoe Tinkler - S225694807
**Date:** 6th Oct 2025

---

## Introduction

This repository contains a single R Markdown Script that performs analysis of gene expression, tree growth and biological sequence data.
The R Markdown Script is broken into two parts:

> Note: The HTML output does not show the coding used to create outputs. View the raw .rmd file for coding used.

**Part 1: Gene Expression and Tree Growth Analysis**  
   - Downloads gene expression and tree growth datasets.  
   - Calculates mean gene expression, highest expressed genes, and counts genes expressed less than 10.  
   - Visualises gene expression distribution.  
   - Analyses tree circumferences at two sites (Northeast and Southwest) over time.  
   - Calculates growth over 10 years and performs a t-test to compare sites.  

**Part 2: Biological Sequence Analysis**  
   - Downloads coding sequences (CDS) for *E. coli* and *Bifidobacteriaceae bacterium* WP012.  
   - Calculates total coding DNA lengths and sequence composition.  
   - Translates DNA to protein sequences and calculates amino acid frequencies.  
   - Analyses codon usage between the two organisms.  
   - Analyses k-mer protein sequences between the two organisms.

---

## How to Run the Analysis

1. **Open the R Markdown file** in RStudio.
2. **Knit the document** to HTML. This will:  
   - Download the datasets from GitHub and Ensembl  
   - Process gene expression and tree growth data.  
   - Analyse biological sequences for DNA and protein features, along with codon usage and k-mer representation.  
   - Generate all figures and summary tables.
3. **View the outputs** directly in the knitted html.

## Required:

  **R** 
    R >= 4.3.0
    R Core Team (2025). R: A Language and Environment for Statistical Computing_. R Foundation for Statistical Computing, Vienna, Austria. <https://www.R-project.org/>.

  **Seqinr**  
    Used for Sequence processing and codon usage analysis  
    Charif D, Lobry J (2007). “SeqinR 1.0-2: a contributed package to the R project for statistical computing devoted to biological sequences retrieval and analysis.” In Bastolla U, Porto M, Roman H, Vendruscolo M (eds.), Structural approaches to sequence evolution: Molecules, networks, populations, series Biological and Medical Physics, Biomedical Engineering, 207-232. Springer Verlag, New York. ISBN : 978-3-540-35305-8.

  **R.utils**   
    Used for file utilities   
    Bengtsson H (2025). _R.utils: Various Programming Utilities_. doi:10.32614/CRAN.package.R.utils <https://doi.org/10.32614/CRAN.package.R.utils>, R package version 2.13.0, <https://CRAN.R-project.org/package=R.utils>

  **ggplot2**   
    Used for data visualisation
    Wickham H (2016). ggplot2: Elegant Graphics for Data Analysis_. Springer-Verlag New York. ISBN 978-3-319-24277-4, <https://ggplot2.tidyverse.org>.

---

## Input Files

| Input | Source | Description |
|-------|--------|------------|
| `gene_expression.tsv` | GitHub | RNA-seq count data for three GTEx samples |
| `growth_data.csv` | GitHub | Tree circumference measurements at two sites from 2005 to 2020 |
| `ecoli_cds.fa` | Ensembl | Coding sequences (CDS) for *Escherichia coli* str. K-12 substr. MG1655 str. K12 |
| `bifido_cds.fa` | Ensembl | Coding sequences (CDS) for *Bifidobacteriaceae bacterium* WP012 |

---

## Inputs and Outputs for each Code Chunk

1. `gene_expression download`  
**Purpose:** Download the gene expression dataset from GitHub and save it locally within working directory  
**Inputs:** `gene_expression.tsv` from GitHub.  
**Outputs:** `gene_expression_data` data frame. The first few rows are displayed for checking.  

2. `average_expression`  
**Purpose:** Calculate the mean expression for each gene across all of the samples  
**Inputs:** `gene_expression_data`  
**Outputs:** Updated data frame, table of top 10 genes by mean expression.  

3. `10 genes mean expression`  
**Purpose:** Sort genes by mean expression and read top 10 lines 
**Inputs:** `gene_expression_data`  
**Outputs:** Genes that have the highest expression across samples. 

4. `genes less than 10`  
**Purpose:** Count the number of genes with mean expression of less than 10 and print the result  
**Inputs:** `gene_expression_data`  
**Outputs:** Number of genes with mean expression less than 10.  

5. `gene expression histogram`
**Purpose:** Visualise gene expression distribution.  
**Inputs:** `gene_expression_data$MeanExpression`  
**Outputs:** Histogram figure.  

6. `import tree growth data`
**Purpose:** Load tree growth dataset.  
**Inputs:** `growth_data.csv` from GitHub  
**Outputs:** `growth_data` data frame, first few rows displayed.  

7. `mean and SD at 2 sites`
**Purpose:** Compute mean and standard deviation of tree circumferences at Northeast and Southwest sites.  
**Inputs:** `growth_data`  
**Outputs:** Summary statistics for both sites.  

8. `box plot for tree circumferences`
**Purpose:** Compare tree circumferences between sites over time.  
**Inputs:** `northeast`, `southwest` subsets  
**Outputs:** Boxplot figure showing NE & SW circumferences in 2005 and 2020.  

9. `mean growth 10yr`
**Purpose:** Calculate tree growth over the last 10 years.  
**Inputs:** `northeast`, `southwest` subsets  
**Outputs:** Mean 10-year growth for each site.  

10. `t test results`
**Purpose:** Compare mean growth statistically between sites.  
**Inputs:** 10-year growth data from NE and SW sites  
**Outputs:** Full t-test output and p-value.  

11. `loading packages`
**Purpose:** Load required packages for biological sequence analysis.  
**Inputs:** None  
**Outputs:** Packages loaded into R session.  

12. `download cds files`
**Purpose:** Download and unzip coding sequence FASTA files.  
**Inputs:** Ensembl URLs for E. coli and Bifidobacteriaceae  
**Outputs:** Local FASTA files: `ecoli_cds.fa` and `bifido_cds.fa`.  

13. `cds`
**Purpose:** Read CDS sequences and count them.  
**Inputs:** FASTA files  
**Outputs:** `ecoli_cds`, `bifido_cds` lists and summary table of CDS counts.  

14. `total coding DNA`
**Purpose:** Summarise CDS lengths.  
**Inputs:** `ecoli_cds`, `bifido_cds`  
**Outputs:** table of total number of coding DNA 

15. `total coding DNA boxplot`
**Purpose:** Create a box plot of the total coding DNA of both organisms 
**Inputs:** `ecoli_len`, `bifido_len`  
**Outputs:** Boxplot figure and mean and median of the two organisms CDS lengths

16. `DNA bases`
**Purpose:** Determine nucleotide composition of the first CDS.  
**Inputs:** `ecoli_cds`, `bifido_cds`  
**Outputs:** Base frequency tables and barplot figures.  

17. `protein sequence`
**Purpose:** Translate CDS to protein sequences and summarise amino acids.  
**Inputs:** `ecoli_cds`, `bifido_cds`  
**Outputs:** Amino acid frequency tables and barplots.  

18. `codon usage`
**Purpose:** Calculate codon usage of both organisms for comparison
**Inputs:** `ecoli_dna`, `bifido_dna`
**Outputs:** `ord_codon_usage_table`, `codon_usage_table` data frame for comparison between RSCU values for each organism

19. `codon ggplot`
**Purpose:** Data visualisation of codon usage for each organism
**Inputs:** `ord_codon_usage_table`
**Outputs:** Grouped bar plot made with ggplot 2 which shows codon usage of each AA for both organisms

20. `codon barplot`
**Purpose:** Data visualisation of codon usage for each organism
**Inputs:** `ord_codon_usage_table`
**Outputs:** Grouped bar plot  which shows codon usage of each AA for both organisms when RSCU minus 1
`rscu_matrix`

21. `bifido k-mers`
**Purpose:** Count frequency of k-mers 3-5 length in Bifidobactericeae bacterium
**Inputs:** `bifido_prot`, `all_counts_bifido`
**Outputs:** Top and Bottom 10 Bifidobactericeae k-mers with counts

22. `e. coli k-mers`
**Purpose:** Compare the same k-mers from Bifidobactericeae to k-mers in E. coli
**Inputs:** `ecoli_prot`, `all_counts_bifido`
**Outputs:** Data frame of `kmer_comparison` which compares the same k-mers in both organisms

23. `top k-mer plots`
**Purpose:** Visualisation of overrepresented k-mers in both organisms
**Inputs:** `kmer_comparison``kmer_matrix`
**Outputs:** A plot of the k-mer comparisons counts in each organism.

24. `bottom k-mer plots`
**Purpose:** Visualisation of underrepresented k-mers in both organisms
**Inputs:** `kmer_comparison``kmer_matrix`
**Outputs:** A plot of the k-mer comparisons counts in each organism.
