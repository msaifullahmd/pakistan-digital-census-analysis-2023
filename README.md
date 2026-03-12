# pakistan-digital-census-analysis-2023
Analysis of Pakistan's 1st Digital Census (2023) with GIS data &amp; ISIC codes. Includes population distribution, housing units, economic activity tracking across 160K+ enumeration blocks. Data from Pakistan Bureau of Statistics.

# Pakistan Census 2023 Dataset - Population Statistics by Administrative Unit

## 📊 Dataset Overview
This dataset contains official population statistics from **Pakistan's 7th Population and Housing Census (2023)** - the country's first-ever digital census. The data is disaggregated by administrative units (provinces, divisions, districts) with key demographic indicators.

**Source:** Pakistan Bureau of Statistics (PBS)
**Census Year:** 2023
**Previous Census:** 2017
**Geographic Coverage:** All provinces and territories of Pakistan

## 📁 Files in This Repository
| File Name | Description |
|-----------|-------------|
| `census_2023_population.csv` | Main dataset with population statistics by administrative unit |
| `data_dictionary.csv` | Detailed explanation of all variables |
| `README.md` | This file - dataset documentation |

## 📋 Variable Dictionary

| Variable | Description | Example Values | Notes |
|----------|-------------|----------------|--------|
| `NAME OF ADMINISTRATIVE UNIT` | Name of province, division, or district | "Punjab", "Karachi Central", "Lahore" | Hierarchical administrative levels |
| `AREA IN SQ.KM` | Total geographic area in square kilometers | 205344, 1752 | Land area only |
| `ALL SEXES` | Total population count | 127688922, 5732954 | Male + Female + Transgender |
| `MALE` | Male population count | 65217408, 3012487 | |
| `FEMALE` | Female population count | 62462487, 2720061 | |
| `TRANS GENDER` | Transgender population count | 9027, 406 | Officially counted in 2023 census |
| `SEX RATIO` | Males per 100 females | 104.39, 110.75 | Calculated as (Male/Female)*100 |
| `DENSITY PER SQ.KM` | Population per square kilometer | 622, 3272 | Total Population/Area |
| `URBAN PROPORTION` | Percentage living in urban areas | 36.7, 100.0 | 0-100% scale |
| `AVG. H.HOLD SIZE` | Average persons per household | 6.7, 5.2 | |
| `POPULATION 2017` | Population as per 2017 census | 110012442, 4675679 | For growth calculation |
| `2017-2023 AVG. ANNUAL G.RATE` | Average yearly growth rate between censuses | 2.55, 1.52 | Expressed as percentage |

## 🔍 Key Insights This Data Can Reveal

### Demographic Analysis
1. **Population Distribution:** Which provinces/districts have the highest/lowest populations?
2. **Gender Balance:** Which areas have the highest male-to-female ratios?
3. **Transgender Population:** Geographic distribution of officially counted transgender persons
4. **Urbanization:** Which areas are most/least urbanized?

### Density & Growth
5. **Population Density:** Most crowded vs. most sparsely populated districts
6. **Growth Hotspots:** Which areas grew fastest since 2017?
7. **Urban-Rural Divide:** Compare urban vs. rural population proportions
8. **Household Size:** Regional variations in average family size

### Comparative Analysis
9. **2017 vs 2023:** How has the population landscape changed?
10. **Provincial Rankings:** Rank provinces by different demographic indicators

## 📈 Sample Analysis Questions You Can Answer

Using this dataset, you can find:

1. **Which province has the largest population?**
   *Answer: Punjab (~127.7 million)*

2. **Which district has the highest population density?**
   *(You'll calculate this)*

3. **Where is the transgender population highest?**
   *(You'll identify from TRANS GENDER column)*

4. **Which areas grew fastest since 2017?**
   *(Sort by ANNUAL GROWTH RATE)*

5. **What's the most urbanized province?**
   *(Compare URBAN PROPORTION across provinces)*

6. **Where are households largest?**
   *(Sort by AVG. H.HOLD SIZE)*

## 🛠️ How to Use This Data

### In Excel/Google Sheets:
1. Download the CSV file
2. Use pivot tables to summarize by province
3. Create charts showing population distribution
4. Calculate rankings and comparisons

### In Python (Pandas):
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the data
df = pd.read_csv('census_2023_population.csv')

# Display basic information
print("Dataset Shape:", df.shape)
print("\nColumn Names:")
print(df.columns.tolist())
print("\nData Types:")
print(df.dtypes)
print("\nFirst 5 rows:")
print(df.head())

# Summary statistics
print("\nSummary Statistics:")
print(df.describe())

# Check for missing values
print("\nMissing Values:")
print(df.isnull().sum())

# Top 10 most populous administrative units
top_10_population = df.nlargest(10, 'ALL SEXES')[['NAME OF ADMINISTRATIVE UNIT', 'ALL SEXES']]
print("\nTop 10 Most Populous Areas:")
print(top_10_population)

# Areas with highest population density
top_10_density = df.nlargest(10, 'DENSITY PER SQ.KM')[['NAME OF ADMINISTRATIVE UNIT', 'DENSITY PER SQ.KM']]
print("\nTop 10 Highest Density Areas:")
print(top_10_density)

# Fastest growing areas (highest growth rate)
fastest_growth = df.nlargest(10, '2017-2023 AVG. ANNUAL G.RATE')[['NAME OF ADMINISTRATIVE UNIT', '2017-2023 AVG. ANNUAL G.RATE']]
print("\nTop 10 Fastest Growing Areas:")
print(fastest_growth)

# Simple visualization example
plt.figure(figsize=(12, 6))
top_10 = df.nlargest(10, 'ALL SEXES')
plt.barh(top_10['NAME OF ADMINISTRATIVE UNIT'], top_10['ALL SEXES'])
plt.xlabel('Population')
plt.title('Top 10 Most Populous Administrative Units in Pakistan (2023)')
plt.tight_layout()
plt.show()
