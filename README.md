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
| Protein   | log2FC_Mutant_1  | p_value_mutant_1  | log2FC_Mutant_2  | p_value_mutant_2  |
|-----------|----------------|------------------|----------------|------------------|
| Protein 1  | -2.234  | 0.011936301  | -0.034013746  | 0.870449822  |
| Protein 2  | -0.4356 | 0.048117947  | 0.977276688  | 0.006824968  |
| Protein 3  | 4.1234  | 0.030068286  | -0.148552283  | 0.184937661  |
| Protein 4  | 0.2456  | 0.025751486  | 0.007016625  | 0.961535499  |
| Protein 5  | 0.3456  | 0.020128667  | 0.032894575  | 0.761733234  |
| Protein 6  | 4.4567  | 0.044012327  | -0.119952382  | 0.212598854  |
| Protein 7  | 0.82312 | 0.018204593  | 0.396669404  | 0.005511213  |
| Protein 8  | -3.53   | 0.014411964  | 0.168111964  | 0.97312934  |
| Protein 9  | -2.37567| 0.009532262  | 1.166365433  | 0.99997572  |
| Protein 10 | -0.4567 | 0.009608587  | -0.002227916  | 0.050023696  |

 To check the **structure** of your dataset:
```r
str(data)
```
## 📊 Generating a Volcano Plot for Mutant 1
To create a volcano plot for **Mutant 1**, we need to extract the relevant data from the dataset. 
We will create a new object named `mut1` that contains only **Protein, log2FC_Mutant_1, and p_value_mutant_1**.

```r
mut1 <- select(data, protein, log2FC_Mutant_1, p_value_mutant_1)
```

### Explanation:
- `select(data, protein, log2FC_Mutant_1, p_value_mutant_1)`: This function from **dplyr** extracts only the relevant columns needed for plotting.

Now, we generate a volcano plot using `ggplot2`:

```r
ggplot(mut1,
       aes(x=log2FC_Mutant_1,
           y=-log10(p_value_mutant_1))) +
  geom_point()
```

### Explanation of Functions:
- `ggplot(mut1, aes(...))`: Initializes the plot with `mut1` data and defines **aesthetics** (`aes`).
- `x=log2FC_Mutant_1`: The **x-axis** represents the **log2 fold change**, showing the magnitude of change.
- `y=-log10(p_value_mutant_1)`: The **y-axis** represents the **-log10(p-value)**, which helps highlight significant proteins (higher values mean more significant changes).
- `geom_point()`: Adds **scatter points** to create the volcano plot.


### Generating the Updated Volcano Plot using alpha to address overplotting

ggplot(mut1,
       aes(x=log2FC_Mutant_1,
           y=-log10(p_value_mutant_1))) +
  geom_point(alpha=0.3)
  
  - `geom_point(alpha=0.3)`: Reduces overplotting by making points semi-transparent (`alpha=0.3`).

## 🎨 Adding Color to Indicate Significance
To highlight significantly abundant proteins, we will create a **new column** in `mut1` that categorizes proteins based on a **p-value threshold**.

```r
mut1$threshold = as.factor(mut1$p_value_mutant_1 < 0.001)
```

### Explanation:
- `mut1$p_value_mutant_1 < 0.001`: This checks if the p-value is **less than 0.001** (significance threshold).
- `as.factor(...)`: Converts this logical value (`TRUE/FALSE`) into a categorical variable.
- `mut1$threshold`: Stores this new categorical variable in the dataset.

### Viewing the Updated Dataframe
```r
View(mut1)
```

### Generating the Updated Volcano Plot with Color
```r
ggplot(mut1,
       aes(x=log2FC_Mutant_1,
           y=-log10(p_value_mutant_1),
           colour = threshold)) +
  geom_point(alpha=0.3)
```

### Explanation of the Updated Plot:
- `colour = threshold`: Colors the points based on significance (TRUE = significant, FALSE = not significant).
- `geom_point(alpha=0.3)`: Keeps transparency to manage overplotting.


