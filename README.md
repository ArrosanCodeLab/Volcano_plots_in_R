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

## **📊 Example Volcano Plot**
You can generate a Volcano Plot using **R (`ggplot2`)** or **Python (`matplotlib`)**.

### **📌 R Code Example (Using ggplot2)**
```r
# Load required libraries
library(ggplot2)

# Simulated Data
set.seed(42)
gene_names <- paste0("Gene", 1:500)
log2FC <- rnorm(500, mean=0, sd=2)  # Simulated log2 fold changes
p_values <- runif(500, min=0.0001, max=1)  # Simulated p-values

df <- data.frame(Gene = gene_names, log2FC = log2FC, p_value = p_values)
df$neg_log10_pval <- -log10(df$p_value)

df$Significance <- ifelse(df$p_value < 0.05 & abs(df$log2FC) > 1, "Significant", "Not Significant")

# Volcano Plot
ggplot(df, aes(x = log2FC, y = neg_log10_pval, color = Significance)) +
  geom_point(alpha = 0.7) +
  scale_color_manual(values = c("red", "black")) +
  theme_minimal() +
  xlab("Log2 Fold Change") +
  ylab("-log10 P-value") +
  ggtitle("Volcano Plot of Simulated Data")
```

### **📌 Python Code Example (Using Matplotlib & Pandas)**
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Simulated Data
np.random.seed(42)
genes = ["Gene" + str(i) for i in range(1, 501)]
log2FC = np.random.normal(0, 2, 500)  # Simulated log2 fold change
p_values = np.random.uniform(0.0001, 1, 500)  # Simulated p-values
neg_log10_pval = -np.log10(p_values)

df = pd.DataFrame({"Gene": genes, "log2FC": log2FC, "p_value": p_values, "neg_log10_pval": neg_log10_pval})
df["Significance"] = np.where((df["p_value"] < 0.05) & (abs(df["log2FC"]) > 1), "Significant", "Not Significant")

# Volcano Plot
plt.figure(figsize=(8, 6))
plt.scatter(df["log2FC"], df["neg_log10_pval"], c=df["Significance"].map({"Significant": "red", "Not Significant": "black"}), alpha=0.7)
plt.axhline(-np.log10(0.05), linestyle='--', color='blue', label='p = 0.05')
plt.xlabel("Log2 Fold Change")
plt.ylabel("-log10 P-value")
plt.title("Volcano Plot of Simulated Data")
plt.legend()
plt.show()
```

---

## **📂 Files in This Repository**
- 📜 `volcano_plot.R` → Contains the **R script** for generating a volcano plot.
- 🐍 `volcano_plot.py` → Contains the **Python script** for generating a volcano plot.

---

## **📢 Contributions**
🚀 If you want to improve or add more features, feel free to **open a pull request!**
