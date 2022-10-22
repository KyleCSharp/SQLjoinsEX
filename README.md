# SQLjoinsEX
/* joins: select all the computers from the products table:
using the products table and the categories table, return the product name and the category name */
 select products.name , Categories.name
 from products
 inner join categories
 on categories.CategoryID = products.CategoryID
 where categories.Name = 'computers';
/* joins: find all product names, product prices, and products ratings that have a rating of 5 */
 select products.name, products.price, reviews.Rating
 from products
 inner join reviews
 on reviews.ProductID = products.ProductID
 where reviews.rating = 5;
 
/* joins: find the employee with the most total quantity sold.  use the sum() function and group by */
select E.FirstName, E.LastName , sum(sales.Quantity) as sum
from sales
inner join employees AS E
on E.EmployeeID= sales.EmployeeID
group by E.EmployeeID
order by sum desc
-- THERARE 2 WITH THE SAME SALE SCORE 
LIMIT 2;
/* joins: find the name of the department, and the name of the category for Appliances and Games */
select departments.name as 'Department name' , categories.name as 'Category Name'
from departments
inner join categories on categories.DepartmentID = departments.DepartmentID
where categories.Name = 'Appliances' or 'Games';
-- not showing games
/* joins: find the product name, total # sold, and total price sold,
 for Eagles: Hotel California --You may need to use SUM() */
select products.name, sum(sales.quantity) as 'total sold', sum(sales.quantity * sales.PricePerUnit) as 'total money made'
from products
inner join sales on sales.ProductID = products.ProductID
where products.name ='Eagles: Hotel California';

/* joins: find Product name, reviewer name, rating, and comment on the Visio TV. (only return for the lowest rating!) */
select products.name, reviews.Reviewer as 'reviewer name', reviews.Rating, reviews.Comment as 'comment'
from products
inner join reviews on reviews.ProductID = products.ProductID
where Rating = 1 and products.name = 'Visio TV';

-- ------------------------------------------ Extra - May be difficult
/* Your goal is to write a query that serves as an employee sales report.
This query should return the employeeID, the employee's first and last name, the name of each product, how many of that product they sold */
select employees.EmployeeID, employees.FirstName, employees.LastName, products.name, sum(sales.Quantity) as 'total sold'
from sales
inner join employees on sales.EmployeeID = employees.EmployeeID
inner join products on products.ProductID = sales.ProductID
group by employees.EmployeeID, products.ProductID
order by sales.Quantity desc;
