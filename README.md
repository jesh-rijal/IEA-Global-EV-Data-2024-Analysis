# 🚗 IEA Global EV Data 2024 (EDA) Project

## 📌 Project Overview

This project performs an **Exploratory Data Analysis (EDA)** on the **International Energy Agency (IEA) Global EV Data 2024 dataset**. The goal is to understand global Electric Vehicle (EV) adoption trends, identify patterns across regions, analyze vehicle sales growth, and visualize the evolution of EV markets worldwide.

The notebook walks through the complete EDA workflow, including:

* 📥 Data loading
* 🧹 Data cleaning
* ⚙️ Data preprocessing
* 🔍 Missing value inspection
* ♻️ Duplicate checking
* 📦 Outlier detection
* 📊 Statistical analysis
* 📈 Trend analysis
* 🎨 Data visualization

---

# 📂 Dataset Information

The dataset contains information about global electric vehicle statistics collected by the International Energy Agency (IEA).

### Key Features

| Column | Description |
|----------|-------------|
| 🌍 region | Country or geographical region |
| 📊 category | Type of data category |
| ⚡ parameter | EV-related metric (e.g., EV Sales, EV Stock) |
| 🚘 mode | Vehicle category or transportation mode |
| 🔋 powertrain | EV technology type |
| 📅 year | Reporting year |
| 📏 unit | Measurement unit |
| 🔢 value | Numerical value of the metric |
| 📉 percentage | Percentage values (removed during cleaning) |

---

# 🛠 Technologies Used

* 🐍 Python
* 🐼 Pandas
* 🔢 NumPy
* 📈 Matplotlib
* 🎨 Seaborn
* 📓 Jupyter Notebook

⬇️ Install required libraries:

```bash
pip install pandas numpy matplotlib seaborn notebook
```

---

# 📁 Project Structure

```text
📂 IEA-Global-EV-Data-2024-Analysis
│
├── 📑 EDA Report of IEA Global EV 2024.pdf
├── ⚡📊 IEA Global EV Data 2024 new.csv
├── 🐍📓 IEA Global EV Data 2024 new.ipynb
├── 📖 README.md
│
└── 📁 outputs/
    ├── 📈 visualizations
    └── 📊 charts
```

---

## ▶️ How to Run the Project

### 1️⃣ 💻 Open Git Bash

### 2️⃣ 📥 Clone the Repository

```bash
git clone https://github.com/jesh-rijal/IEA-Global-EV-Data-2024-Analysis.git
```

### 3️⃣ 📂 Move into the Project Folder

```bash
cd IEA-Global-EV-Data-2024-Analysis
```

### 4️⃣ 📝 Open the Project in VS Code

```bash
code .
```

### 5️⃣ 🚀 Run the Jupyter Notebook

📓 Open the notebook file **`IEA Global EV Data 2024 new.ipynb`** and run all cells sequentially to reproduce the **Exploratory Data Analysis (EDA)**.

---

# 🔍 Notebook Walkthrough

## 1️⃣ Importing Libraries

The notebook begins by importing essential Python libraries:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

### Purpose

* 🔢 NumPy → Numerical operations
* 🐼 Pandas → Data manipulation
* 📈 Matplotlib → Plotting graphs
* 🎨 Seaborn → Advanced visualizations

---

## 2️⃣ Loading the Dataset

```python
dataset = pd.read_csv('IEA Global EV Data 2024 new.csv')
```

The dataset is loaded into a Pandas DataFrame for analysis.

---

## 3️⃣ Initial Data Inspection

The following commands are used:

```python
dataset.head()
dataset.sample(5)
dataset.tail()
dataset.shape
dataset.columns
```

### Purpose

- 🔍 View first records
- 🎲 View random records
- 📋 View last records
- 📐 Check dataset dimensions
- 📝 Display column names

---

## 4️⃣. Cleaning the Value Column

The dataset stores some numeric values in string format.

```python
dataset['value'] = (
    dataset['value']
    .astype(str)
    .str.replace('.', '', regex=False)
    .str.replace(',', '.', regex=False)
)
```

Then:

```python
dataset['value'] = pd.to_numeric(dataset['value'], errors='coerce')
dataset['value'] = dataset['value'].astype(int)
```

### Purpose

- 🧹 Remove formatting issues
- 🔄 Convert strings into numerical values
- 📊 Enable statistical analysis

---

## 5️⃣. Removing the Percentage Column

```python
dataset = dataset.drop(columns=['percentage'])
```

### Reason

The percentage column contains inconsistent and corrupted values and does not contribute significantly to the analysis.

---

## 6️⃣. Dataset Summary

```python
dataset.info()
dataset.describe()
dataset.describe(include='object')
```

### Purpose

Provides:

- 🏷️ Data types
- ✅ Non-null counts
- 📊 Statistical summary
- 🗂️ Categorical summaries

---

## 7️⃣. Understanding Categorical Variables

The notebook explores unique values from:

```python
dataset['region']
dataset['category']
dataset['parameter']
dataset['mode']
dataset['powertrain']
dataset['year']
dataset['unit']
```

### Purpose

* Understand available categories and dimensions within the dataset.

---

## 8️⃣. Missing Value Analysis

```python
dataset.isnull().sum()
```

Checks for missing values in every column.

---

## 9️⃣. Duplicate Record Analysis

```python
dataset.duplicated().sum()
```

Determines whether duplicate records exist.

---

## 🔟. Outlier Detection

### Boxplot Visualization

```python
sns.boxplot(dataset['year'])
```

Used to identify unusual values in the Year column.

### IQR Method

```python
Q1 = dataset['year'].quantile(0.25)
Q3 = dataset['year'].quantile(0.75)
IQR = Q3 - Q1
```

Outliers are removed using:

```python
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR
```

### Purpose

* Improve data consistency and reduce skewness.

---

# 📊 Exploratory Analysis

## 1️⃣ Region Distribution

```python
dataset['region'].value_counts()
```

Shows the number of records available for each region.

---

## 2️⃣ Year Distribution

```python
dataset['year'].value_counts()
```

Displays record frequency by year.

---

## 3️⃣ Mode Distribution

```python
dataset['mode'].value_counts()
```

Shows how EV data is distributed among transportation modes.

---

## 4️⃣ Highest EV Metric Value

```python
highest_sales = dataset['value'].max()
```

Identifies:

- 📈 Maximum recorded EV metric
- 🌍 Associated region
- 🏷️ Related category

---

# 📈 EV Adoption Trend Analysis

The notebook filters:

```python
EV Stock
EV Sales
```

Then groups data by year:

```python
yearly_adoption = (
    ev_data
    .groupby('year')['value']
    .sum()
    .reset_index()
)
```

### 📈 Visualization

```python
sns.lineplot()
```

### 💡 Insight

Shows how global EV adoption has evolved over time.

---

# 🥧 EV Mode Distribution

The notebook filters records measured in:

```python
unit == 'Vehicles'
```

Then creates a pie chart showing the distribution of EV transportation modes.

### 📈 Visualization

```python
plt.pie()
```

### 💡 Insight

Illustrates which vehicle categories dominate the EV market.

---

# 🌍 Regional EV Analysis

The notebook groups vehicle data by region:

```python
vehicles.groupby('region')['value'].sum()
```
This code groups the data by region and calculates the total value for each region, enabling a comparative analysis of EV activity across regions.

### 📊 Bar Chart

```python
sns.barplot()
```

### 💡 Insight

Highlights regions with the highest EV activity and adoption.

---

# 📈 Visualizations Included

The project generates:

### 1️⃣. Year Outlier Boxplot

Shows outliers within the Year column.

### 2️⃣. Cleaned Year Boxplot

Displays year distribution after outlier removal.

### 3️⃣. EV Adoption Trend Line Chart

Visualizes EV growth over time.

### 4️⃣. EV Mode Pie Chart

Shows market share of vehicle categories.

### 5️⃣. Regional Sales Bar Chart

Compares total EV values across regions.

---

# 🎯 Key Objectives

This analysis helps answer questions such as:

- 📈 How fast is EV adoption growing globally?
- 🌐 Which regions dominate EV sales and stock?
- 🚙 Which transportation modes are most common?
- ⚠️ Are there data quality issues?
- 📅 What trends can be observed over time?

---

# 📌 Future Improvements

Potential enhancements:

- 🎛️ Interactive dashboards using Plotly
- 🔮 EV market forecasting
- 🤖 Machine learning models
- ⏳ Time-Series Analysis
- 🌐 Region-wise comparative dashboards

---

# 🤝 Contributing

We welcome contributions from everyone! Follow the steps below to contribute.

---

## 1️⃣ Fork the Repository
Click the **Fork** button at the top right of this repository.

---

## 2️⃣ Clone Your Fork

Replace `<your-username>` and `<repository-name>` with your GitHub details:

```bash
git clone https://github.com/your-username/repository-name.git
cd repository-name
````

---

## 3️⃣ Create a New Branch

Create a meaningful branch name based on your work:

```bash
git checkout -b feature-name
```

💡 Examples:

* `feature-login-system`
* `fix-navbar-bug`
* `improve-dashboard-ui`

---

## 4️⃣ Make Your Changes

Add your improvements or fixes to the project.

---

## 5️⃣ Commit Your Changes

```bash
git commit -m "Add a clear description of your changes"
```

---

## 6️⃣ Push to GitHub

```bash
git push origin feature-name
```

---

## 7️⃣ Open a Pull Request

Go to the original repository and click **“New Pull Request”**.

Explain:

* What you changed
* Why you changed it

---

## ✅ Guidelines

* Keep code clean and readable
* Follow existing project style
* Test your changes before submitting PR
* Use meaningful commit messages

---

Thank you for contributing! 🚀

---

# 👨‍💻 Author

```bash
Name: Jesh Rijal
GitHub: [My GitHub Profile](https://github.com/jesh-rijal)
```
---

# 📜 License

This project is open-source and available for educational and learning purposes.

---

# ⭐ If you like this project

Give it a ⭐ on GitHub!
