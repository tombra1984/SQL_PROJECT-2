Question 1: find all duplicate records

SQL Queries:
-- # Find all duplicate data from all_sessions

DELETE FROM all_sessions
	WHERE fullvisitorid        --# fullvisitorid was used as it had unique identifiers which can apply all through table--
		IN (
			SELECT fullvisitorid 
			FROM all_sessions 
			GROUP BY fullvisitorid 
			HAVING COUNT (*) >1)
Answer: 



Question 2: find the total number of unique visitors (`fullVisitorID`)

SQL Queries:
--# use count as the column has already been cleaned of duplicates

SELECT COUNT (
   
    fullvisitorid
   
    ) 
FROM

all_sessions

Answer:13421



Question 3: find the total number of unique visitors by referring sites

SQL Queries:

--# visitid was used since it identifies the unique number of visits in the site

SELECT COUNT (visitid) 

FROM 

 a_all_sessions

Answer:
13421


Question 4: find each unique product viewed by each visitor

SQL Queries:

select name as productname, fullvisitorid as visitor --# idenitify columns to use. Fullvisitorid identifies the visitor.
from products as v2p                    
join a_all_sessions as p             #--inner join products table with a_all_sessions table
on p.productsku=v2p.sku           #--using the sku's ( a_all_sessions sku is same with product sku just named differently)
order by v2productname desc     #-- arrange the table in descending order by product name to get product name
Answer:

Product names
" Leatherette Notebook Combo"
"SPF-15 Slim & Slender Lip Balm"
" Infant Short Sleeve Tee Green"
"Badge Holder"
" Metallic Notebook Set"
"Spiral Notebook and Pen Set"
"22 oz Android Bottle"
"Red Shine 15 oz Mug"

Question 5: compute the percentage of visitors to the site that actually makes a purchase

SQL Queries:
select 
round(sum(transactions)*100.0/sum(pageviews),1) as percent  --#the sum of transactions on the site divided by number 
                                                            of pageviews multiplied by 100 rounded to a whole


from all_sessions                                           --- #table from which columns were extracted

where transactions >0
Answer: 7%
