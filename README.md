
# Healthcare Spending Impact Analysis: Optimizing Health Investment Strategies Across Africa

![Capstone Project](figures/efficiency_ranking.png)

This repository documents our comprehensive analysis of healthcare financing and outcomes across African countries. We identify which spending patterns deliver the greatest health impact per dollar invested and highlight high-efficiency health systems that achieve strong outcomes despite limited resources.

## 🌐 Project Overview

**Research Question**:  
*"Which spending patterns deliver the greatest health impact per dollar invested, and which countries offer scalable models of efficient health system performance?"*

**Key Finding**:  
**Efficiency > Spending** - How you spend matters more than how much you spend. Algeria achieves 11+ years more life expectancy than predicted by its spending level.

**Data Sources**:  
- WHO Global Health Expenditure Database (GHED)
- World Bank Health, Nutrition and Population (HNP) Statistics

**Time Period**: 2000-2022  
**Coverage**: 47 African countries  
**Observations**: 1,054 country-year records

---

## 🔬 The Complete Data Pipeline

Our analysis follows a rigorous, transparent data science workflow. Below is the **chronological journey** from raw data to actionable insights.

### 📥 **Stage 1: Data Acquisition**  
*(Notebook: `notebooks/data_acquisition.ipynb`)*

**What We Did**:
1. Downloaded 12 WHO GHED indicator files (2000-2023)
2. Downloaded World Bank HNP data for all health indicators
3. Downloaded WHO codes files (COUNTRY.csv, REGION.csv, etc.)

**Why It Matters**:  
Starting with raw data ensures transparency and reproducibility. The WHO GHED provides detailed health financing data, while the World Bank offers outcome metrics and socioeconomic context.

**Key Insight**:  
The WHO data uses a standardized coding system (SpatialDimensionValueCode) that must be mapped to country names for integration with World Bank data.

---

### 🌍 **Stage 2: WHO Data Processing**  
*(Notebook: `notebooks/who_data_aggregation_processing.ipynb`)*

**What We Did**:
1. Loaded and inspected `COUNTRY.csv` to understand African country codes
2. Filtered for African countries using the ParentTitle field
3. Created a country mapping for standardization
4. Processed all 12 WHO indicator files, keeping only African countries
5. Merged all indicators into a unified WHO dataset

**Why It Matters** 
This stage transforms raw WHO data into a clean, African-focused dataset. The country mapping ensures we only include African nations and correctly identify regional groupings.

**Key Insight**: 
The WHO uses a hierarchical coding system where ParentTitle = 'Africa' is our filter for African countries. This aligns with the World Bank's regional definitions.

---

### 🌍 **Stage 3: World Bank Data Processin**  
*(Notebook: `notebooks/wb_cleaning_transformation.ipynb`)*

**What We Did**:
1. Loaded the raw World Bank data
2. Transformed the data from wide to long format using melt()
3. Extracted the year from the column names and converted to numeric
4. Pivoted the data to create a wide-format dataset with indicators as columns
countries
5. Standardized country names to match WHO data
6. Saved the processed dataset as world_bank_health_outcomes.csv

**Why It Matters** 
World Bank data comes in a wide format that's difficult to analyze. Converting to long format makes it easier to work with and merge with WHO data.

**Key Insight**: 
Country name standardization is critical - the World Bank and WHO use different naming conventions for the same countries. Our mapping ensures accurate merging.

---

### 🌍 **Stage 4: Data Integration**  
*(Notebook: `notebooks/who_wb_data_aggregation.ipynb`)*

**What We Did**:
1. Loaded the processed WHO and World Bank datasets
2. Standardized country name column for merging
3. Applied country name standardization to both datasets
4. Merged WHO financing data with World Bank outcomes
5. Filtered for relevant years (2000-2022) and cleaned missing values
6. Saved the final unified dataset as african_health_spending_outcomes.csv

**Why It Matters** 
This integration creates the foundation for our analysis by linking health financing (WHO) with health outcomes (World Bank).

**Key Insight**: 
The merge on Country Name and Year ensures we're comparing spending and outcomes for the same country in the same year - critical for valid analysis.

---

### 🌍 **Stage 5:  Analysis & Insight**  
*(Notebook: `notebooks/afriHealth_capstone_analysis.ipynb`)*

**What We Did**:
1. Conducted Exploratory Data Analysis (EDA)
2. Built a linear regression model to predict life expectancy
3. Calculated efficiency scores as residuals (actual - predicted)
4. Applied Weighted Mean 66POP for regional aggregation
5. Generated key visualizations
6. Saved the final unified dataset as african_health_spending_outcomes.csv

**Why It Matters** 
This stage transforms cleaned data into actionable insights using rigorous statistical methods aligned with World Bank standards.

**Key Insight**: 
The Weighted Mean 66POP rule (no aggregate if missing data >1/3 of population) ensures our regional results are robust and transparent

---

### **📊 Key Variables Explained**  

Use MS excel to open the text file 'key-variables-explained.csv' for explanations of key variables and why each matters.  

**What We Did**:
1. Conducted Exploratory Data Analysis (EDA)
2. Built a linear regression model to predict life expectancy
3. Calculated efficiency scores as residuals (actual - predicted)
4. Applied Weighted Mean 66POP for regional aggregation
5. Generated key visualizations
6. Saved the final unified dataset as african_health_spending_outcomes.csv

**Why It Matters** 
This stage transforms cleaned data into actionable insights using rigorous statistical methods aligned with World Bank standards.

**Key Insight**: 
The Weighted Mean 66POP rule (no aggregate if missing data >1/3 of population) ensures our regional results are robust and transparent

---

### **📈 Methodology: Weighted Mean 66POP**  
This is the gold standard for regional aggregation per World Bank methodology:

"Aggregates are calculated as weighted averages of available data. No aggregate is shown if countries with missing data represent more than one third of the total population of your custom group." 

**Why we use it**:
1. Prevents misleading averages from incomplete data
2. Larger countries (like Nigeria) properly influence regional averages
3. No imputation - only real data is used
4. Ensures transparency and policy relevance

**Example:** If calculating West Africa's average, and Nigeria (200M people) and Ghana (30M) have data but Côte d'Ivoire (28M) and others (42M) are missing, we can compute the average because missing population (70M) is < 1/3 of total (~300M).



### ** Running the Analysis References & Acknowledgements**  
Run the notebooks in this sequence:
- data_acquisition.ipynb
- who_ghed_data_aggregation_processing.ipynb
- wb_cleaning_transformation.ipynb
- who_wb_data_integration.ipynb
- afriHealth_capstone_analysis.ipynb

### ** View Results**  
All outputs are saved in:
- Processed data/processed-data/
- Final dataset: data/final-processed-data/african_health_spending_outcomes.csv
- Visualizations: figures/
- Project documentation: docs/



### **📚 References & Acknowledgements**  
This is the gold standard for regional aggregation per World Bank methodology:

"Aggregates are calculated as weighted averages of available data. No aggregate is shown if countries with missing data represent more than one third of the total population of your custom group." 

**Data Sources**:
1. World Health Organization. (2024). Global Health Expenditure Database
2. World Bank. (2024). Health, Nutrition and Population Statistics
3. World Bank. (2024). Aggregation Rules Documentation


**Tools used**:
- Python (pandas, numpy, scikit-learn, matplotlib, seaborn)
- Jupyter Notebook

**Team Members**:
- Jaji Jimoh Oludare: Data Wrangler
- Chidewu Tatenda: EDA Lead
- Rediet Tedla: Modeling Lead
- Daniel Cole: Visualizer
- Kingsley Njoku: Storyteller & Presenter
- Fondoh, Peter : 


...
### **📁 File Structure**  

africa-health-spending/
│
├── data/
│   ├── raw-data/
│   │   ├── who_ghed/
│   │   │   ├── data/                # Raw WHO GHED indicator files
│   │   │   └── codes/               # COUNTRY.csv, REGION.csv, etc.
│   │   └── world_bank/
│   │       └── world_bank_health_outcomes_raw.csv
│   │
│   ├── processed-data/
│   │   ├── world_bank_health_outcomes.csv
│   │   └── unified_african_health_financing.csv
│   │
│   └── final-processed-data/
│       └── african_health_spending_outcomes.csv
│
├── notebooks/
│   ├── 1_data_acquisition.ipynb     # Initial data download & setup
│   ├── who_ghed_data_aggregation_processing  # WHO GHED cleaning & filtering
│   ├── wb_cleaning_transformation.ipynb # World Bank cleaning & transformation
│   ├── who_wb_data_integration.ipynb     # Merging WHO & World Bank data
│   └── afriHealth_capstone_analysis.ipynb    # Final analysis & visualization
│
├── figures
│   ├── efficiency_ranking.png
│   ├── spending_trend.png.png
│   ├── govt_spending_vs_life.png
│   ├── oop_vs_infant_mortality.png
│   ├── 10 most efficient countries.csv
│   └── Regional Trends (2020, Weighted Mean 66POP.csv
│
├── docs/
│   ├── Group 7 - Project summary Report.docx
│   └── Group_7-Healthcare Spending Impact Analysis from 2000 to 2022.pptx
│
├── Video Presentation link
├── key-variables-explained.csv
└── README.md
...
