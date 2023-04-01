
# *Apex Fitness*
## MIST4610 Group 21482_9

Group Project 1: Data Base and Model for a new and innovative Workout Facility, *Apex Fitness*


## Authors

- Ethan Watts      [@wattsxx](https://www.github.com/wattsxx)
- Michael Wagner   [@Mikecwagner21](https://www.github.com/Mikecwagner21)
- Angela Canales   [@Angeladc](https://www.github.com/Angeladc)
- Joe Murphy       [@josephgmurphy](https://www.github.com/josephgmurphy)
- Nakul Sajan      [@nakulsajan](https://www.github.com/nakulsajan)
## Problem Description

  When analyzing the current amenities that gyms today have to offer, we noticed a serious window of opportunity. Proper Diet and Calorie replenishment is vital in one’s journey to peak physical health, a need not met by today’s gym standard. This is why Apex Fitness chose to bring the nutrients to the customer, allowing them to reach their peak physical performance. Our model displays the necessary database and model for our Apex Fitness chain. We have created a model to allow us to track our statistics across nearly every branch imaginable. From Customers to Employees, Orders to Inventory, we are able to find every statistic and number needed to provide our customers with the best workout experience available. More specifically we have 12 separate entities, 4 of which are associative entities, tracking our main departments. We collect extensive data on inventory, customers, employees, products, and the services we provide. Through our 12 entities we collect information on each branch in the most efficient way possible, allowing us to cross compare data across multiple entities. You will find a few examples of the efficiency of our database in the queries mentioned below, which display the level of detail we record from our facilities. Through the use of our data model, data base, and ability to query, we are able to provide an Apex level experience to our customers. 


## Data Model

![Data Model](https://github.com/wattsxx/GroupProjectDataModel/blob/main/GroupProjectDataModel.png)

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


## Ten Queries
TP_Q1()
SELECT employeeName, payRateHR, COUNT(classID) AS 'Number of Classes'
FROM Employees
JOIN Class ON Employees.employeeID = Class.Employees_employeeID
GROUP BY employeeName, payRateHR
ORDER BY COUNT(classID) DESC;

Description Q1: This query identifies the names and pay rates of all employees who have taught classes, along with the number of classes they have taught from most to least. From a managerial perspective, one would need this query to identify the performance and efforts of those employees who teach classes, guided by the number of classes taught. We can identify if the top-performing employees are getting fair enough compensation, and guide a few pay rate decisions through this data. 

TP_Q2()
SELECT membershipType, COUNT(visitID)
FROM Membership
JOIN Customers ON Membership.membershipID = Customers.Membership_membershipID
JOIN Visit ON Customers.customerID = Visit.Customers_customerID
GROUP BY membershipType
ORDER BY COUNT(visitID) DESC;

Description Q2: This query identifies which membership type makes up the most visits compared to the others. This could be useful in terms of identifying which memberships are the most popular among the most active members, helpful with deciding new marketing strategies for certain memberships or maybe even thinking about providing price deals or discounts on these memberships. 

TP_Q3()
SELECT supplierName
FROM ShopSuppliers
JOIN Products ON ShopSuppliers.shopSupplierID = Products.productSuppliedBy
JOIN Orders ON Products.productID = Orders.productID
GROUP BY supplierName
ORDER BY (SELECT SUM(productID*quantityOrdered) FROM Orders) DESC;

Description Q3: This query determines which of the suppliers products are the most to least popular. This will be helpful in determining which products to keep ordering from our suppliers and keep our shop stocked on these items to help build and maintain customer loyalty.

TP_Q4() 
SELECT AVG(productCalories) AS 'Average Calories'
FROM Products
JOIN Orders ON Products.productID = Orders.productID
JOIN Customers ON Orders.customerID = Customers.customerID
WHERE customerDOB BETWEEN '1993-03-30' AND '2003-03-30';

Description Q4: This query returns the average amount of Calories consumed within all orders made by customers between the ages of 20-30. If we know the eating habits of an important generational cohort such as 20 year olds, we can order/make better products that better suit their needs. Additionally, we can market more aggressively products with an amount of Calories that this age group tends to like.

TP_Q5()
SELECT Employees.employeeID, employeeName, COUNT(DISTINCT shiftDate) as NumberofShifts
FROM Employees
JOIN shiftDetails ON Employees.employeeID = shiftDetails.employeeID
WHERE Employees.reportsTo = "200217"
GROUP BY Employees.employeeID
ORDER BY COUNT(DISTINCT shiftDate)
LIMIT 1;

Description Q5: This query identifies which employee has worked the most shifts reporting to a certain location manager, which in this case is employeeID 200217. This is important from a managerial perspective because we can determine which employees are eligible for full-time or stay in part-time positions depending on the shifts worked.

TP_Q6()
SELECT DISTINCT(employeeName), jobTitle
FROM Employees
JOIN Class ON Employees.employeeID = Class.Employees_employeeID
WHERE NOT EXISTS(SELECT * FROM Class WHERE Employees.employeeID = Class.Employees_employeeID AND locationID = 1);

Description Q6: This query identifies the names of all employees who have not taught any classes at a particular location. We can choose from any location to pull this data out of. From a managerial perspective, this data could be useful in terms of resource allocation planning. If an excessive amount of employees have not taught classes at a location, resources could be allocated to help these employees start teaching and maybe decide to open up more class offerings within that location, instead of putting them towards those where many have taught. 

TP_Q7()
SELECT Customers.customerName
FROM Customers
JOIN Membership ON Customers.membershipID = Membership.membershipID
WHERE Membership.membershipType = "Basic" AND Customers.customerDOB BETWEEN "1970-1-1" AND "1990-1-1" AND Customers.customerName REGEXP "^B";

Description Q7: This query relays the names of customers that have the “basic” membership and were also born between 1970 and 1990. This could be helpful when working for a gym as we are able to specify the membership type of the customer while simultaneously finding out both date of birth and alphabetically finding the name. If someone was working at the front desk and working with a customer, the system would be able to verify that the person was a member and let them in.

TP_Q8()
SELECT Products.productID, productFlavor, COUNT(receiptID) 
FROM Products
JOIN Orders ON Products.productID = Orders.productID
WHERE quantityOrdered > (SELECT AVG(quantityOrdered) FROM Orders WHERE Products.productID = Orders.productID)
GROUP BY Products.productID, productFlavor;

Description Q8: This query lists the number of orders for a certain product that contains a larger quantity purchased than the average for that product. This could be useful from a managerial perspective because it can determine which products are above average on the popularity spectrum. We could work on price deals for these popular products and new marketing strategies for them.

TP_Q9()
SELECT SUM(cost*quantity)
FROM Inventory 
WHERE machineCondition = "poor"
GROUP BY InventoryID;

Description Q9: In any gym the equipment will eventually wear down due to use, and will end up costing the business some money. Gym equipment is something that also needs to be replaced and knowing how much money that could potentially send them back is important. With this, knowing which equipment could potentially go bad in the nearby future is also important in planning ahead for anything that may come up.

TP_Q10()
SELECT SupplierName, 100*(SUM(productStock)/(SELECT SUM(productStock) FROM Products)) AS "Percentage of Stock"
FROM ShopSuppliers
JOIN Products ON ShopSuppliers.shopSupplierID = Products.productSuppliedBy
GROUP BY shopSupplierID;

Description Q10: This query details the makeup of the company’s products. It returns the name of each supplier and the percentage of total products in stock that those companies’ products account for. The idea behind this query from a manager’s perspective is that it is important to know where our products come from. If we know the suppliers of our products and their contributions to our company, we can better the relationships that we most depend on. 

## The Matrix

![Matrix](https://github.com/wattsxx/The-Matrix/blob/main/The%20Matrix.png)
