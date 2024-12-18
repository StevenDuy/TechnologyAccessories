# Technology Accessories Store Database

This README file provides instructions for creating the database for the Technology Accessories Store Sales Management System.

## Prerequisites

- SQL Server 2012 or later
- SQL Server Management Studio (SSMS) or any other SQL client tool

## Instructions

Follow these steps to create the `TechnologyAccessories` database and its tables.

### Step 1: Create the Database

Run the following SQL script to create the `TechnologyAccessories` database:

```sql
CREATE DATABASE TechnologyAccessories;
```

### Step 2: Use the Created Database

Select the newly created database to perform further operations:

```sql
USE TechnologyAccessories;
```

### Step 3: Create the Tables

Run the following SQL script to create the necessary tables: `Customer`, `Employee`, `Product`, and `Order`.

```sql
-- Create Customer table
CREATE TABLE Customer (
    CustomerID INT PRIMARY KEY IDENTITY(1,1),
    Name VARCHAR(50),
    Address VARCHAR(50),
    Phone VARCHAR(50)
);

-- Create Employee table
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY IDENTITY(1,1),
    EmployeeName VARCHAR(50),
    EmployeeRole VARCHAR(50),
    EmployeeAddress VARCHAR(255),
    EmployeePhone VARCHAR(15)
);

-- Create Product table
CREATE TABLE Product (
    ProductID INT PRIMARY KEY IDENTITY(1,1),
    ProductName VARCHAR(100),
    Quantity INT,
    Price DECIMAL(10, 2)
);

-- Add an image file column to the Product table
ALTER TABLE Product
ADD ImageFile VARBINARY(MAX);

-- Add username and password columns to the Employee table
ALTER TABLE Employee
ADD Username VARCHAR(50),
    Password VARCHAR(50);

-- Create Order table
CREATE TABLE [Order] (
    OrderID INT PRIMARY KEY IDENTITY(1,1),
    OrderProductID INT,
    OrderProductName VARCHAR(100),
    OrderCustomerID INT,
    OrderCustomerName VARCHAR(50),
    OrderEmployee VARCHAR(50),
    OrderDate DATE,
    OrderAmount INT,
    OrderPrice DECIMAL(10, 2),
    OrderBill DECIMAL(10, 2),
    FOREIGN KEY (OrderProductID) REFERENCES Product(ProductID),
    FOREIGN KEY (OrderCustomerID) REFERENCES Customer(CustomerID)
);
```

### Step 4: Change the Connection String in Code

To connect your application to the database, update the connection string in your code. Here’s an example connection string:

```csharp
string connectionString = "Data Source=YOUR_SERVER_NAME;Initial Catalog=TechnologyAccessories;Integrated Security=True";
```

Replace `YOUR_SERVER_NAME` with the name of your SQL Server instance.

### How to Obtain the Connection String Path in SSMS

1. Open SQL Server Management Studio (SSMS).
2. Connect to your SQL Server instance.
3. In the Object Explorer, right-click on your server name.
4. Select "Properties".
5. In the "Server Properties" window, look for the "Connection String" in the "General" section.

Alternatively, you can use the "Connect" dialog in SSMS to find the connection string:
1. In SSMS, go to "File" > "Connect Object Explorer".
2. Fill in the "Server name" with your SQL Server instance name.
3. Choose the authentication method and provide the necessary credentials.
4. Click "Connect".
5. The "Server name" field in this dialog represents the `Data Source` part of your connection string.

For detailed instructions, refer to the official guide from Microsoft: [Connect and query SQL Server using SSMS - Microsoft Learn](https://learn.microsoft.com/en-us/sql/ssms/quickstarts/ssms-connect-query-sql-server?view=sql-server-ver16).

### Summary

1. **Create Database**: The script creates a new database named `TechnologyAccessories`.
2. **Use Database**: The script switches to the `TechnologyAccessories` database for subsequent operations.
3. **Create Tables**: The script creates four main tables: `Customer`, `Employee`, `Product`, and `Order`. It also modifies the `Product` and `Employee` tables to add additional columns as needed.
4. **Change Connection String in Code**: Update your application’s connection string in the code to connect to the `TechnologyAccessories` database.
5. **Obtain Connection String Path in SSMS**: Use SQL Server Management Studio to find your server's connection string. Follow the official guide from Microsoft for detailed instructions.

### Note

This project is an academic exercise and is intended for reference purposes only.
