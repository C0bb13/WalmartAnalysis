# Walmart Product Performance Analysis

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0-green.svg)](https://pandas.pydata.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow.svg)](https://powerbi.microsoft.com/)

## Project Overview
Walmart needs to understand the relationship between discount strategies and customer satisfaction (ratings) to optimize their promotional approach and improve customer loyalty. To help them solve this problem, I analyzed a dataset of Walmart products to examine the relationship between discount and ratings, as well as how the type of product moderates this relationship. I used Python for statistical validation and Power BI to assemble an interactive report that Walmart can use to guide their discount optimzation strategy.

## Technology Used
* Data Processing: Python (Pandas)
* Statistical Analysis: Scipy (ANOVA Testing), NumPy
* Visualization: Seaborn, Matplotlib, Power BI
* Analytics Engine: DAX (Data Analysis Expressions)

## Key Findings
* There is a very weak overall correlation between discount and ratings (*r* = 0.05).
* However, viewing product correlations by category reveals stronger correlations for Beauty (*r* = 0.31) and Food (*r* = 0.16) items.
* The highest rated brand is *Amay's*.
* The *home* category of items is significantly better rated than the other categories, especially *clothing* and *beauty*.

## Technical Challenges & Solutions
1. Parsing Dictionary Data
   While cleaning data in Python, I realized that the rating_stars column contained string-formatted dictionaries for the 5 star levels for each product. This prevented analysis of the ratings breakdown of each item. To get around this, I wrote a function which first attempted to converted the data into true dictionaries if they weren't already. Then I parsed the dictionary data into 5 numerical columns, 1 for each star level, which allowed for a higher level of granularity in comparing ratings.
2. Ensuring Data Parity
   During the transition from Jupyter Notebooks to Power BI, a $0.01$ discrepancy in correlation coefficients was identified in the data. Power BI was "row-folding" the data by default, removing data points it registered as identical. To fix this, I added the unique product id to the visual and modified the Python visual code to drop it from the visual, ensuring that no similar values were dropped.
3. Advanced Ranking & Tie-Breaking
   I was trying to add a standard Top-10 filter in Power BI to identify the top 10 best rated brands, struggling with the return of 11 brands instead of 10. I realized that this was likely due to a tie in ratings. My theory was confirmed after I wrote a custom DAX Ranking Measure using an alphabetical tie-breaker and applied it to the visual, ensuring a clean Top 10 ranking for the dashboard.
