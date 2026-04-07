# Hat-Sale-Section-Analysis


This is an anonymized version of a real report that I presented to management which led to (X) stores changing their sale section pricing structure, and led to the segments monthly sales increasing by X%. 

The full report can be viewed [here](https://docs.google.com/document/d/13WyTioV-JLnFqsjsWH5RaKfD5tZsQBvFkX1OmZiTm1Y/edit?tab=t.0)

Tableau charts used in the report can be viewed [here](https://public.tableau.com/app/profile/jacob.perovich/viz/SaleSectionAnalysis/ProjectOverview)






```SQL
--This query also was used to,..... explain)... and create the ‘ClearanceSales’ Table
--First block cleans column names to proper names that SQL can read.
With cleaned_data as (
 
SELECT


DATE,
Ticket_id,
Location,
Payment_methods,
REPLACE(Product_Name, ' ', '_') AS Product_Name,
TRIM((REPLACE(REPLACE(Category, ' ', '_'), '/', ''))) AS Category,
Selling_Price,
Quantity,
Discount,
Tax,
Net_Sales
FROM
`jacobperovichportfolio.Portfolio_Data.Sales`
WHERE
Date BETWEEN '2024-01-01' AND '2025-12-31'


),




--filters for hat categories only and filters out product names that have a list price < $20 (but keeps instances where those products were discounted)
CATEGORIES AS(
SELECT
*
FROM
cleaned_data
WHERE
category IN ('SNAPBACK','ROPER','A_FRAME','BUCKET','HATS',
               'UNSTRUCTURED_ADJ','FITTED','FLEXONE_FITS','STRUCTURED_ADJ','VISOR')
 AND (
  product_name NOT IN(
    'Special_Product1', 'Special_Product2', 'Special_Product3')
   OR discount > 0)
  AND Net_sales > 17
)






SELECT
date,
location,
Product_name,
Category,
Payment_methods,
Ticket_Id,
Selling_price,
Quantity,
Discount,
tax,
Net_sales,
FROM CATEGORIES


WHERE
Net_Sales < (quantity * 42)




--orders resulting data by date
ORDER BY date

```
