This is a snapshot of SQL used to retrieve data from PVFC(Pine Valley Furniture Company Database) dataset.

1. Using WHERE command to join tables and write a query to display Order_ID and Order_Date for all the orders made by customers in the territory of Southwest (i.e., Territory_Name= “Southwest”). 


SELECT ORDER_ID, ORDER_DATE
FROM ORDER_T A, CUSTOMER_T B, DOES_BUSINESS_IN_T C, TERRITORY_T D
WHERE A.CUSTOMER_ID = B.CUSTOMER_ID
AND B.CUSTOMER_ID = C.CUSTOMER_ID
AND C.TERRITORY_ID = D.TERRITORY_ID
AND D.TERRITORY_NAME ="SouthWest";


2. Using sub-query technique to write a SQL query to display Order_ID and Order_Date for all the orders made by customers in the territory of Southwest. 


SELECT ORDER_ID,ORDER_DATE 
FROM  ORDER_T A, CUSTOMER_T B, DOES_BUSINESS_IN_T C
WHERE A.CUSTOMER_ID = B.CUSTOMER_ID
AND B.CUSTOMER_ID = C.CUSTOMER_ID
AND C.TERRITORY_ID = (SELECT TERRITORY_ID FROM TERRITORY_T WHERE   TERRITORY_NAME='SouthWest');




3.	Identifying Product_ID and Product_Description for the products with a price larger than the price of the product “Computer Desk”? 

SELECT PRODUCT_ID, PRODUCT_DESCRIPTION
FROM PRODUCT_T
WHERE STANDARD_PRICE > (SELECT MAX(STANDARD_PRICE) FROM PRODUCT_T WHERE PRODUCT_DESCRIPTION = "COMPUTER DESK");

4.	Identifying Customer_Name(s) of the customers who have ordered the product with the largest price?

SELECT CUSTOMER_NAME
FROM CUSTOMER_T A, ORDER_T B, ORDER_LINE_T C, PRODUCT_T D
WHERE A.CUSTOMER_ID = B.CUSTOMER_ID
AND B.ORDER_ID = C.ORDER_ID
AND C.PRODUCT_ID = D.PRODUCT_ID
AND STANDARD_PRICE = (SELECT MAX(STANDARD_PRICE) FROM PRODUCT_T);


5.  Give 10% discount to all the products manufactured by the product line Scandinavia (i.e., Product_Line_Name= “Scandinavia”).  

Select Product_ID, Product_Description, Product_Finish,
 0.90* Standard_Price as Discounted_Price from Product_t as A
 where A.Product_Line_Id in  (Select B.Product_Line_ID
 from PRODUCT_LINE_t as B where Product_Line_Name ='Scandinavia');

