# **📌 Volcano Plot - Understanding the Visualization**

A **Volcano Plot** is a scatter plot used to visualize **differential expression** in genomics, proteomics, and transcriptomics studies. It helps identify significantly upregulated and downregulated genes based on statistical significance and fold change.

---

## **🛠️ Plot Axes**
- **X-axis (Log2 Fold Change):** Represents the magnitude of change between conditions.
- **Y-axis (-log10 P-value):** Represents statistical significance, where higher values indicate more significant results.

---

## **🔍 How to Interpret?**
- **⬆️ Upregulated Genes:** (High Log2FC & Low P-value) → Located at the **top-right** of the plot.
- **⬇️ Downregulated Genes:** (Low Log2FC & Low P-value) → Located at the **top-left** of the plot.
- **⚪ Non-significant Genes:** (Low significance) → Found near the **center and bottom** of the plot.

---

# 📌 Volcano Plot in R - Getting Started

## 🚀 Installing Required Packages
To use the Volcano Plot, the following packages should be installed in your R environment.  

If these packages are not installed, use the following code to install them:  

```r
install.packages("ggplot2")
install.packages("dplyr")
```

## 📦 Loading the Required Packages
Once the packages are installed, load them using the following code:

```r
library(dplyr)
library(ggplot2)
```

## 📂 Loading Your Data
### **Note:**  
Make sure your data is in `.csv` format (a type of Excel file).  
If your data is in `.xlsx` format, save it as `.csv` before proceeding.

Let's create an object called `data` (you can use any name for this).  
We will use the `read.csv()` function, which helps load `.csv` files into an R object.

```r
data <- read.csv("file path")
```

### **Important Note on File Paths**
Be careful with file paths!  
- On **Windows**, file paths use `\` (backslash).  
- In R, **you must replace `\` with `/` (forward slash)** when specifying file paths.

#### Example:
```r
data <- read.csv("H:/My_Code_development/250308_Volcano_plots_in_R/Volcano_plots_in_R/Sample_file.csv")
```

## 🔍 Viewing Your Data
Once your data is loaded, you can see the object in your **R Environment**.

To **view** your dataset in RStudio:
```r
View(data)
```
### Example of Data View in R
| Protein   | log2FC  | p_value       | neg_log10_pval |
|-----------|--------|--------------|---------------|
| Protein 1  | -2.234  | 0.011936301  | 2.02313       |
| Protein 2  | -0.4356 | 0.048117947  | 1.417693      |
| Protein 3  | 4.1234  | 0.030068286  | 1.621891      |
| Protein 4  | 0.2456  | 0.025751486  | 1.689198      |
| Protein 5  | 0.3456  | 0.020128667  | 1.796185      |
| Protein 6  | 4.4567  | 0.044012327  | 1.456426      |
| Protein 7  | 0.82312 | 0.018204593  | 1.839819      |
| Protein 8  | -3.53   | 0.014411964  | 1.941277      |
| Protein 9  | -2.37567| 0.009532262  | 2.168936      |
| Protein 10 | -0.4567 | 0.009608587  | 2.165068      |

 To check the **structure** of your dataset:
```r
str(data)
```







## **📂 Files in This Repository**
- 📜 `volcano_plot.R` → Contains the **R script** for generating a volcano plot.
- 🐍 `volcano_plot.py` → Contains the **Python script** for generating a volcano plot.

---

## **📢 Contributions**
🚀 If you want to improve or add more features, feel free to **open a pull request!**
