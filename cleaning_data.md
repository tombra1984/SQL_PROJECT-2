What issues will you address by cleaning the data?
- Identify and delete if necessary replicated data from each table
- Identify missing values and extreme values




Queries:
-- #first identify the replicated rows in each table--

SELECT productsku, total_ordered 
FROM sales_by_sku
GROUP BY productsku,total_ordered
HAVING COUNT(*) > 1;


--#Delete the rows that have duplicates--


DELETE FROM sales_by_sku
WHERE productsku IN (
	SELECT productsku
    FROM sales_by_sku
    GROUP BY productsku, total_ordered
    HAVING COUNT(*) > 1
);


-- #To check for null values per table
SELECT * FROM sales_by_sku
WHERE productsku IS NULL OR total_ordered IS NULL;

--manipulate above query to determine null values in various tables