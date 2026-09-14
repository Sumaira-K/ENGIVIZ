# ENGIVIZ — Netflix Content Analytics & Visualization

A data analysis and visualization project exploring the **Netflix Titles dataset** to uncover patterns in content format, geographic distribution, genre composition, and catalog evolution.

The project combines **Python, Pandas, NumPy, and Matplotlib** to transform raw catalog data into structured analysis and presentation-ready visualizations.

---

## Project Overview

**ENGIVIZ** analyzes **8,807 Netflix titles across 12 attributes** to answer questions such as:

* How has the balance between Movies and TV Shows changed over time?
* Which countries contribute the most content to the Netflix catalog?
* How geographically concentrated or diversified is the catalog?
* Which genre combinations occur most frequently?
* Which individual genres dominate the catalog?
* Which genres commonly appear together?

Rather than focusing only on basic descriptive statistics, the analysis connects multiple dimensions of the dataset to identify broader catalog-level trends.

---

## Key Findings

### 1. Increasing Share of TV Content

Between **2014 and 2021**, the share of TV Shows among newly added titles increased from **20.8% to 33.7%**, representing a **12.9 percentage-point increase**.

The trend was not linear, however, with TV content peaking at 41.0% in 2016 before declining and subsequently increasing again.

### 2. Geographic Diversification

The United States is the largest content-producing country in the dataset with **3,690 country-tags**, followed by India with **1,046**.

At the same time, the combined share of the top five countries decreased from **82.4% in 2014 to 66.1% in 2021**, indicating greater geographic diversification over time.

### 3. Regional Differences in Content Format

The dataset shows significant differences between countries.

For example:

* **India:** 92.0% Movies / 8.0% TV Shows
* **Japan:** 37.4% Movies / 62.6% TV Shows
* **South Korea:** 26.4% Movies / 73.6% TV Shows

This highlights how content composition varies significantly across markets.

### 4. Genre Concentration

The most common individual genre tag is **International Movies**, appearing on **2,752 titles**, followed by **Dramas** with 2,427 titles and **Comedies** with 1,674 titles.

The most frequent exact genre combination is **Dramas, International Movies**, with 362 titles.

### 5. Genre Co-occurrence

The analysis goes beyond simple genre frequency by measuring pairwise genre co-occurrence.

For example, **Dramas and International Movies overlap on 1,483 titles**, substantially higher than their exact-combination count of 362. This demonstrates why pairwise analysis can reveal relationships hidden by simple category-frequency analysis.

---

# Analysis Workflow

```text
Raw Netflix Dataset
        │
        ▼
Data Loading
        │
        ▼
Data Quality Assessment
        │
        ├── Missing Values
        ├── Duplicate Checks
        └── Date Validation
        │
        ▼
Data Transformation
        │
        ├── Country Expansion
        ├── Genre Expansion
        ├── Year Extraction
        └── Genre Combinations
        │
        ▼
Exploratory Data Analysis
        │
        ├── Format Trends
        ├── Geographic Distribution
        ├── Genre Analysis
        └── Genre Co-occurrence
        │
        ▼
Visualization & Insights
```

---

# Dataset

The project uses the **Netflix Titles dataset**, containing:

| Attribute           |           Details |
| ------------------- | ----------------: |
| Records             |             8,807 |
| Columns             |                12 |
| Content Types       | Movies & TV Shows |
| Year Range          |         2008–2021 |
| Unique `show_id`    |             8,807 |
| Unique Genre Tags   |                42 |
| Unique Country Tags |               122 |

The dataset contains information including:

* Show ID
* Type
* Title
* Director
* Cast
* Country
* Date Added
* Release Year
* Rating
* Duration
* Listed-in / Genre
* Description

---

# Data Cleaning & Preparation

The notebook performs several preprocessing and validation steps before analysis.

### Missing-value analysis

Missing values were quantified by both count and percentage.

The largest missing-value categories are:

| Column     | Missing |
| ---------- | ------: |
| Director   |  29.91% |
| Country    |   9.44% |
| Cast       |   9.37% |
| Date Added |   0.11% |
| Rating     |   0.05% |
| Duration   |   0.03% |

### Duplicate validation

The analysis verifies:

* `show_id` uniqueness
* Case-insensitive title duplicates
* Date parsing
* Missing `date_added` values

`show_id` contains **zero duplicates**.

The notebook also identifies six case-insensitive title matches and treats them as potential distinct works rather than automatically removing them.

### Feature transformation

Additional analytical fields are created for:

* Year added
* Month added
* Exploded country values
* Exploded genre values
* Genre combinations

This allows multi-valued categorical fields to be analyzed independently.

---

# Visualizations

The project produces five primary visualizations.

## 1. Netflix Catalog Evolution

Shows the change in Movie vs. TV Show share over time alongside the changing concentration of the top five content-producing countries.
![Uploading image.png…]()



---

## 2. Top Content-Producing Countries

A stacked horizontal bar chart comparing Movie and TV Show contributions across the top 18 countries.



---

## 3. Genre Combinations — Movies vs. TV Shows

Compares the most common genre combinations across Movies and TV Shows.



---

## 4. Most Common Genre Tags

Ranks the 20 most frequently occurring individual genre tags.



---

## 5. Genre Co-occurrence Heatmap

Visualizes pairwise relationships between the top 15 genre categories and identifies which genres frequently occur together.



---

# Technical Stack

| Technology                          | Purpose                              |
| ----------------------------------- | ------------------------------------ |
| **Python**                          | Core analysis                        |
| **Pandas**                          | Data manipulation and transformation |
| **NumPy**                           | Numerical analysis                   |
| **Matplotlib**                      | Data visualization                   |
| **Jupyter Notebook / Google Colab** | Interactive analysis environment     |

---

# Analytical Techniques

The project demonstrates practical data-analysis techniques including:

* Exploratory Data Analysis (EDA)
* Missing-value analysis
* Duplicate detection
* Date parsing and temporal feature extraction
* Multi-label categorical analysis
* DataFrame grouping and aggregation
* Percentage calculations
* Time-series trend analysis
* Country-level comparison
* Genre frequency analysis
* Pairwise co-occurrence analysis
* Correlation-style heatmap visualization
* Insight generation from visual patterns

---

# How to Run

### 1. Clone the repository

```bash
git clone https://github.com/Sumaira-K/ENGIVIZ.git
cd ENGIVIZ
```

### 2. Install dependencies

```bash
pip install pandas numpy matplotlib jupyter
```

### 3. Obtain the dataset

Place:

```text
netflix_titles.csv
```

in the notebook's working directory.

The notebook also includes a Google Colab upload fallback if the CSV is not found locally.

### 4. Run the notebook

```bash
jupyter notebook ENGIVIZ.ipynb
```

Alternatively, open the notebook directly in **Google Colab**.

---

# Reproducibility

The analysis is designed to be reproducible from the source dataset.

The notebook:

1. Loads the raw dataset.
2. Validates data quality.
3. Performs required transformations.
4. Generates analytical tables.
5. Produces the visualizations.
6. Saves the charts into the `charts/` directory.

The analysis also explicitly accounts for the fact that **2021 is a partial year**, since the latest `date_added` value in the dataset is September 25, 2021.

---

# Limitations & Analytical Caveats

The analysis considers several limitations rather than treating the dataset as perfectly complete.

### Partial 2021 data

The dataset ends on **September 25, 2021**, meaning 2021 should not be interpreted as a complete calendar year.

### Multi-country titles

A title associated with multiple countries is counted once for each listed country.

Therefore, country-level totals can exceed the total number of titles.

### Missing country information

Approximately **9.44% of titles have no country information** and are excluded from country-based rankings.

### Genre interpretation

Genre values are multi-label categorical data. Consequently, an individual title can contribute to multiple genre categories.

These considerations are important when interpreting the visualizations and derived insights.

---

# What This Project Demonstrates

ENGIVIZ demonstrates an end-to-end analytical workflow rather than simply plotting predefined charts:

**Data → Cleaning → Transformation → Analysis → Visualization → Interpretation**

Key skills demonstrated:

* Python-based data analysis
* Pandas data manipulation
* Numerical computation with NumPy
* Exploratory Data Analysis
* Multi-dimensional categorical analysis
* Data visualization
* Analytical storytelling
* Data-quality validation
* Reproducible notebook-based workflows

---

# Future Improvements

Potential extensions include:

* Interactive dashboards using **Plotly, Streamlit, or Power BI**
* Additional temporal analysis
* Country-level trend exploration
* Rating and duration analysis
* Director and cast network analysis
* NLP analysis of title descriptions
* Recommendation-system experimentation
* Interactive filtering by country, genre, rating, and release year
* Automated analytical reporting

---

# Author

**Sumaira K**

Computer Science / AI & Data Science

GitHub: [Sumaira-K](https://github.com/Sumaira-K)

---

## Repository

[View the ENGIVIZ repository](https://github.com/Sumaira-K/ENGIVIZ)

---

## License

This project is intended for educational, analytical, and portfolio purposes.
