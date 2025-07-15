-- EDA : Exploratory Data Analysis 

-- Here we are jsut going to explore the data and find trends or patterns or anything interesting like outliers

-- normally when you start the EDA process you have some idea of what you're looking for

-- with this info we are just going to look around and see what we find!


SELECT * 
FROM world_layoffs.layoffs_staging2;

-- EASIER QUERIES

SELECT MAX(total_laid_off)
FROM world_layoffs.layoffs_staging2;

-- Which companies had 1 which is basically 100 percent of they company laid off
select MAX( percentage_laid_off), MIN(percentage_laid_off)
from layoffs_staging2
WHERE  percentage_laid_off IS NOT NULL;

-- these are mostly startups it looks like who all went out of business during this time
SELECT * 
FROM world_layoffs.layoffs_staging2
WHERE percentage_laid_off =1;

SELECT * 
FROM world_layoffs.layoffs_staging2
WHERE percentage_laid_off =1 AND country = 'india'; -- COUNTRY SPECIFIC 


-- if we order by funcs_raised_millions we can see how big some of these companies were
SELECT company, industry ,funds_raised_millions
FROM world_layoffs.layoffs_staging2
WHERE  percentage_laid_off = 1 -- 100% laid off
ORDER BY funds_raised_millions DESC;

SELECT company, industry ,funds_raised_millions,percentage_laid_off
FROM world_layoffs.layoffs_staging2
WHERE  percentage_laid_off like '0%' OR '1'-- may be not 100%  laid off
ORDER BY funds_raised_millions DESC;

SELECT *
FROM world_layoffs.layoffs_staging2
WHERE  percentage_laid_off = 1
ORDER BY funds_raised_millions DESC;
-- BritishVolt looks like an EV company, Quibi! I recognize that company - wow raised like 2 billion dollars and went under - ouch






-- SOMEWHAT TOUGHER AND MOSTLY USING GROUP BY--------------------------------------------------------------------------------------------------

-- Companies with the biggest single Layoff

SELECT company, total_laid_off
FROM layoffs_staging2
ORDER BY 2 DESC
LIMIT 5;
-- now that's just on a single day

-- Companies with the most 🔥🔥Total Layoffs -- like insight Amazon has highest total laid off.
SELECT company, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY company
ORDER BY 2 DESC
LIMIT 5;


-- by Industry/ Location
SELECT industry, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY industry
ORDER BY 2 DESC
LIMIT 10;

-- by Date
SELECT `date`, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY `date`
ORDER BY 1 DESC
;
-- this it total in the past 3 years or in the dataset
SELECT YEAR(`date`), SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY YEAR(`date`)
ORDER BY 1 DESC;

--  stage
SELECT stage, SUM(total_laid_off)
FROM layoffs_staging2
GROUP BY stage
ORDER BY 2 DESC
LIMIT 10;






-- TOUGHER QUERIES------------------------------------------------------------------------------------------------------------------------------------

-- Earlier we looked at Companies with the most Layoffs. Now let's look at that per year. It's a little more difficult.
-- I want to look at 
SELECT SUBSTRING(date,1,7) as dates, SUM(total_laid_off) AS total_laid_off
FROM layoffs_staging2
GROUP BY dates
ORDER BY dates ASC;

-- SHORTLISTING data based on date but only on monthly basis of 3 year combine may not be useful and effective for EDA
SELECT substring(`date`,6,2) as Months , SUM(total_laid_off)
FROM layoffs_staging2
where substring(`date`,6,2) is NOT NULL
GROUP BY Months
ORDER BY 1 ASC
;

-- Creating "Dates" column containing year-month which give clear data insight.ALTER

SELECT substring(`date`,1,7) as Dates, SUM(total_laid_off)
FROM layoffs_staging2
WHERE substring(`date`,1,7) IS NOT NULL
GROUP BY Dates
ORDER BY 1 ASC
;

-- now use it in a CTE so we can query off of it
-- Rolling total

