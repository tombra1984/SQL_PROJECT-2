What are your risk areas? Identify and describe them.
Risk areas include, empty columns, empty rows in various tables, Text in number fields


QA Process:

- Unit price evaluation in table
SELECT *, unit_price / '1000000' as d_unit_price
from analytics;

-Try to manually spot check for errors


- Drop columns that had no data

ALTER TABLE a_all_sessions
DROP COLUMN productrefundamount, 
DROP COLUMN productrevenue,
DROP COLUMN itemquantity,
DROP COLUMN itemrevenue
DROP COLUMN transactionrevenue; 



-Comparing row counts against average row value to identify outliers

SELECT COUNT(*) AS row_count, AVG(productrevenue) AS avg_value
FROM all_sessions