# AI Programming Foundations Project

## Project Description

This project implements a complete, reproducible data science workflow using the classic Iris flower
dataset. The workflow covers data ingestion, cleaning, exploratory analysis, and visualization, and
is structured to serve as a reusable foundation for future machine learning, deep learning, and
generative AI projects. All steps are modular, documented, and version-controlled with Git.

**Dataset:** Iris Flower Measurements — [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/53/iris)  
150 rows × 5 columns (sepal length, sepal width, petal length, petal width, species)

---

## What You Will Build / What Was Built

- `data_workflow.ipynb` — Jupyter Notebook with the full data workflow
- `module_summary.pdf` — Written report with academic citations
- `requirements.txt` — Reproducibility file listing all package versions
- `README.md` — This file

---

## How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/pgpaologhidoni/ai-programming-foundations-project.git
cd ai-programming-foundations-project
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Open and run the notebook

```bash
jupyter notebook data_workflow.ipynb
```

Run all cells top-to-bottom using **Kernel → Restart & Run All**.

### 4. Regenerate requirements.txt (optional)

```bash
pip freeze > requirements.txt
```

---

## Project Structure

```
ai-programming-foundations-project/
├── data_workflow.ipynb                   # Main analysis notebook
├── iris.csv                              # Dataset
├── figure1_petal_length_distribution.png
├── figure2_sepal_vs_petal.png
├── figure3_correlation_heatmap.png
├── module_summary.pdf                    # Written report with citations
├── requirements.txt
└── README.md
```

---

## Bias Awareness

Poor data cleaning can introduce bias in several ways. In this project:

- **Median imputation for missing values** was chosen over mean imputation because the median is
  robust to outliers. Using the mean could pull imputed values toward extreme observations,
  artificially inflating or deflating class-level averages and misrepresenting the true
  distribution of a species' measurements.
- **Dropping duplicates without inspection** is a potential source of bias if duplicates are
  not random — for example, if a particular species was measured redundantly while another was
  not. In such a case, deduplication would reduce representation unevenly across classes,
  skewing grouped statistics and future model training.
- **Feature selection bias**: focusing only on petal features (as their correlation is high) could
  cause a model to overlook sepal width, which carries independent signal for setosa identification.
- **Sample bias**: the Iris dataset is perfectly balanced (50 samples per species) and was collected
  under controlled conditions. Models trained on it may not generalise to real-world plant surveys
  with unequal sampling or environmental variation.

---

## Future Integration Reflections

### How would this workflow change for a Machine Learning project?

The current workflow ends at exploratory analysis and visualization. In a machine learning context,
the cleaned and explored dataset would feed directly into a training pipeline. Specific additions
would include: encoding the `species` column as a numeric target (label encoding or one-hot),
splitting the data into train/validation/test sets, fitting a classifier (e.g., logistic regression,
random forest, or SVM), and evaluating performance with metrics such as accuracy, precision, recall,
and confusion matrices. The modular cleaning and EDA functions written here can be imported as-is
into that pipeline without modification, which is exactly why reproducible workflow design matters.

### How does this project prepare for neural networks?

Neural networks require well-scaled, numeric input tensors. The cleaning pipeline already ensures
there are no missing values or duplicates — two prerequisites for stable gradient-based training.
The next steps would be feature normalisation (standardisation or min-max scaling) and conversion
of the DataFrame to NumPy arrays or PyTorch/TensorFlow tensors. The EDA correlation analysis
also informs architectural decisions: high feature correlation (e.g., petal length and petal width,
r = 0.96) suggests that a shallow network with a small input layer may be sufficient, or that
dimensionality reduction (PCA) before training could improve convergence.

### What is the potential for agentic automation?

An agentic AI system could automate this entire workflow end-to-end. For example, an agent could
monitor a data source for new CSV uploads, trigger the cleaning pipeline automatically, generate
updated visualizations and summary statistics, flag any anomalies (e.g., sudden appearance of
missing values or distributional drift), and write a natural-language summary of findings. The
modular, function-based design of this notebook makes it straightforward to wrap each stage as
a tool that an agent can call in sequence or in parallel, enabling fully automated, self-correcting
data pipelines with minimal human intervention.

<!-- development branch -->
