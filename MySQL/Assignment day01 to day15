
use classicmodels;
select * from employees;
SELECT employeenumber, firstname, lastname
FROM employees
WHERE jobtitle = 'Sales Rep' AND reportsTo = 1102;

select * from products;
select distinct productLine from products where productLine like "%cars";
-- Case Statement
select * from customers;
select customerNumber, customerName, case
when country IN ("USA", "Canada") then "North America"
when country IN ("UK", "France", "Germany") then "Europe"
else "Other"
End as CustomerSegment from customers;
-- Group by
select * from orderdetails;
select productCode, sum(quantityOrdered) as total_ordered from orderdetails group by productCode order by total_ordered desc limit 10;
select * from payments;
select monthname(paymentDate) as payment_month, count(*) as num_payments from payments group by monthname(paymentDate) having num_payments > 20;
-- Constraints
create database Customers_Orders;
use Customers_Orders;
create table Customers (customer_id int primary key auto_increment,
						first_name varchar(50) NOT NULL,
                        last_name varchar(50) NOT NULL,
                        email varchar(255) Unique,
                        phone_number varchar(20));
create table Orders (order_id int primary key auto_increment,
                     customer_id int,
                     order_date DATE,
                     total_amount decimal(10,2),
                     FOREIGN KEY (customer_id) REFERENCES Customers(Customer_id),
                     CHECK(total_amount >=0));
 -- Joins
 select * from customers;
 select * from orders;
                        
 -- Self join
create table Project(EmployeeID int primary key auto_increment,
				     FullName varchar(50) NOT NULL,
                     Gender Enum ("Male", "Female"),
                     ManagerID int);
insert into Project values (1,"Pranaya", "Male",3),
                            (2,"Priyanka", "Female",1),
                            (3,"Preety", "Female",null),
                            (4,"Anurag", "Male",1),
                            (5,"Sambit", "Male",1),
                            (6,"Rajesh", "Male",3),
                            (7,"Hina", "Female", 3);
select * from Project;
SELECT M.FullName AS ManagerName, E.FullName AS EmpName FROM Project E JOIN  project M ON E.ManagerID = M.EmployeeID;
-- DDL Command
create table Facility(Facility_ID int,
					  Name varchar(100),
                      State varchar(100),
                      Country varchar(100));
alter table Facility modify Facility_ID int primary key auto_increment;
alter table Facility add column City varchar(100) Not Null;
CREATE TABLE Facility_New (
    FacilityID INT PRIMARY KEY auto_increment,
    Name VARCHAR(100),
    City VARCHAR(100) NOT NULL, 
    State Varchar(100),
    Country varchar(100));
DROP TABLE Facility;
ALTER TABLE Facility_New RENAME TO Facility;
desc facility;
-- View
select* from productlines;
select * from orderdetails;
select * from orders;
CREATE VIEW product_category_sales AS
SELECT 	
    pl.productLine AS product_category,
    SUM(od.quantityOrdered * od.priceEach) AS total_sales,
    COUNT(DISTINCT o.orderNumber) AS number_of_orders
FROM orderdetails od
JOIN products p ON od.productCode = p.productCode
JOIN productlines pl ON p.productLine = pl.productLine
JOIN orders o ON od.orderNumber = o.orderNumber
GROUP BY pl.productLine;
select * from product_category_sales;
-- Stored Procedures
call Get_country_payments(2003, "France");
-- Window Functions
select* from customers;
select * from orders;
SELECT 
    c.customerName,
    COUNT(o.orderNumber) AS order_count,
    DENSE_RANK() OVER (ORDER BY COUNT(o.orderNumber) DESC) AS order_frequency_rnk
FROM Customers c
LEFT JOIN Orders o ON c.customerNumber = o.customerNumber
GROUP BY c.customerName
ORDER BY order_count DESC;


WITH MonthlyOrders AS (
    SELECT 
        YEAR(orderDate) AS Year,
        MONTHNAME(orderDate) AS Month,
        COUNT(orderNumber) AS Total_Orders
    FROM Orders
    GROUP BY Year, Month),
YoY_Calculation AS (
    SELECT 
           Year,
            Month,
			Total_Orders,
        LAG(Total_Orders) OVER (PARTITION BY Month ORDER BY Year) AS prev_year_order_count
    FROM MonthlyOrders)
SELECT 
          Year,
          Month,
          Total_Orders,
    CASE 
        WHEN prev_year_order_count IS NULL THEN "Null"
        ELSE CONCAT(ROUND((( - prev_year_order_count) / prev_year_order_count) * 100, 0), '%') 
    END AS  YoY_change
FROM YoY_Calculation
ORDER BY Year, 
    FIELD( Month, 'January', 'February', 'March', 'April', 'May', 'June', 
                      'July', 'August', 'September', 'October', 'November', 'December');

SELECT productLine,
    COUNT(*) AS Total
FROM Products
WHERE buyPrice > (SELECT AVG(buyPrice) FROM Products)
GROUP BY productLine order by Total desc;

create table Emp_EH (EmpID int primary key,
					  EmpName varchar(100),
                      EmailAddress varchar(255));
call InsertEmployee(1, "Joe", "joe.email@example.com");
-- Test Error Handling
call InsertEmployee(1,"Smith","Smith.email@example.com");
-- TRIGGERS (Before Insert)
CREATE TABLE Emp_BIT (Name VARCHAR(100),
                      Occupation VARCHAR(100),
                      Working_date DATE,
                      Working_hours INT);
                      
INSERT INTO Emp_BIT VALUES('Robin', 'Scientist', '2020-10-04', 12),  
                          ('Warner', 'Engineer', '2020-10-04', 10),  
                          ('Peter', 'Actor', '2020-10-04', 13),  
						  ('Marco', 'Doctor', '2020-10-04', 14),  
                          ('Brayden', 'Teacher', '2020-10-04', 12), 
                          ('Antonio', 'Business', '2020-10-04', 11);
-- Test Negative Value
INSERT INTO Emp_BIT VALUES ('Lucas', 'Pilot', '2020-10-04', -8);
select* from Emp_BIT;

