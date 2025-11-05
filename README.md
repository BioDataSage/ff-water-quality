# ff-water-quality

## Project Navigation
* data
  * country_indicators_and_fmr.csv - Our scrubbed and transformed data. This is the output .csv from code block 1 of water_health_correlation_pipeline.
  * fetal_mortality.csv - Under-5 mortality data. Taken from 'https://www.who.int/data/sets/health-inequality-monitor-dataset#igme-u5mr'
  * water_health_indicators - WASH indicator data. Taken from 'https://www.who.int/data/sets/health-inequality-monitor-dataset#wash'
* figures
  * vip_plot.png
* results
  * pearson_correlation_results.txt - Pearson correlation results between indicators and under-5 mortality. This is the output .txt from code block 2 of water_health_correlation_pipeline.qmd
* water_health_correlation_pipeline.qmd
  * This is our core pipeline that contains our data scrubber and data manipulation. It uses the Quatro medium. The medium is capable of interpretting both R and Python allowing each team member to play to their unique strengths.
***


# WASH Access and Child Mortality

## Research Question / Focus
What factors of water supply, sanitation, and hygiene are the biggest contributors to a country's infant mortality rate?

## Data Sources
- WASH Indicators (WHO Health Inequality Monitor - JMP): https://www.who.int/data/sets/health-inequality-monitor-dataset#wash
- Under-5 Mortality (WHO Health Inequality Monitor - IGME): https://www.who.int/data/sets/health-inequality-monitor-dataset#igme-u5mr
- Ejemot-Nwadiaro, R.I. et al. (2021) “Hand-washing promotion for preventing diarrhoea,” Cochrane database of systematic reviews, 12(1), p. CD004265. Available at: https://doi.org/10.1002/14651858.CD004265.pub4.
- Wolf, J. et al. (2018) “Impact of drinking water, sanitation and handwashing with soap on childhood diarrhoeal disease: updated meta-analysis and meta-regression,” Tropical medicine & international health: TM & IH, 23(5), pp. 508–525. Available at: https://doi.org/10.1111/tmi.13051.


## Indicators (independent variables)
- Population using basic sanitation services (%)
- Population using limited sanitation services (%)
- Population practising open defecation (%)
- Population using basic drinking water services (%)
- Population using limited drinking water services (%)
- Population using surface water (%)
- Population using basic hygiene services (%)
- Population using limited hygiene services (%)
- Population with no hygiene services (%)

## Outcome (dependent variables)
- Infant mortality rate (under-5 mortality or infant mortality as reported in IGME)

## Data Gathering / Data Cleaning
- Filtered the main dataset to keep only relevant data and dates on or before 2019, removing irrelevant columns to focus on necessary variables
- Converted date variables to appropriate formats and created a combined key (country_year) joining country/region and year for easier merging.
- Pivoted the main dataset to wide format with each indicator as a separate column for modeling.
- Cleaned the infant mortality dataset by selecting relevant dates, filtering, and creating a matching country_year key.
- Merged the two cleaned datasets on country_year and date, renamed columns for clarity, removed missing data and duplicates, creating the final dataset for analysis

## Data Completeness Consideration
Countries with insufficient data across the key WASH and mortality variables were identified.  
To maintain consistency and analytical reliability, countries with substantial missing values were excluded for correlation-based analyses, while broader visualizations could include all countries where data were available.

## Data Manipulation
- Join WASH indicators and infant mortality by country and year. (e.g., basic sanitation, open defecation)
- Create derived field(s) when needed:
  - High/low infant mortality label

## Aggregation
- Time-series (trend over 2000–2019, inclusive of both years)

## Analysis Plan
- Descriptive statistics for indicators and infant mortality
- Correlation analysis:
  - Compute Pearson correlations between each WASH indicator (% water, % sanitation, % hygiene) and infant mortality.
  - Report correlation coefficients.
- Fit a random forests classification model with intant mortality as the outcome and WASH variables as predictors.
- Use feature importance scores to rank variables by their contribution. 

# Data Analysis:
We cleaned, processed, and analyzed WASH datasets using R and Python within Posit Cloud (Jupyter & RStudio) and google colab. The analysis work included data wrangling, statistical summaries, and exploratory techniques to identify patterns, relationships, and trends in the data. We also implemented a Random Forest model in R to support predictive analysis and evaluate feature importance.
# Data Visualization:
We created various visual outputs to communicate findings effectively. This included scatter plots, bar graphs, tables, and other visual summaries built using Matplotlib in Python and ggplot2 in R. These charts helped highlight key patterns and illustrated important insights from the WASH datasets

Here is the plot for indicator importance:

![Indicator Importance Plot](https://github.com/BioDataSage/ff-water-quality/blob/main/figures/vip_plot.png)

Here is the scatter plot showing correlation in between Basic hygiene service and infant mortality 

![Scatter plot](https://github.com/BioDataSage/ff-water-quality/blob/main/figures/basic.png)

## Supporting Literature
Our analysis identified **basic drinking water access** and **basic hygiene services** as the strongest WASH-related predictors of lower infant mortality. Two key published studies corroborate these findings:
- Ejemot-Nwadiaro et al. (2021) found that hand-washing promotion in low- and middle-income settings reduces diarrhoeal disease incidence by approximately 25-33%.  (https://pubmed.ncbi.nlm.nih.gov/33539552/)
- Wolf et al. (2018) conducted a meta-analysis showing that improved drinking water, sanitation, and hand-washing interventions significantly lower childhood diarrhoea risk. (https://pubmed.ncbi.nlm.nih.gov/29537671/)

# Tools & Libraries Used

Python: Matplotlib, Pandas, NumPy

R: dplyr, ggplot2, tidyverse, ggthemes, tidyverse, tidymodels, rpart, rpart.plot, randomForest, infer, vip

Environment: Posit Cloud (RStudio & Jupyter)

# Team Members:
1.Chi Chi Okezie

2.Courtney-Grace Neizer

3.Darren Lee

4.Shivani Pawar
 
