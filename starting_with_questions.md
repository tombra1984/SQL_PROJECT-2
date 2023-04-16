Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
-- # identify columns needed and what table they belong 

SELECT 
	city, 
	country, 
	SUM(totaltransactionrevenue)/1000000 as TTR 
FROM 
	a_all_sessions 
         
-- # put in conditons to get the best answer

where (
	totaltransactionrevenue is not null)
and
(
	city!= 'not available in demo dataset' and city!='(not set)' )

-- # Group by the necessary variables in this case country and city

GROUP BY 
	country,city

-- # Arrange the data to return in decending order
ORDER BY
	TTR DESC


Answer:

Answer: "San Francisco" "UNITED STATES" "1564"



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

--# identify columns needed and what table they belong 

SELECT 
a.country, 
a.city, 
AVG(orderedquantity) as average     --# determine the average of the products ordered
FROM 
    a_all_sessions as a
JOIN products as p                  --# combine Tables that have the necessary columns
ON p.sku=a.productsku

--# Put in the conditions to get best possible answer without errors

where (
	orderedquantity is not null)
and
(
	city!= 'not available in demo dataset' and city!='(not set)' )

--# Group by the variables searched for

GROUP BY city, country, orderedquantity 
ORDER BY average DESC


Answer:

Mountain view, United States, 15170



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
--# Determine the columns necessary 

SELECT  v2productcategory as p_types, country, city
FROM a_all_sessions                                     --# Table that houses the desired columns

                                                        --# Put in conditions that streamline the dataset

where (
	v2productcategory is not null 
		and v2productcategory !='not available in demo dataset' 
			and v2productcategory!='(not set)'
			    and v2productcategory!= '${escCatTitle}'				
)
and
(
	city!= 'not available in demo dataset' and city!='(not set)' )

                                                        --# Group by the variables to be determined

GROUP BY country, city,v2productcategory

                                                        --# Arrange by product

ORDER BY p_types


Answer:
most products ordered are apparel related from the USA




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:


SELECT                                           --# identify the required columns                                        
p.name, 
city, 
SUM(total_ordered) AS total_quantity_ordered    --# Get the total products ordered
FROM a_all_sessions AS a

JOIN products as p                          --# Join products to get product name
on a.productsku=p.sku

JOIN sales_by_sku as s	                    --# Join sales_by_sku to get the amount of the product that was sold
on s.productsku=p.sku	
	
     WHERE                                  --# Define conditions to streamline results generated 
	   (
         name IS NOT NULL
AND country IS NOT NULL
AND city IS NOT NULL  
AND sku IS NOT NULL
AND total_ordered IS NOT NULL)
	 and
	(name != 'not available in demo dataset' and name!='(not set)'
AND country != 'not available in demo dataset' and country!='(not set)'
AND city != 'not available in demo dataset' and city!='(not set)'  
AND sku!= 'not available in demo dataset' and sku!= '(not set)'
)

GROUP BY city, name                         --# Group by the questioned variables 


ORDER BY total_quantity_ordered DESC        --# Ordered by the highest total quantity of a product ordered

Answer:
" 17oz Stainless Steel Sport Bottle", Sunnyvale,  334




**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

--# Determine the columns and Tables required 
SELECT b.city,b.country, a.revenue, a.revenue/1000000 AS city_revenue
From a_all_sessions AS b        

JOIN analytics as a             --# inner join on analytics
ON b.fullvisitorid=a.fullvisitorid 

where (                         --# put in conditions not to consider places with null values
	revenue is not null)
and
(
	city!= 'not available in demo dataset' and city!='(not set)')



GROUP BY a.revenue, b.city, b.country    --# Group by questioned variables 

Order by a.revenue DESC                   --# order by highest revenue 

