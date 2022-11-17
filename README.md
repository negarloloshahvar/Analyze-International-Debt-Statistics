# Analyze-International-Debt-Statistics

In this project, we are going to analyze international debt data collected by The World Bank. The dataset contains information about the amount of debt (in USD) owed by developing countries across several categories.

## Project Questions

we are going to find the answers to questions like:

- What is the total amount of debt that is owed by the countries listed in the dataset?
- Which country owns the maximum amount of debt and what does that amount look like?
- What is the average amount of debt owed by countries across different debt indicators?

The data used in this project is provided by The World Bank. It contains both national and regional debt statistics for several countries across the globe as recorded from 1970 to 2015.

## Project Tasks
### 1. The World Bank's international debt data

```
SELECT *
FROM international_debt
LIMIT 10;
```

### 2. Finding the number of distinct countries

```
SELECT COUNT(DISTINCT country_name)
    AS total_distinct_countries
FROM international_debt;
```

### 3. Finding out the distinct debt indicators

```
SELECT COUNT(DISTINCT country_name)
    AS total_distinct_countries
FROM international_debt;
```

### 4. Totaling the amount of debt owed by the countries

```
SELECT 
    ROUND(SUM(debt)/1000000 ,2)  AS total_debt
FROM international_debt; 
```

### 5. Country with the highest debt

```
SELECT 
    country_name,
    SUM(debt) AS total_debt
FROM international_debt
GROUP BY country_name
ORDER BY total_debt DESC
LIMIT 1;
```

### 6. Average amount of debt across indicators

```
SELECT 
    indicator_code AS debt_indicator,
    indicator_name,
    AVG(debt) AS average_debt
FROM international_debt
GROUP BY debt_indicator, indicator_name
ORDER BY average_debt DESC
LIMIT 10;
```

### 7. The highest amount of principal repayments
```
SELECT 
    country_name, 
    indicator_name
FROM international_debt
WHERE debt = (SELECT 
                 MAX(debt)
             FROM international_debt
             WHERE indicator_code = 'DT.AMT.DLXF.CD');
```

### 8. The most common debt indicator

```
SELECT
        indicator_code,
        COUNT(indicator_code) AS indicator_count
FROM international_debt
GROUP BY indicator_code
ORDER BY indicator_count DESC, indicator_code DESC
LIMIT 20;
```

### 9. Other viable debt issues and conclusion
```
SELECT country_name, MAX(debt) AS maximum_debt
FROM international_debt
GROUP BY country_name
ORDER BY maximum_debt DESC
LIMIT 10;
```

### Project Insights
We can see that the indicator DT.AMT.DLXF.CD tops the chart of average debt. This category includes repayment of long term debts.
An interesting observation in the above finding is that there is a huge difference in the amounts of the indicators after the second one. This indicates that the first two indicators might be the most severe categories in which the countries owe their debts.
China has the highest amount of debt in the long-term debt (DT.AMT.DLXF.CD) category. This is verified by The World Bank.
In this project, we took a look at debt owed by countries across the globe. We extracted a few summary statistics from the data and unraveled some interesting facts and figures. We also validated our findings to make sure the investigations are correct.
