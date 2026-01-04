# 🧬 Diabetes-Induced Lung Gene Expression Alterations

## 📋 Project Overview
This study investigates **gene expression alterations in lung tissue** of streptozotocin-induced diabetic rats using microarray analysis. The project compares **7 diabetic** versus **5 healthy control** rats to identify differentially expressed genes associated with Type 1 diabetes.

### 🎯 Research Question
Does Type 1 diabetes induce significant gene expression changes in lung tissue, similar to other organs (kidney, liver, heart)?

## 📊 Dataset
- **Source**: PubMed GEO database (Affymetrix microarray data)
- **Sample size**: 12 male Wistar rats
  - 7 diabetic (streptozotocin-induced)
  - 5 healthy controls
- **Platform**: Affymetrix GeneChip
- **Tissue**: Lung cells

## 🔬 Analysis Pipeline

### 1. **Data Import & Quality Control**
- Raw `.CEL` file processing using `affy` package
- Quality assessment with:
  - `affyQCReport` for log intensity distributions
  - `simpleaffy` for array quality metrics
  - Correlation analysis with `MKmisc`

### 2. **Preprocessing & Normalization**
Five preprocessing methods compared:
- **MAS 5.0** (`robloxbioc`)
- **RMA** (`rma`)
- **GCRMA** (`gcrma`)
- **PLIER** (`justPlier`)
- **VSNRMA** (`vsnrma`)

**Selection criteria**:
- Mean-SD plots
- Boxplot distributions
- Array correlation matrices
- Row variance analysis

**Selected method**: **VSNRMA** demonstrated optimal performance for variance stabilization and normalization.

### 3. **Statistical Analysis**
- **Linear modeling** with `limma` package
- **Empirical Bayes moderation** for variance estimation
- **Multiple testing correction** using Benjamini-Hochberg (FDR)
- **Two design approaches**:
  1. Single coefficient for diabetic vs. normal contrast
  2. Separate coefficients with contrast matrix

## 📈 Key Findings

### 🧪 **Gene Expression Changes**
- **Minimal alterations**: Most genes show small expression changes
- **Direction**: Primarily **upregulation** in diabetic samples
- **Magnitude**: Log2 fold changes typically within **±0.8 range**
- **Statistical significance**: All reported genes show adjusted p-values < 0.05

### 📚 **Consistency with Literature**
Results align with published studies showing:
- Approximately **46 genes** with ±1.5-fold changes
- Only **5 genes** with ±2-fold changes
- **1 gene** with +3-fold increase
- Lung tissue shows **less dramatic** changes compared to other organs (kidney, liver)

## 🛠️ Technical Implementation

### 📦 **R Packages Used**
```r
affy, affyQCReport, simpleaffy, MKmisc, arrayQualityMetrics,
RobLoxBioC, gcrma, plier, vsn, genefilter, limma

## 📁 File Structure

Diabetes_Lung_Expression/
├── 3rd.Rmd                    # Main analysis report
├── litdb.bib                  # Bibliography
├── Affymetrix/               # Raw .CEL files
│   ├── Diabetic_1.CEL
│   ├── Diabetic_2.CEL
│   └── ...
├── PreprocessedData.RData    # Normalized datasets
├── FinalData.RData          # Filtered VSNRMA data
└── README.md                # This file

## 🚀 Reproducibility
# Install Dependencies

# Install required packages
install.packages(c("affy", "affyQCReport", "simpleaffy", "MKmisc", 
                   "RobLoxBioC", "gcrma", "plier", "vsn", 
                   "genefilter", "limma", "rmarkdown"))

# Install Bioconductor packages
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install(c("affy", "gcrma", "plier", "vsn", "limma"))

# Run Analysis

# Render the complete report
rmarkdown::render("3rd.Rmd", output_format = "pdf_document")

# Or run chunks interactively
source("3rd.Rmd")

## 📝 Interpretation & Implications
Biological Significance
Lung tissue shows resilience to diabetes-induced transcriptional changes

Minor alterations may explain subclinical pulmonary dysfunction in diabetes

Potential for early biomarker discovery in diabetic lung complications

Clinical Relevance
Understanding organ-specific diabetes effects

Insights into diabetic pulmonary complications

Basis for targeted therapeutic approaches

## ⚠️ Limitations
Small sample size (n=12)

Single time-point analysis

Microarray limitations vs. RNA-seq sensitivity

Species-specific findings (rat → human translation)

## 🔮 Future Directions
Validation with RNA-seq technology

Time-course studies to track progression

Pathway analysis of altered genes

Integration with proteomic/metabolomic data

Human tissue validation studies

# 👨‍🔬 Author
Rezaul Karim Tusar
PhD Candidate in Bioinformatics | MSc Epidemiology
📧 rezaul.tusar.med@gmail.com
🔗 GitHub




