# Experiment 4: Data Wrangling and Data Visualization

**Name:** Guinto, Nyle Justine C.

**Section:** 2ECE-A

---

## 📑 Table of Contents
*   [Short Description](#-short-description)
*   [Project Overview](#-project-overview)
*   [DataFrame Operations Summary](#-dataframe-operations-summary)
*   [Problem Specifications & Solutions](#-problem-specifications--solutions)
*   [Project File Structure](#-project-file-structure)
*   [Prerequisites & Requirements](#-prerequisites--requirements)
*   [How to Run](#-how-to-run)

---

## 🔗 Short Description

A Pandas lab assignment demonstrating DataFrame filtering using categorical and numerical conditions, constructing focused DataFrames, and communicating data comparisons using clear and correctly labeled plots.

---

## 🔎 Project Overview

This project contains Python solutions for data wrangling and visualization using the `pandas` and `matplotlib` libraries. The tasks demonstrate data manipulation concepts including:

*   Filtering tabular data using several categorical and numerical conditions.
*   Constructing focused DataFrames by selecting relevant features.
*   Summarizing the relationship between categorical features and a numerical variable.
*   Communicating a data comparison using clear and correctly labeled plots.

---

## ⚙️ DataFrame Operations Summary

| Task | Target Output Variable | Key Pandas Operations | Key Logic |
| :--- | :--- | :--- | :--- |
| **A. Visayas Communication** | `VisComm` | `[]` (Boolean Indexing) | Filters the dataset for students whose `Hometown` is Visayas and `Track` is Communication, retaining specific columns. |
| **B. Visayas Female** | `VisFemale` | `[]` (Boolean Indexing) | Filters the dataset for students whose `Hometown` is Visayas and `Gender` is Female, retaining specific columns, and further filtering for `Average >= 60` without overwriting. |
| **C. Category-Average** | `track_mean`, `gender_mean`, `hometown_mean` | `.groupby()`, `.mean()`, `plt.bar()` | Computes the mean `Average` for every category within `Track`, `Gender`, and `Hometown` using `.groupby()`. Visualizes these means using `matplotlib` bar charts. |

---

## 📝 Problem Specifications & Solutions

This section covers the core tasks of the experiment, demonstrating various Pandas data extraction and matplotlib visualization techniques:

*   **A. Visayas Communication DataFrame:** Computes the overall `Average` across subjects, then uses Boolean indexing `(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')` to filter the data before column selection.
*   **B. Visayas Female DataFrame:** Uses Boolean indexing `(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')` to create the DataFrame, and filters rows where `Average >= 60` on the fly without overwriting `VisFemale`.
*   **C. Category-Average Visualization:** Uses `.groupby()` to aggregate the data and calculate the mean for each category. Creates a figure with three subplots using `plt.subplots(1, 3)` to display the bar charts.

```python
import pandas as pd
import matplotlib.pyplot as plt

# Load the dataset
df = pd.read_csv('board2.csv')

# Calculate the Average of the 4 subjects if not already present in the source CSV
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

# ---------------------------------------------------------
# A. VISAYAS COMMUNICATION DATAFRAME
# ---------------------------------------------------------
# Apply filtering conditions before column selection
VisComm = df[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')]

# Retain and order specified columns
VisComm = VisComm[['Name', 'Gender', 'Math', 'Electronics', 'Average']]

# Display the resulting DataFrame and its number of rows
display(VisComm)
print(f"Number of rows: {len(VisComm)}")

# ---------------------------------------------------------
# B. VISAYAS FEMALE DATAFRAME
# ---------------------------------------------------------
# Filter for Visayas and Female
VisFemale = df[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')]

# Retain specified columns
VisFemale = VisFemale[['Name', 'Track', 'GEAS', 'Electronics', 'Average']]

# Display the VisFemale DataFrame
print("Visayas Female DataFrame:")
display(VisFemale)

# Display rows where Average is at least 60 without overwriting the original DataFrame
print("\nVisayas Female DataFrame (Average >= 60):")
display(VisFemale[VisFemale['Average'] >= 60])

# ---------------------------------------------------------
# C. CATEGORY-AVERAGE VISUALIZATION
# ---------------------------------------------------------
# a. Compute the mean of Average for every category
track_mean = df.groupby('Track')['Average'].mean().reset_index()
gender_mean = df.groupby('Gender')['Average'].mean().reset_index()
hometown_mean = df.groupby('Hometown')['Average'].mean().reset_index()

# b. Display the three summary tables
print("Mean Average by Track:")
display(track_mean)
print("\nMean Average by Gender:")
display(gender_mean)
print("\nMean Average by Hometown:")
display(hometown_mean)

# c. Create one figure containing three bar charts
fig, axes = plt.subplots(1, 3, figsize=(15, 5))

# Plot 1: Mean Average by Track
axes[0].bar(track_mean['Track'], track_mean['Average'], color='skyblue')
axes[0].set_title('Mean Average by Track')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Average')
axes[0].set_ylim(0, 100)

# Plot 2: Mean Average by Gender
axes[1].bar(gender_mean['Gender'], gender_mean['Average'], color='lightcoral')
axes[1].set_title('Mean Average by Gender')
axes[1].set_xlabel('Gender')
axes[1].set_ylabel('Mean Average')
axes[1].set_ylim(0, 100)

# Plot 3: Mean Average by Hometown
axes[2].bar(hometown_mean['Hometown'], hometown_mean['Average'], color='lightgreen')
axes[2].set_title('Mean Average by Hometown')
axes[2].set_xlabel('Hometown')
axes[2].set_ylabel('Mean Average')
axes[2].set_ylim(0, 100)

# Adjust layout for readability
plt.tight_layout()
plt.show()

# d. Interpretation Statements
# 1. Track: Communication recorded the highest sample mean average (67.98), followed closely by Microelectronics (67.50) and Instrumentation (65.23).
# 2. Gender: Male students recorded a slightly higher sample mean average (67.18) compared to Female students (66.62).
# 3. Hometown: Students from Luzon recorded the highest sample mean average (68.08), followed by Mindanao (66.67) and Visayas (65.75).


```
---

## 📁 Project File Structure
├── GUINTO_ECE2112_PA4.ipynb  # Main Jupyter Notebook containing all executed cells 
├── README.md                 # Project documentation (this file)
└── board2.csv                # Source dataset containing student exam variables


---

## 🛠️ Prerequisites & Requirements

To run the notebook successfully, ensure the following are installed:

*   **Python 3.x**
*   **Jupyter Notebook** or an IDE that supports `.ipynb` files (like VS Code)
*   **Pandas Library** (Can be installed via `pip install pandas`)
*   **Matplotlib Library** (Can be installed via `pip install matplotlib`)
  
---

## 🚀 How to Run

### Using Jupyter Notebook / VS Code
1.  Clone the repository
    `https://github.com/nylejustineguintoeng-sudo/EXPERIMENT-3-PYTHON-DATA-ANALYSIS-PANDAS.git`
    to your local machine.
2.  Ensure that `board2.csv` and `GUINTO_ECE2112_PA4.ipynb` are located in the same directory.
3.  Open `GUINTO_ECE2112_PA4.ipynb` in your preferred Jupyter environment.
4.  Select **Run All** (or execute each cell sequentially using `Shift + Enter`) to load the DataFrame, generate the requested subsets, and output the visualizations.

