# Engineering of Data Analysis — Nova SBE (2024/25)

> **Course:** Engineering of Data Analysis | Nova School of Business & Economics
> **Authors:** Francisco Costa · Drey Tengan

---

## Overview

This repository contains two pair assignments from the Engineering of Data Analysis course at Nova SBE. The work spans two core themes in modern data engineering: **big data processing at scale** and **privacy-preserving data analysis**. Each assignment applies these concepts to real-world datasets, benchmarking different tools and frameworks across performance, scalability, and data utility trade-offs.

---

## Assignment 1 — Big Data Processing & Scalable Analytics

### Business Context
Based on the [ACM DEBS 2015 Grand Challenge](http://www.debs2015.org/call-grand-challenge.html), this assignment used NYC taxi trip data to explore how different data processing frameworks handle large-scale analytical workloads. The goal was to benchmark performance across frameworks and understand when to use each tool.

### Research Questions
- How do Pandas, Spark, and GPU-accelerated cuDF compare in processing speed at different data scales?
- What is the performance cost of Python UDFs in Spark SQL?
- How can clustering be used to optimise real-world infrastructure decisions (e.g. taxi rank placement)?

### Key Results

| Framework | Small Dataset (135MB) | Large Dataset |
|-----------|----------------------|---------------|
| Pandas | 8.36s | ❌ Crashed (RAM exceeded) |
| Spark Pandas API | 20.20s | 1459.86s |
| Spark SQL | 8.35s | 560.39s |
| **cuDF (GPU)** | **2.64s** | **9.26s** |

- **cuDF (GPU) was 3× faster than Pandas** on the small dataset and the only framework that could handle the large dataset without crashing
- **Python UDFs in Spark added ~40% overhead** vs pure Spark SQL expressions (10.77s vs 7.67s) — highlighting the importance of avoiding UDFs in production pipelines
- **Spark SQL** emerged as the best balance between scalability and familiarity for large datasets where Pandas fails
- **K-Means clustering** (scikit-learn, cuML, Spark MLlib) used to identify optimal taxi rank locations — cuML was fastest (2.22s vs scikit-learn 6.19s vs Spark MLlib 44.76s)

### Exercises Covered
1. **Simple statistics benchmark** — Total revenue per taxi licence across Pandas, Spark Pandas API, Spark SQL, and cuDF
2. **UDF performance impact** — Comparing Python UDFs vs native Spark SQL for heatmap grid calculations
3. **Route analysis** — Top 20 most frequent NYC taxi routes above a distance threshold, using Spark SQL and Spark Pandas API
4. **Taxi rank optimisation** — K-Means clustering to identify optimal taxi stand locations, benchmarked across scikit-learn, cuML, and Spark MLlib

### Technologies Used

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?style=flat&logo=apachespark&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![cuDF](https://img.shields.io/badge/cuDF%20(RAPIDS)-76B900?style=flat&logo=nvidia&logoColor=white)
![cuML](https://img.shields.io/badge/cuML%20(RAPIDS)-76B900?style=flat&logo=nvidia&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=flat&logo=googlecolab&logoColor=white)

---

## Assignment 2 — Data Privacy & Anonymisation

### Business Context
As data-driven organisations collect increasingly sensitive information, ensuring privacy while preserving analytical utility is a critical challenge. This assignment explored how anonymisation techniques affect the quality of statistical and machine learning results, using health and demographic datasets.

### Research Questions
- How does k-anonymisation affect statistical utility compared to the original data?
- Does workload-aware anonymisation preserve data quality better than standard anonymisation?
- How does differential privacy impact regression and clustering results?

### Key Results
- **Standard k-anonymisation** significantly degraded statistical distributions compared to the original dataset
- **Workload-aware anonymisation** preserved query-relevant attributes much more effectively — demonstrating that tailoring privacy to the analytical task reduces utility loss
- **Differential privacy (Laplace mechanism)** maintained reasonable regression performance for the Life Expectancy dataset, with the trade-off depending on the privacy budget (ε)
- **Differentially private regression** outperformed the anonymised dataset in preserving correlations between Adult Mortality and Life Expectancy
- Applying differential privacy to clustering (Exercise 4) showed measurable but manageable degradation — highlighting the viability of privacy-preserving ML in clinical contexts

### Exercises Covered
1. **Local vs remote file access** — Benchmarking Pandas, Spark SQL, and cuDF for reading local vs remote datasets
2. **K-anonymisation & workload-aware anonymisation** — Applied to a heart disease dataset; comparing statistical utility before and after anonymisation
3. **Differential privacy for regression** — Life Expectancy dataset anonymised using Laplace mechanism and differentially private regression; compared against workload-aware k-anonymisation
4. **Differential privacy for ML** — Extending ML techniques from a previous course to anonymised clinical data; evaluating how privacy-preserving transformations affect clustering performance

### Technologies Used

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?style=flat&logo=apachespark&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![IBM Differential Privacy](https://img.shields.io/badge/IBM%20Diffprivlib-054ADA?style=flat)
![Anonymity API](https://img.shields.io/badge/Anonymity%20API-555555?style=flat)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=flat&logo=googlecolab&logoColor=white)

---

## Skills Demonstrated

- **Big Data Processing** — Benchmarking Pandas, Spark SQL, Spark Pandas API, and GPU-accelerated cuDF across different dataset scales
- **Distributed Computing** — Writing and optimising Spark SQL queries; understanding when Spark outperforms single-node frameworks
- **GPU-Accelerated Analytics** — Using RAPIDS (cuDF, cuML) for dramatically faster data processing and clustering
- **Data Privacy & Anonymisation** — Implementing k-anonymisation, workload-aware anonymisation, and differential privacy
- **Privacy-Utility Trade-off Analysis** — Quantifying how anonymisation degrades statistical and ML results
- **Geospatial Analysis** — Grid-based coordinate transformations and heatmap visualisation for NYC taxi data
- **Clustering** — K-Means across scikit-learn, cuML, and Spark MLlib for infrastructure optimisation

---

## Files

| File | Description |
|------|-------------|
| `EoDA_2425_assignment1.ipynb` | Big data processing & scalable analytics |
| `EoDA_2425_assignment2.ipynb` | Data privacy, anonymisation & differential privacy |

---

## Datasets

- **NYC Taxi Trip Data** (ACM DEBS 2015 Grand Challenge) — available via [Google Drive](https://drive.google.com/drive/folders/1WMwLUj0t4Q0GSll96lbF2bDjaPVh1w8z)
- **Heart Disease Dataset** — provided through the course
- **Life Expectancy Dataset** — [Kaggle](https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who)

---

## How to Run

1. Clone this repository
   ```bash
   git clone https://github.com/franciscosta/engineering-of-data-analysis.git
   ```
2. Open either notebook in [Google Colab](https://colab.research.google.com/) with a GPU runtime enabled (required for cuDF/cuML exercises)
3. Follow the setup cells at the top of each notebook to configure Spark, Pandas, and cuDF
4. Add the datasets to your Google Drive using the links above

---

## Course

Engineering of Data Analysis — Nova School of Business & Economics, 2024/25
