# 🧹 Data Cleaning with MySQL: Layoffs Dataset

## 📌 Project Overview
This project demonstrates **data cleaning techniques** applied to a messy layoffs dataset using **MySQL**. The main goal was to prepare the dataset for further analysis by:
- Removing duplicates
- Handling missing values
- Standardizing text formatting
- Ensuring consistency in numerical columns

## 🗂️ Folder Structure


## 🛠️ Tools Used
- **MySQL** for writing and executing SQL queries.
- **GitHub** for version control and project hosting.

## 💡 Key Steps in Data Cleaning
1. **Removing Duplicates**
   - Used `ROW_NUMBER()` to identify and remove duplicate rows based on key fields (`company`, `location`, `industry`, etc.).
2. **Handling Missing Data**
   - Replaced null values with appropriate defaults or dropped incomplete rows.
3. **Standardizing Text**
   - Unified text formats for columns like `Industry` and `Stage`.
4. **Cleaning Numerical Fields**
   - Fixed inconsistent numerical values and converted text-based numbers to integers.

## 📊 Example Queries
Below is a snippet of the SQL queries used in this project. Full details are available in `Layoffs_Data_Cleaning.sql`.

```sql
-- Identify and remove duplicates
WITH duplicate_cte AS (
  SELECT *,
         ROW_NUMBER() OVER (PARTITION BY company, location, industry 
                            ORDER BY total_laid_off DESC) AS row_num
  FROM layoffs_data
)
DELETE FROM layoffs_data
WHERE row_num > 1;

-- Handle missing values in "total_laid_off" column
UPDATE layoffs_data
SET total_laid_off = 0
WHERE total_laid_off IS NULL;

-- Standardize text in the "industry" column
UPDATE layoffs_data
SET industry = UPPER(industry);
