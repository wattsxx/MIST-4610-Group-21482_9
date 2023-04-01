

# MIST4610 Group 21482_9

Group Project 1: Data Base and Model for New A Southern Based Workout Facility


## Authors

- [@wattsxx](https://www.github.com/wattsxx)
- [@Mikecwagner21](https://www.github.com/Mikecwagner21)
- [@Angeladc](https://www.github.com/Angeladc)
- [@josephgmurphy](https://www.github.com/josephgmurphy)
- [@nakulsajan](https://www.github.com/nakulsajan)
## Problem Description

Database for a Southern Based Workout Facility, *Apex Fitness*. The Database includes several entities to record information about Inventory, Locations, Employees, Shifts and Shift Details, Visits by customers, Classes offered at locations, the different Memberships available, infortmation about our Customers, Products and their Suppliers, and finally Orders placed by Customers. 

The Inventory entity records information about gym equipment per location. Some of this information includes quantity of specific machines, brand, model, and even cost and condition of the machine. 

The Locations entity records basic information for each of our locations, including address, phone, city, ect. The primary purpose of Locations is used in relationships with other entities to express things such as employees employed at a location, or what customers visit which location. 

The Employees entity records information on those employed at our facilities. We record vital information such as their name, job title, payrate, and even who they report to. We made this entity join onto itself so we could express those employees with employees that report to them. We also created this as a non-mandatory foreign key, allowing us the ability to leave reportsTo null in the case of a supervisor. Finally we give every employee their own ID which is used in tracking them within other entities. 

The Shift entity contains information about what shifts we have for all locations. This provides the start and end time for each shift. Shifts are identified by their primary key shiftID. 

The shiftDetails entity contains more specific information about the instances of a shift. We made this an associative/weak entity between Employees and Shift in order to track which employees are working each shift as well as how long the employee worked. We wanted to track this incase employees were working more than one shift, multiple shifts or less than a shift. This way allows us to track specific employees and the hours they worked to easily detemine their total hours. 

The Visit entity is an associative/weak entity between Customers and Location. We made this an identifying relationship as you cannot have a Visit without a Customer and a Location to Visit. We record data here such as which customer visited, what location, the time of the visit, and even the visit date. This allows us to know when are peak times of activity are, as well as what days may be more active than others. 

The Class entity is another associative/weak entity that is between the customer and an employee. This again is an identifying relationship because a class is held by an employee, and in the event that no customer would participate, the class would be cancelled. The Class entity allows us to store information about which employee is hosting the class, the customer that attends, a start and end time, a class title, and a classID. This allows us to store what classes we have available and create a schedule between the customer and the employee hosting the class. We can store when the class begins and ends, and what kinds of classes we have available. 

The Memberships entity shows which memberships we have available. We reccord a unique membershipID for each tier of membership, as well as each tiers respective information. Each membership has a name, platinum basic or gold, a monthly rate for the membership, and features that each member obtains for a certain tier of membership. This allows us to track what tier each customer is, and determine their level of access to unique features. 

The Customers entity records the customers name, phone, address, DOB, and their membershipID. This allows us to store basic information about the customer, and the customerID helps to idnetify the customer when using the Visit and Class entities.

The Products entity stores information about what food items we have available at our location. This is what sets us apart from every other gym, allowing the customer to purchase in house protein shakes and items instead of dealing with the troubles of making their own. It is super convenient to the customer, and convenience is a service customers will pay for. Outside of our reason for the addition of a in house menu, our products table includes basic information such as calories, flavor, quantity in stock, price, productID, and who its supplied by. We use this productID in order to track details on our orders from customers. 

The Orders entity is a associatve/weak entity between Products and Customer to determine which products they have ordered, and record data on the sale. This table records the date ordered, and the quantity of product ordered. This allows us to track which products we are selling the most of, as well as track what products specific customers buy more to further identify relationships between the customer and product. 

The ShopSuppliers entity simply records the suppliers infromation that provide our products. We reccord their name, address, and phone as well as creating a shopSupplierID. We use this shopSupplierID within Products to allow us to not only know where the products came from, but which suppliers products sell the best. 
## Data Model

![Data Model](https://github.com/wattsxx/GroupProjectDataModel/blob/main/GroupProjectDataModel.png)

## Data Dictionary


![Locations](https://github.com/wattsxx/Data-Dictionary/blob/main/Locations%20Table.png)

![Class](https://github.com/wattsxx/Data-Dictionary/blob/main/Class%20Table.png)

![Customers](https://github.com/wattsxx/Data-Dictionary/blob/main/Customers%20Table.png)

![Employees](https://github.com/wattsxx/Data-Dictionary/blob/main/Employees%20Table.png)

![Inventory](https://github.com/wattsxx/Data-Dictionary/blob/main/Inventory%20Table.png)

![Memberships](https://github.com/wattsxx/Data-Dictionary/blob/main/Membership%20Table.png)

![Orders](https://github.com/wattsxx/Data-Dictionary/blob/main/Orders%20Table.png)

![Products](https://github.com/wattsxx/Data-Dictionary/blob/main/Products%20Table.png)

![Shift](https://github.com/wattsxx/Data-Dictionary/blob/main/Shift%20Table.png)

![shiftDetails](https://github.com/wattsxx/Data-Dictionary/blob/main/shiftDetails%20Table.png)

![ShopSuppliers](https://github.com/wattsxx/Data-Dictionary/blob/main/Shop%20suppliers%20Table.png)

![Visit](https://github.com/wattsxx/Data-Dictionary/blob/main/Visit%20Table.png)


[Link](https://docs.google.com/document/d/1d1Kczm4RgS-gKGNEknKKuGpcYVNTDvc4p7c3umfHKIU/edit?usp=sharing)

## Ten Queries
TP_Q1()
SELECT employeeName, payRateHR, COUNT(classID) AS 'Number of Classes'
FROM Employees
JOIN Class ON Employees.employeeID = Class.Employees_employeeID
GROUP BY employeeName, payRateHR
ORDER BY COUNT(classID) DESC;


TP_Q2()
SELECT membershipType, COUNT(visitID)
FROM Membership
JOIN Customers ON Membership.membershipID = Customers.Membership_membershipID
JOIN Visit ON Customers.customerID = Visit.Customers_customerID
GROUP BY membershipType
ORDER BY COUNT(visitID) DESC;


TP_Q3()
SELECT supplierName
FROM ShopSuppliers
JOIN Products ON ShopSuppliers.shopSupplierID = Products.productSuppliedBy
JOIN Orders ON Products.productID = Orders.productID
GROUP BY supplierName
ORDER BY (SELECT SUM(productID*quantityOrdered) FROM Orders) DESC;


TP_Q4() 
SELECT AVG(productCalories) AS 'Average Calories'
FROM Products
JOIN Orders ON Products.productID = Orders.productID
JOIN Customers ON Orders.customerID = Customers.customerID
WHERE customerDOB BETWEEN '1993-03-30' AND '2003-03-30';


TP_Q5()
SELECT Employees.employeeID, employeeName, COUNT(DISTINCT shiftDate) as NumberofShifts
FROM Employees
JOIN shiftDetails ON Employees.employeeID = shiftDetails.employeeID
WHERE Employees.reportsTo = "200217"
GROUP BY Employees.employeeID
ORDER BY COUNT(DISTINCT shiftDate)
LIMIT 1;


TP_Q6()
SELECT DISTINCT(employeeName), jobTitle
FROM Employees
JOIN Class ON Employees.employeeID = Class.Employees_employeeID
WHERE NOT EXISTS(SELECT * FROM Class WHERE Employees.employeeID = Class.Employees_employeeID AND locationID = 1);


TP_Q7()
SELECT Customers.customerName
FROM Customers
JOIN Membership ON Customers.membershipID = Membership.membershipID
WHERE Membership.membershipType = "Basic" AND Customers.customerDOB BETWEEN "1970-1-1" AND "1990-1-1" AND Customers.customerName REGEXP "^B";


TP_Q8()
SELECT Products.productID, productFlavor, COUNT(receiptID) 
FROM Products
JOIN Orders ON Products.productID = Orders.productID
WHERE quantityOrdered > (SELECT AVG(quantityOrdered) FROM Orders WHERE Products.productID = Orders.productID)
GROUP BY Products.productID, productFlavor;


TP_Q9()
SELECT SUM(cost*quantity)
FROM Inventory 
WHERE machineCondition = "poor"
GROUP BY InventoryID;


TP_Q10()
SELECT SupplierName, 100*(SUM(productStock)/(SELECT SUM(productStock) FROM Products)) AS "Percentage of Stock"
FROM ShopSuppliers
JOIN Products ON ShopSuppliers.shopSupplierID = Products.productSuppliedBy
GROUP BY shopSupplierID;
