# 📊 Human Resources Analytics Dashboard — Tableau

![Tableau](https://img.shields.io/badge/Tableau-Dashboard-E97627?style=for-the-badge&logo=tableau&logoColor=white)
![Python](https://img.shields.io/badge/Python-Data%20Generation-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Preparation-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Status](https://img.shields.io/badge/Project-Completed-03C4A1?style=for-the-badge)

## 📌 Project Overview

The **Human Resources Analytics Dashboard** is an interactive Tableau project designed to provide a comprehensive view of workforce composition, employee demographics, compensation, departmental distribution, hiring trends, termination trends, and individual employee records.

The project contains two main Tableau dashboards:

1. **HR | Summary** — an executive-level overview of workforce KPIs and HR trends.
2. **HR | Details** — an interactive employee-level table for detailed filtering and record analysis.

The dashboard is designed with an interactive dark-theme interface, custom navigation, filters, dashboard actions, tooltips, geographic analysis, and calculated fields.

---

## 🎯 Business Objective

The objective of this project is to transform employee-level HR data into an interactive analytical solution that can help HR teams and management:

- Monitor active, hired, and terminated employees.
- Understand workforce distribution across departments.
- Analyze gender, age, and education composition.
- Compare education levels with employee performance.
- Analyze salary patterns by education, gender, age, and job title.
- Identify workforce distribution across states and cities.
- Analyze hiring and termination trends over time.
- Explore individual employee records using interactive filters.
- Evaluate employee tenure and length of employment.

---

## 🗂️ Dataset

The project uses a synthetic employee dataset named **`HumanResources.csv`**.

### Dataset Size

| Metric | Value |
|---|---:|
| Total Records | 8,950 |
| Columns | 15 |
| Active Employees | 7,984 |
| Terminated Employees | 966 |
| Departments | 7 |
| Job Titles | 28 |
| Education Levels | 4 |

The standalone `HumanResources.csv` contains 8 states and 24 cities. The packaged Tableau Hyper source inside the `.twbx` contains the version used by the exported dashboard and includes additional geographic values visible in the workbook, such as West Virginia and cities including Charleston, Huntington, and Morgantown. Therefore, **the packaged `.twbx` / Hyper source should be treated as the authoritative dashboard data source**.

### Dataset Columns

| Column | Description |
|---|---|
| `employee_id` | Unique employee identifier |
| `first_name` | Employee first name |
| `last_name` | Employee last name |
| `gender` | Employee gender |
| `state` | Employee state |
| `city` | Employee city |
| `hiredate` | Employee hiring date |
| `department` | Employee department |
| `job_title` | Employee job title |
| `education_level` | Highest education level |
| `salary` | Employee salary |
| `performance_rating` | Employee performance rating |
| `overtime` | Whether the employee works overtime |
| `birthdate` | Employee date of birth |
| `termdate` | Employee termination date; blank for active employees |

> **Note:** The dataset is synthetic and was generated programmatically for dashboard development and portfolio/learning purposes. It should not be interpreted as real-world company HR data.

---

## 🐍 Data Generation

The dataset was generated using the included **`csv file creation.py`** script.

### Python Libraries Used

- Python
- Pandas
- NumPy
- Faker
- Random
- Datetime

The script creates employee attributes including:

- Employee IDs and names
- Gender
- State and city
- Hire and termination dates
- Departments and job titles
- Education levels
- Salary
- Performance rating
- Overtime status
- Birth dates

The generated data is exported to:

```text
HumanResources.csv
```

The Tableau workbook uses a packaged Hyper data source, so the dashboard can be opened independently of the CSV file.

---

## 🛠️ Tools & Technologies

| Tool / Technology | Purpose |
|---|---|
| **Tableau** | Interactive dashboard development and visualization |
| **Tableau Hyper** | Packaged analytical data source |
| **Python** | Synthetic HR dataset generation |
| **Pandas** | DataFrame creation and CSV generation |
| **NumPy** | Randomized data generation and numerical operations |
| **Faker** | Synthetic names and date generation |
| **GitHub** | Project version control and portfolio presentation |

---

# 📊 Dashboard 1 — HR Summary

The **Summary** dashboard provides an executive-level view of the organization's workforce.

![HR Summary Dashboard](HR%20Summary)

### Key KPI Cards

- **Active Employees:** 7,984
- **Hired Employees:** 8,950
- **Terminated Employees:** 966

### Summary Dashboard Sections

#### 👥 Workforce Overview
Displays active employees, hired employees, and terminated employees with trend visuals.

#### 🏢 Department Analysis
Shows employee distribution across:

1. Operations
2. Sales
3. Customer Service
4. IT
5. Marketing
6. Finance
7. HR

#### 👤 Gender Analysis
The dashboard visualizes workforce composition by gender.

- Female: 46%
- Male: 54%

#### 🎓 Education & Age
Analyzes the relationship between:

- Education level
- Age groups
- Gender

Age groups include:

- `<25`
- `25–34`
- `35–44`
- `45–54`
- `55+`

#### ⭐ Education & Performance
Shows employee performance distribution across education levels.

Performance categories:

- Excellent
- Good
- Satisfactory
- Needs Improvement

#### 💰 Income Analysis
Visualizes salary differences across education levels and gender.

#### 📈 Age & Salary
A scatter plot is used to analyze the relationship between employee age, salary, and job title.

#### 🗺️ Location Analysis
Maps employee distribution across U.S. states and distinguishes between:

- HQ
- Branch

---

# 📋 Dashboard 2 — HR Details

The **Details** dashboard provides an employee-level view of the HR dataset.

![HR Details Dashboard](HR Details.png)

The employee table provides grouped analytical sections for:

- ID
- Demographics
- Role
- Geographics
- Salary
- Status
- Length of Employment

### Interactive Filters

Users can filter employee records by:

- Full Name
- Gender
- Age Group
- Education Level
- Employee ID
- City
- Department
- Job Title
- State
- Hire Date
- Termination Date
- Salary Range

### Employee Information

Each record can display:

- Employee ID
- Full Name
- Age
- Gender
- Education
- Job Title
- Department
- City
- State
- Salary
- Employment Status
- Hire Date
- Length of Employment

---

# 🧮 Tableau Calculated Fields & Techniques

The workbook uses several Tableau calculations to create dynamic HR metrics and interactions.

### Employee Status

```text
IF ISNULL([Termdate]) THEN 'Hired'
ELSE 'Terminated'
END
```

Used to classify employees based on whether a termination date exists.

### Total Employees

```text
COUNT([Employee_ID])
```

### Terminated Employees

```text
COUNT(
    IF NOT ISNULL([Termdate])
    THEN [Employee_ID]
    END
)
```

### Active Employees

```text
COUNT(
    IF ISNULL([Termdate])
    THEN [Employee_ID]
    END
)
```

### Age

```text
DATEDIFF('year', [Birthdate], TODAY())
```

### Age Groups

Employees are categorized into:

```text
<25
25-34
35-44
45-54
55+
```

### Full Name

```text
[First Name] + ' ' + [Last Name]
```

### Length of Employment

For active employees:

```text
DATEDIFF('year', [Hiredate], TODAY())
```

For terminated employees:

```text
DATEDIFF('year', [Hiredate], [Termdate])
```

The workbook also uses Tableau table calculations such as:

- `RANK()`
- `WINDOW_MAX()`
- `TOTAL()`
- `INDEX()`

These support ranking, percentage-of-total calculations, highlighting, and interactive dashboard behavior.

---

# 🔍 Key Data Insights

Based on the included dataset:

### Workforce

- **8,950** total employee records are available.
- **7,984** employees are currently classified as active.
- **966** employees have termination dates.
- The dataset therefore represents an approximately **89% active / 11% terminated** workforce split.

### Department Distribution

**Operations** has the largest workforce with **2,718** employees, followed by:

- Sales — 1,835
- Customer Service — 1,673
- IT — 1,382
- Marketing — 718
- Finance — 452
- HR — 172

### Education

The largest education group is **Bachelor's degree**, with **5,418 employees**.

Other groups:

- High School — 1,819
- Master — 1,235
- PhD — 478

### Performance

The most common performance rating is **Good**, with **4,449 employees**.

Other ratings:

- Satisfactory — 2,671
- Excellent — 1,112
- Needs Improvement — 718

### Overtime

- No — 6,240 employees
- Yes — 2,710 employees

### Salary

| Statistic | Salary |
|---|---:|
| Minimum | $51,835 |
| Average | $70,946 |
| Median | $66,592 |
| Maximum | $149,377 |

These metrics are calculated from the complete synthetic dataset and provide the basis for the salary visualizations in Tableau.

---

# 🎨 Dashboard Design

The dashboard follows a modern dark analytical theme.

The project uses the following primary design colors:

```text
#777777  → Gray
#F5F5F5  → White
#03C4A1  → Neon / Teal
#C52A87  → Pink
```

The color palette is used consistently for:

- Active employees
- Terminated employees
- Highlights
- Interactive elements
- KPI emphasis
- Navigation
- Dashboard actions

---

# ⚙️ Tableau Features Used

This project demonstrates practical Tableau skills including:

- Interactive dashboards
- Dashboard actions
- Filters
- Filter groups
- Tooltips
- Highlighting
- Table calculations
- Calculated fields
- KPI / BAN cards
- Bar charts
- Donut charts
- Scatter plots
- Geographic maps
- Trend charts
- Employee detail tables
- Custom dashboard navigation
- Interactive filtering
- Conditional status classification
- Ranking
- Percentage-of-total calculations
- Dynamic employment-duration calculations

---

# 📁 Project Structure

```text
HR Tableau Project/
│
├── Human Resource Dashboard.twbx
├── Human Resource Dashboard.twb
│
├── HumanResources.csv
├── csv file creation.py
│
├── HR  Summary.png
├── HR  Details.png
│
├── Human Resource Dashboard.pdf
├── Human Resource Dashboard 1.pdf
│
├── colours.txt
│
└── Human Resource Dashboard.twb Files/
    ├── Data/
    │   └── federated.hyper
    │
    └── Image/
        ├── Logo.png
        ├── dashboard-summary-active.png
        ├── dashboard-summary-inactive.png
        ├── dashboard-records-active1.png
        ├── dashboard-records-inactive.png
        ├── filter-active.png
        ├── filter-inactive.png
        ├── info-shown.png
        ├── info-hidden.png
        ├── download pdf.png
        ├── download image.png
        └── ...
```

---

# 🚀 How to Use

### Option 1 — Open the packaged Tableau workbook

Open:

```text
Human Resource Dashboard.twbx
```

The `.twbx` file is the packaged Tableau workbook and contains the workbook along with its packaged data/assets.

### Option 2 — Open the Tableau workbook

Open:

```text
Human Resource Dashboard.twb
```

If Tableau requests the data source, use the included dataset or packaged Hyper data source.

### Option 3 — Explore the source dataset

Open:

```text
HumanResources.csv
```

The CSV contains the employee-level data used by the project.

---

# 📌 Project Highlights for Data Analyst Portfolio

This project demonstrates my ability to:

- Build end-to-end BI dashboards.
- Convert raw employee-level data into meaningful HR analytics.
- Create interactive Tableau dashboards.
- Design KPI-driven reports.
- Develop calculated fields and table calculations.
- Perform demographic and salary analysis.
- Build geographic visualizations.
- Create employee-level drill-down analysis.
- Apply dashboard actions and interactive filters.
- Generate and structure synthetic datasets using Python.
- Combine Python-based data preparation with Tableau visualization.

---

# 💼 Skills Demonstrated

**Tableau | Data Visualization | Business Intelligence | Dashboard Development | Calculated Fields | Table Calculations | Data Analysis | HR Analytics | KPI Reporting | Interactive Filters | Dashboard Actions | Geographic Analysis | Python | Pandas | NumPy | Faker | Data Storytelling**

---

# 📷 Dashboard Preview

### HR Summary

![HR Summary](HR Summary.png)

### HR Details

![HR Details](HR Details.png)

---

# 📄 Project Files

| File | Purpose |
|---|---|
| `Human Resource Dashboard.twbx` | Packaged Tableau workbook |
| `Human Resource Dashboard.twb` | Tableau workbook definition |
| `HumanResources.csv` | Standalone HR employee dataset generated with Python |
| `csv file creation.py` | Python script used to generate the standalone dataset |
| `Human Resource Dashboard.pdf` | Exported HR Details dashboard |
| `Human Resource Dashboard 1.pdf` | Exported HR Summary dashboard |
| `colours.txt` | Dashboard color palette |
| `*.hyper` | Tableau Hyper data source |

---

# 🧠 Key Learning Outcomes

Through this project, I strengthened my practical understanding of:

1. HR analytics and workforce KPIs.
2. Tableau dashboard architecture.
3. Interactive filtering and dashboard actions.
4. Tableau calculated fields.
5. Table calculations and ranking.
6. Data storytelling and dashboard layout.
7. Geographic and demographic analysis.
8. Salary and performance analysis.
9. Employee-level drill-down reporting.
10. Python-based synthetic data generation.

---

# 👨‍💻 Author

**Bhaskar Patel**

Data Analyst | Tableau | SQL | Python | Data Visualization

---

⭐ If you find this project useful, feel free to explore the workbook and dashboard files in this repository.
