# Walmart Product Performance Analysis

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0-green.svg)](https://pandas.pydata.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow.svg)](https://powerbi.microsoft.com/)

## Project Overview
Walmart needs to understand the relationship between discount strategies and customer satisfaction (ratings) to optimize their promotional approach and improve customer loyalty. To help them solve this problem, I analyzed a dataset of Walmart products to examine the relationship between discount and ratings, as well as how the type of product moderates this relationship. I used Python for statistical validation and Power BI to assemble an interactive report that Walmart can use to guide their discount optimization strategy.

## Technology Used
* Data Processing: Python (Pandas)
* Statistical Analysis: Scipy (ANOVA Testing), NumPy
* Visualization: Seaborn, Matplotlib, Power BI
* Analytics Engine: DAX (Data Analysis Expressions)

## Key Findings
* There is a very weak overall correlation between discount and ratings ($r = 0.05$).
* However, viewing product correlations by category reveals stronger correlations for Beauty ($r = 0.31$) and Food ($r = 0.16$) items.
* The highest rated brand is *Amay's*.
* The *home* category of items is significantly better rated than the other categories, especially *clothing* and *beauty*.

![Project Screenshot](images/RWalmartDashboard.png)
*Figure 1: Interactive Power BI dashboard showing findings without filtering for a specific product category.*
![Project Screenshot](images/RWalmartBeauty.png)
*Figure 2: Detailed view of the Beauty category, highlighting the stronger correlation between discount and ratings.*
![Project Screenshot](images/RWalmartFood.png)
*Figure 3: Food item analysis showing the correlation between discount percentage and customer satisfaction.*

## Technical Challenges & Solutions
1. Parsing Dictionary Data
   While cleaning data in Python, I realized that the rating_stars column contained string-formatted dictionaries for the 5 star levels for each product. This prevented analysis of the ratings breakdown of each item. To get around this, I wrote a function which first attempted to converted the data into true dictionaries if they weren't already. Then I parsed the dictionary data into 5 numerical columns, 1 for each star level, which allowed for a higher level of granularity in comparing ratings.
2. Ensuring Data Parity
   During the transition from Jupyter Notebooks to Power BI, a $0.01$ discrepancy in correlation coefficients was identified in the data. Power BI was aggregating duplicate product entries, slightly skewing the correlation. To fix this, I added the unique product id to the visual and modified the Python visual code to drop it from the visual, ensuring that no similar values were dropped. By forcing the visual to use the unique Product ID in the background, I preserved the raw data integrity and matched the Python output. 
3. Advanced Ranking & Tie-Breaking
   I was trying to add a standard Top-10 filter in Power BI to identify the top 10 best rated brands, struggling with the return of 11 brands instead of 10. I realized that this was likely due to a tie in ratings. My theory was confirmed after I wrote a custom DAX Ranking Measure using an alphabetical tie-breaker and applied it to the visual, ensuring a clean Top 10 ranking for the dashboard.

## Business Applications
If I were to present my findings to Walmart, I would suggest that they employ different discounting strategies depending on the category of the item. Products in the *food* and especially the *beauty* category responded much more positively to discounting strategies than other categories. Other categories, such as *home*, actually exhibited a small negative correlation ($r = -0.10$). I would recommend avoiding promotional spending on these categories, as customers seem to be more suspicious of price rollbacks for certain items. Additionally, I confirmed that there is a significantly higher average rating for the *home* category, which suggests that Walmart does not need to focus on increasing ratings in this particular category. 

## How to Run
1. Clone the repo: `git clone https://github.com/C0bb13/.github.io.git`
2. Install dependencies: `pip install pandas numpy seaborn matplotlib scipy tabulate statsmodels`
3. Open `WalmartProject.pbix` to view the dashboard or the Jupyter Notebook for the statistical deep-dive.
