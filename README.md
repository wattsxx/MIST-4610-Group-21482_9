# MIST-4610-Group-21482_9
Group Project 1: Data Base and Model for New A Southern Based Workout Facility


# MIST4610 Group 21482_9

Group Project 1: Data Base and Model for New A Southern Based Workout Facility


## Authors

- [@wattsxx](https://www.github.com/wattsxx)
- [@Mikecwagner21](https://www.github.com/Mikecwagner21)
- [@Angeladc](https://www.github.com/Angeladc)
- [@josephgmurphy](https://www.github.com/josephgmurphy)
- [@nakulsajan](https://www.github.com/nakulsajan)
## Problem Description

Database for a Southern Based Workout Facility, *INSERT NAME OF GYM HERE*. The Database includes several entities to record information about Inventory, Locations, Employees, Shifts and Shift Details, Visits by customers, Classes offered at locations, the different Memberships available, infortmation about our Customers, Products and their Suppliers, and finally Orders placed by Customers. 

The Inventory entity records information about gym equipment per location. Some of this information includes quantity of specific machines, brand, model, and even cost and condition of the machine. 

The Locations entity records basic information for each of our locations, including address, phone, city, ect. The primary purpose of Locations is used in relationships with other entities to express things such as employees employed at a location, or what customers visit which location. 

The Employees entity records information on those employed at our facilities. We record vital information such as their name, job title, payrate, and even who they report to. We made this entity join onto itself so we could express those employees with employees that report to them. We also created this as a non-mandatory foreign key, allowing us the ability to leave reportsTo null in the case of a supervisor. Finally we give every employee their own ID which is used in tracking them within other entities. 

The Shift entity contains information about what shifts we have for all locations. This provides the start and end time for each shift. Shifts are identified by their primary key shiftID. 
## Data Model

*INSERT SCREEN SHOT OF DATA MODEL HERE*
## Data Dictionary

*INSERT SCREEN SHOT OF DATA DICTIONARY HERE*
## Ten Queries

