## :rocket: [Module 02](https://github.com/Data-Learn/data-engineering/blob/master/DE-101%20Modules/Module02/readme.md) Databases and SQL 
- [Loading data](#loading-data)
- [Requests - output of metrics](#requests-output-metrics)
- [Data models](#data-models)
- [CREATE TABLE](#create-table)
- [INSERT INTO](#insert-into)

### :heavy_check_mark: Loading data <a name="loading-data"></a>
- [x] Loading 'orders'
```
DROP TABLE IF EXISTS orders;
CREATE TABLE orders(
   Row_ID        INTEGER NOT NULL PRIMARY KEY 
  ,Order_ID      VARCHAR(14) NOT NULL
  ,Order_Date    DATE NOT NULL
  ,Ship_Date     DATE NOT NULL
  ,Ship_Mode     VARCHAR(14) NOT NULL
  ,Customer_ID   VARCHAR(8) NOT NULL
  ,Customer_Name VARCHAR(22) NOT NULL
  ,Segment       VARCHAR(11) NOT NULL
  ,Country       VARCHAR(13) NOT NULL
  ,City          VARCHAR(17) NOT NULL
  ,State         VARCHAR(20) NOT NULL
  ,Postal_Code   INTEGER 
  ,Region        VARCHAR(7) NOT NULL
  ,Product_ID    VARCHAR(15) NOT NULL
  ,Category      VARCHAR(15) NOT NULL
  ,SubCategory   VARCHAR(11) NOT NULL
  ,Product_Name  VARCHAR(127) NOT NULL
  ,Sales         NUMERIC(9,4) NOT NULL
  ,Quantity      INTEGER NOT NULL
  ,Discount      NUMERIC(4,2) NOT NULL
  ,Profit        NUMERIC(21,16) NOT NULL
);
set datestyle to 'ISO, MDY';
INSERT INTO orders(Row_ID,Order_ID,Order_Date,Ship_Date,Ship_Mode,Customer_ID,Customer_Name,Segment,Country,City,State,Postal_Code,Region,Product_ID,Category,SubCategory,Product_Name,Sales,Quantity,Discount,Profit) VALUES (1,'CA-2018-152156','11/08/2018','11/11/2018','Second Class','CG-12520','Claire Gute','Consumer','United States','Henderson','Kentucky',42420,'South','FUR-BO-10001798','Furniture','Bookcases','Bush Somerset Collection Bookcase',261.96,2,0,41.9136);
INSERT INTO orders(Row_ID,Order_ID,Order_Date,Ship_Date,Ship_Mode,Customer_ID,Customer_Name,Segment,Country,City,State,Postal_Code,Region,Product_ID,Category,SubCategory,Product_Name,Sales,Quantity,Discount,Profit) VALUES (2,'CA-2018-152156','11/08/2018','11/11/2018','Second Class','CG-12520','Claire Gute','Consumer','United States','Henderson','Kentucky',42420,'South','FUR-CH-10000454','Furniture','Chairs','Hon Deluxe Fabric Upholstered Stacking Chairs, Rounded Back',731.94,3,0,219.582);
...
...
```
- [x] Loading 'people'
```
DROP TABLE IF EXISTS people;
CREATE TABLE people(
   Person VARCHAR(17) NOT NULL PRIMARY KEY
  ,Region VARCHAR(7) NOT NULL
);
INSERT INTO people(Person,Region) VALUES ('Anna Andreadi','West');
INSERT INTO people(Person,Region) VALUES ('Chuck Magee','East');
INSERT INTO people(Person,Region) VALUES ('Kelly Williams','Central');
INSERT INTO people(Person,Region) VALUES ('Cassandra Brandow','South');
```
- [x] Loading 'returns'
```
DROP TABLE IF EXISTS returns;
CREATE TABLE returns(
   Returned   VARCHAR(10) NOT NULL
  ,Order_id   VARCHAR(25) NOT NULL
);
INSERT INTO returns(Returned,Order_id) VALUES ('Yes','CA-2016-100762');
INSERT INTO returns(Returned,Order_id) VALUES ('Yes','CA-2016-100762');
...
...
```

### :heavy_check_mark: Requests - output of metrics <a name="requests-output-metrics"></a>
- [x] Total Sales, Total Profit, Profit Ratio, Profit per Order, Avg. Discount
```
SELECT
	round(sum(sales)) AS total_sales,
	round(sum(profit)) AS total_profit,
	round(sum(profit)/ sum(sales)* 100) AS profit_ratio,
	round(sum(profit)/ count(order_id)) AS profit_per_order,
	round(AVG(discount)* 100) AS avg_discount
FROM orders
```
- [x] Sales per Customer, Profit per Customer
```
SELECT
	customer_name,
	round(sum(sales)) AS customer_sales,
	round(sum(profit)) AS customer_total
FROM orders
GROUP BY customer_name
ORDER BY
	customer_sales DESC,
	customer_total DESC
```
- [x] Sales per region
```
SELECT
	region,
	round(sum(sales)) AS region_sales
FROM orders
GROUP BY region
ORDER BY region_sales DESC
```
- [x] Monthly Sales by Segment
```
SELECT
	segment,
	round(sum(sales)) AS montly_sales_segment
FROM orders
GROUP BY segment
ORDER BY montly_sales_segment DESC
```
- [x] Monthly Sales by Product Category
```
SELECT
	category,
	round(sum(sales)) AS montly_sales_category
FROM orders
GROUP BY category
ORDER BY montly_sales_category DESC
```
### :heavy_check_mark: Data Models <a name="data-models"></a>

### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Conceptual data model 

<img title="Conceptual data model" src="/module-02/Conceptual data model.png">    


### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Physical data model 

<img title="Physical data model" src="/module-02/Physical data model.png">    

### :heavy_check_mark: CREATE TABLE <a name="create-table"></a>
```
CREATE TABLE shipping
(ship_id   serial primary key NOT NULL,
 ship_mode varchar(15) NOT NULL);
```
```
CREATE TABLE person
(person_id   serial primary key NOT NULL,
 person_name varchar(50) NOT NULL);
```
```
CREATE TABLE customer
(customer_id   varchar(10) NOT NULL,
 customer_name varchar(50) NOT NULL,
 segment       varchar(20) NOT NULL);
```
```
CREATE TABLE product
(product_id   varchar(20) NOT NULL,
 product_name varchar(150) NOT NULL,
 category     varchar(20) NOT NULL,
 sub_category varchar(20) NOT NULL);
```
```
CREATE TABLE order_item
(order_item_id  serial primary key NOT NULL,
 product_id     varchar(20) NOT NULL,
 order_quantity int NOT NULL,
 sales          numeric(9,4) NOT NULL,
 discount       numeric(4,2) NOT NULL,
 profit         numeric(21,16) NOT NULL,
 order_id       varchar(30) NOT NULL);
```
```
CREATE TABLE geography
(geo_id      serial primary key NOT NULL,
 country     varchar(20) NOT NULL,
 person_id   int NOT NULL,
 region      varchar(20) NOT NULL,
 state       varchar(20) NOT NULL,
 city        varchar(20) NOT NULL,
 postal_code varchar(10) NULL);
```
```
CREATE TABLE returned_status
(order_item_id int NOT NULL,
 returned      boolean NOT NULL);
```
```
CREATE TABLE orders_all
(order_id      varchar(30) NOT NULL,
 order_date    date NOT NULL,
 ship_date     date NOT NULL,
 geo_id        int NOT NULL,
 ship_id       int NOT NULL,
 customer_id   varchar(10) NOT NULL);
```
### :heavy_check_mark: INSERT INTO <a name="insert-into"></a>
```
INSERT INTO shipping (ship_mode)
SELECT DISTINCT ship_mode
FROM orders;
```
```   
INSERT INTO person (person_name)
SELECT DISTINCT person
FROM people;
```   
```   
INSERT INTO customer (
		customer_id,
		customer_name,
		segment)
SELECT
	DISTINCT customer_id,
	customer_name,
	segment
FROM orders;
```   
```   
INSERT INTO product (
		product_id,
		product_name,
		category,
		sub_category)
SELECT
	DISTINCT product_id,
	product_name,
	category,
	subcategory
FROM orders;
```   
```   
INSERT INTO geography (
		country,
		person_id,
		region,
		state,
		city,
		postal_code)
SELECT
	country,
	person_id,
	orders.region,
	state,
	city,
	postal_code
FROM orders
JOIN people ON orders.region = people.region
JOIN person ON person.person_name = people.person
GROUP BY
	postal_code,
	orders.country,
	person_id,
	orders.region,
	orders.state,
	orders.city;
 ```  
 ```  
INSERT INTO order_item (
		product_id,
		order_quantity,
		sales,
		discount,
		profit,
		order_id)
SELECT
	product_id,
	quantity,
	sales,
	discount,
	profit,
	order_id
FROM orders
ORDER BY order_id;
```   
```   
INSERT INTO orders_all (
		order_id,
		order_date,
		ship_date,
		geo_id,
		ship_id,
		customer_id)
SELECT
	orders.order_id,
	orders.order_date,
	orders.ship_date,
	geo_id,
	ship_id,
	orders.customer_id
FROM orders
JOIN geography ON orders.postal_code = geography.postal_code
JOIN shipping ON orders.ship_mode = shipping.ship_mode
JOIN customer ON orders.customer_id = customer.customer_id
GROUP BY
	orders.order_id,
	orders.order_date,
	orders.ship_date,
	geo_id,
	ship_id,
	orders.customer_id
ORDER BY order_id;
```
