# Домашнее задание для курса [Analytics Engineering](https://github.com/Data-Learn/data-engineering/blob/master/DE%20-%20101%20Guide.md)



## :rocket: [Модуль 02](https://github.com/Data-Learn/data-engineering/blob/master/DE-101%20Modules/Module02/readme.md) Базы данных и SQL


## :ledger: Содержание
- [Загрузка данных](#загрузка-данных)
- [Создание таблиц - вывод метрик](#создание-таблиц)

## :heavy_check_mark: Загрузка данных <a name="загрузка-данных"></a>
- [x] Загрузка orders
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
- [x] Загрузка people
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
- [x] Загрузка returns
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

## :heavy_check_mark: Создание таблиц - вывод метрик <a name="создание-таблиц"></a>
- [x] Total Sales, Total Profit, Profit Ratio, Profit per Order, Avg. Discount
```
select 
round(sum(sales)) as total_sales, 
round(sum(profit)) as total_profit,
round(sum(profit)/sum(sales)*100) as profit_ratio,
round(sum(profit)/count(order_id)) as profit_per_order,
round(AVG(discount)*100) as avg_discount
from orders
```
- [x] Sales per Customer, Profit per Customer
```
select 
customer_name,
round(sum(sales)) as customer_sales,
round(sum(profit)) as customer_total
from orders
group by customer_name
order by customer_sales DESC, customer_total desc
```
- [x] Sales per region
```
select 
region,
round(sum(sales)) as region_sales
from orders
group by region 
order by region_sales DESC
```
- [x] Monthly Sales by Segment
```
select 
segment,
round(sum(sales)) as montly_sales_segment
from orders
group by segment
order by montly_sales_segment DESC
```
- [x] Monthly Sales by Product Category
```
select 
category,
round(sum(sales)) as montly_sales_category
from orders
group by category 
order by montly_sales_category DESC
```

