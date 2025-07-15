# 🧹 Layoffs EDA Project Using SQL

This project performs end-to-end Data Cleaning and Exploratory Data Analysis (EDA) on global layoffs data using MySQL.

The project was inspired and structured based on tutorials by Alex The Analyst:
- [Data Cleaning in SQL](https://www.youtube.com/watch?v=4UltKCnnnTA)
- [Exploratory Data Analysis in SQL](https://www.youtube.com/watch?v=QYd-RtK58VQ)

## 🛠️ Tools Used
- MySQL
- SQL Workbench / DBeaver / VS Code (any compatible IDE)
- Raw CSV Data (uploaded to a local MySQL database)

## 📊 Project Overview
The goal of this project is to clean, standardize, and analyze layoffs data to uncover insights such as:
- Which companies had the highest number of layoffs
- Trends in layoffs over time (year/month)
- Industry and location-based breakdowns
- Companies with 100% workforce reduction
- Impact of funding and growth stage on layoffs

## 🧼 Data Cleaning Process
- Removed duplicate records
- Trimmed and standardized text fields
- Standardized inconsistent country names (e.g., "United States.")
- Converted date strings into DATE format
- Populated missing industry values using available duplicate rows
- Removed irrelevant or empty records

📄 Cleaning logic is documented in: `Portfolio Project.sql`

## 🔎 EDA Highlights
- Company-wise total layoffs
- Yearly and monthly layoff trends
- Layoffs by industry, country, and funding stage
- Outlier detection (e.g., 100% layoffs)

📄 EDA queries are documented in: `Portfolio Project-1.sql`

## 📁 Files
- `Portfolio Project.sql` → Data Cleaning SQL Script
- `Portfolio Project-1.sql` → EDA SQL Script

## 📌 Outcomes
This project improved my SQL proficiency and provided real-world experience with data wrangling and business trend analysis using structured query language. It serves as a portfolio piece demonstrating my ability to prepare and analyze messy real-world datasets.

## 🚀 Future Scope
- Visualize trends in Power BI or Tableau
- Automate monthly reports using SQL + Python

---

🔗 Let me know your thoughts or suggestions in the Issues tab. Contributions are welcome!
