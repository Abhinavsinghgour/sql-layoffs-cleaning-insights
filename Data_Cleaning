select * 
from layoffs;


-- now when we are data cleaning we usually follow a few steps
-- 1. check for duplicates and remove any
-- 2. standardize data and fix errors
-- 3. Look at null values and see what 
-- 4. remove any columns and rows that are not necessary - few ways

CREATE TABLE layoffs_staging 
LIKE layoffs;

INSERT INTO layoffs_staging
SELECT * 
FROM layoffs;

SELECT * ,
ROW_NUMBER() OVER(PARTITION BY  company, location, industry, total_laid_off, percentage_laid_off,`date`,stage, country, funds_raised_millions) AS row_num
FROM layoffs_staging 
;



WITH duplicate_CTE AS
(
SELECT * ,
ROW_NUMBER() OVER(PARTITION BY  company, location, industry, total_laid_off, percentage_laid_off,`date`,stage, country, funds_raised_millions) AS row_num
FROM layoffs_staging 

)
SELECT *
FROM duplicate_CTE 
WHERE row_num >1;
;

DELETE
FROM layoffs_staging
Where company='Cazoo';


CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` INT
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


INSERT INTO layoffs_staging2
SELECT * ,
ROW_NUMBER() OVER(PARTITION BY  company, location, industry, total_laid_off, percentage_laid_off,`date`,stage, country, funds_raised_millions) AS row_num
FROM layoffs_staging;

select *
FROM layoffs_staging2
;

DELETE 
FROM layoffs_staging2
where row_num>1;

select *
FROM layoffs_staging2
where row_num>1
;


-- 2. standardize data and fix errors

select *
FROM layoffs_staging2
;


SELECT company , trim(company)
FROM layoffs_staging2
ORDER BY 1;

UPDATE layoffs_staging2
SET company= TRIM(company);

-- Checking indusryt Column

SELECT DISTINCT industry
FROM layoffs_staging2
ORDER BY 1;

SELECT *
FROM layoffs_staging2
where industry LIKE 'Crypto%';

UPDATE layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

-- For now we standardize industry column and for NULL and " " rows/values init we look at later phase. refer to line no.
-- checking location column....Answer it's perfect
-- checking country column. 
SELECT DISTINCT country
FROM layoffs_staging2
ORDER BY 1;

-- everything looks good except apparently we have some "United States" and some "United States." with a period at the end. Let's standardize this.
UPDATE layoffs_staging2
SET couNtry = TRIM(TRAILING '.' FROM country);

-- Let's also fix the date columns:
SELECT *
FROM world_layoffs.layoffs_staging2;

-- we can use str to date to update this field
UPDATE layoffs_staging2
set `date`= str_to_date(`date`, "%m/%d/%Y");

-- now we can convert the data type properly
ALTER TABLE layoffs_staging2
MODIFY COLUMN `date` DATE;

select  total_laid_off, percentage_laid_off
FROM layoffs_staging2
ORDER BY 1;

-- Checking industry null or ' ' 

SELECT *
FROM world_layoffs.layoffs_staging2
WHERE total_laid_off IS NULL
AND percentage_laid_off IS NULL;

-- Fetchig data where industry is null or " " to make it consistent or clear it.
 SELECT *
 from layoffs_staging2
 where industry is null OR industry = '';
 
 -- NOT NULL industry DATA: ABally's Interactive can not be made consistent but data like Carvana,Airbnb, juul can be made consistent because it has other non null industry data.
 SELECT *
 from layoffs_staging2
 where company like 'Airbnb%'
;
-- Setting every " "(Blank) value to null.
UPDATE  layoffs_staging2
SET industry = NULL
WHERE industry = '';

SELECT t1. industry,t2. industry
FROM layoffs_staging2 t1
join layoffs_staging2 t2
  ON t1.company= t2.company
WHERE t1. industry IS NULL
AND  t2. industry is NOT NULL;

-- Populating industry where Companies industry data is NULL and same company have different industry data in different field/row.
UPDATE layoffs_staging2 t1
JOIN layoffs_staging2 t2
  ON t1.company = t2.company
SET t1.industry = t2.industry
WHERE t1. industry IS NULL
AND  t2. industry is NOT NULL;

 -- checking wheater is data filled properly. -- See data is filled correctly in industries like Carvana,Airbnb, juul.
 SELECT *
 from layoffs_staging2
 where company like 'Airbnb%'
;
 SELECT *
 from layoffs_staging2;
 
 
 
-- 3. Look at Null Values

-- the null values in total_laid_off, percentage_laid_off, and funds_raised_millions all look normal. I don't think I want to change that
-- I like having them null because it makes it easier for calculations during the EDA phase

-- so there isn't anything I want to change with the null values




-- 4. remove any columns and rows we need to

SELECT *
FROM world_layoffs.layoffs_staging2
WHERE total_laid_off IS NULL;


SELECT *
FROM world_layoffs.layoffs_staging2
WHERE total_laid_off IS NULL
AND percentage_laid_off IS NULL;

-- Delete Useless data we can't really use
DELETE FROM world_layoffs.layoffs_staging2
WHERE total_laid_off IS NULL
AND percentage_laid_off IS NULL;

SELECT * 
FROM world_layoffs.layoffs_staging2;

-- Remove row_num column from TABLE (layoffs_staging2)
ALTER TABLE layoffs_staging2
DROP COLUMN row_num;

-- Finall table for EDA 
SELECT * 
FROM world_layoffs.layoffs_staging2;
 
 
 
 
 
 
