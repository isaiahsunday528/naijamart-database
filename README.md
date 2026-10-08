# naijamart-database
-- ================================================================
-- NAIJAMART DATABASE
-- ================================================================
DROP DATABASE IF EXISTS naijamart;
CREATE DATABASE IF NOT EXISTS naijamart;
USE naijamart;

SET FOREIGN_KEY_CHECKS = 0;
DROP TABLE IF EXISTS order_items;
DROP TABLE IF EXISTS orders;
DROP TABLE IF EXISTS products;
DROP TABLE IF EXISTS categories;
DROP TABLE IF EXISTS suppliers;
DROP TABLE IF EXISTS customers;
SET FOREIGN_KEY_CHECKS = 1;

-- # ---------------------------------------------------------------------- #
-- # Tables                                                                 #
-- # ---------------------------------------------------------------------- #
-- # ---------------------------------------------------------------------- #
-- # Add table "Customers"                                                 #
-- # ---------------------------------------------------------------------- #
-- 1. CUSTOMERS
CREATE TABLE customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100) NOT NULL,
    City VARCHAR(50) NOT NULL,
    Region VARCHAR(50) NOT NULL,
    Gender VARCHAR(20) NOT NULL,
    RegistrationDate DATE NOT NULL,
    CustomerStatus VARCHAR(20) NOT NULL
);

-- # ---------------------------------------------------------------------- #
-- # Tables                                                                 #
-- # ---------------------------------------------------------------------- #
-- # ---------------------------------------------------------------------- #
-- # Add table "Categories"                                                 #
-- # ---------------------------------------------------------------------- #
-- 2. CATEGORIES
CREATE TABLE categories (
    CategoryID INT PRIMARY KEY,
    CategoryName VARCHAR(50) NOT NULL UNIQUE
);
-- # ---------------------------------------------------------------------- #
-- # Tables                                                                 #
-- # ---------------------------------------------------------------------- #
-- # ---------------------------------------------------------------------- #
-- # Add table "Suppliers"                                                 #
-- # ---------------------------------------------------------------------- #
-- 3. SUPPLIERS
CREATE TABLE suppliers (
    SupplierID INT PRIMARY KEY,
    SupplierName VARCHAR(100) NOT NULL,
    City VARCHAR(50) NOT NULL,
    Region VARCHAR(50) NOT NULL
);

-- # ---------------------------------------------------------------------- #
-- # Tables                                                                 #
-- # ---------------------------------------------------------------------- #
-- # ---------------------------------------------------------------------- #
-- # Add table "Products"                                                 #
-- # ---------------------------------------------------------------------- #
-- 4. PRODUCTS
CREATE TABLE products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(150) NOT NULL,
    CategoryID INT NOT NULL,
    Price DECIMAL(12,2) NOT NULL,
    Cost DECIMAL(12,2) NOT NULL,
    StockQuantity INT NOT NULL,
    SupplierID INT NOT NULL,
    ProductStatus VARCHAR(20) NOT NULL,
    FOREIGN KEY (CategoryID) REFERENCES categories(CategoryID),
    FOREIGN KEY (SupplierID) REFERENCES suppliers(SupplierID)
);

-- # ---------------------------------------------------------------------- #
-- # Tables                                                                 #
-- # ---------------------------------------------------------------------- #
-- # ---------------------------------------------------------------------- #
-- # Add table "Orders"                                                 #
-- # ---------------------------------------------------------------------- #
-- 5. ORDERS
CREATE TABLE orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT NOT NULL,
    OrderDate DATE NOT NULL,
    OrderStatus VARCHAR(30) NOT NULL,
    PaymentMethod VARCHAR(30) NOT NULL,
    FOREIGN KEY (CustomerID) REFERENCES customers(CustomerID)
);

-- # ---------------------------------------------------------------------- #
-- # Tables                                                                 #
-- # ---------------------------------------------------------------------- #
-- # ---------------------------------------------------------------------- #
-- # Add table "Items"                                                 #
-- # ---------------------------------------------------------------------- #
-- 6. ORDER_ITEMS
CREATE TABLE order_items (
    OrderItemID INT PRIMARY KEY,
    OrderID INT NOT NULL,
    ProductID INT NOT NULL,
    Quantity INT NOT NULL,
    UnitPrice DECIMAL(12,2) NOT NULL,
    FOREIGN KEY (OrderID) REFERENCES orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES products(ProductID)
);

-- ------------------------------------------------
-- SAMPLE DATA
-- ------------------------------------------------

INSERT INTO customers VALUES
(1,'Adebayo Stores','Ibadan','South West','Male','2025-01-15','Active'),
(2,'Mariam Ventures','Lagos','South West','Female','2025-01-20','Active'),
(3,'Emeka Retail','Enugu','South East','Male','2025-02-02','Active'),
(4,'Musa Enterprises','Kano','North West','Male','2025-02-14','Active'),
(5,'Fatima Fashion Hub','Abuja','North Central','Female','2025-02-20','Active'),
(6,'Tunde Electronics','Lagos','South West','Male','2025-03-05','Active'),
(7,'Chioma Home Store','Port Harcourt','South South','Female','2025-03-12','Active'),
(8,'Daniel Tech Solutions','Lagos','South West','Male','2025-03-25','Active'),
(9,'Aisha Enterprise','Kaduna','North West','Female','2025-04-01','Active'),
(10,'Chinedu Supplies','Onitsha','South East','Male','2025-04-08','Active'),
(11,'Grace Collections','Benin City','South South','Female','2025-04-15','Active'),
(12,'Yusuf Gadgets','Kano','North West','Male','2025-04-22','Active'),
(13,'Kemi Office Mart','Lagos','South West','Female','2025-05-01','Active'),
(14,'Ibrahim Traders','Abuja','North Central','Male','2025-05-08','Active'),
(15,'Blessing Retail','Enugu','South East','Female','2025-05-15','Active'),
(16,'Samuel Computers','Ibadan','South West','Male','2025-05-22','Active'),
(17,'Zainab Stores','Kaduna','North West','Female','2025-06-01','Active'),
(18,'Olumide Ventures','Lagos','South West','Male','2025-06-08','Active'),
(19,'Esther Beauty','Abeokuta','South West','Female','2025-06-15','Active'),
(20,'Peter Home Needs','Uyo','South South','Male','2025-06-22','Active'),
(21,'Hauwa Enterprise','Abuja','North Central','Female','2025-07-01','Active'),
(22,'Michael Retail','Owerri','South East','Male','2025-07-08','Active'),
(23,'Funke Fashion','Ibadan','South West','Female','2025-07-15','Active'),
(24,'Abdul Traders','Sokoto','North West','Male','2025-07-22','Active'),
(25,'Ruth Supplies','Calabar','South South','Female','2025-08-01','Active'),
(26,'Sade Ventures','Ado-Ekiti','South West','Female','2025-08-08','Active'),
(27,'Ifeanyi Stores','Awka','South East','Male','2025-08-15','Active'),
(28,'Hadiza Enterprise','Abuja','North Central','Female','2025-08-22','Active'),
(29,'Tosin Mart','Lagos','South West','Male','2025-09-01','Inactive'),
(30,'Janet Foods','Lagos','South West','Female','2025-09-08','Active');

INSERT INTO categories VALUES
(1,'Electronics'),
(2,'Phones & Tablets'),
(3,'Computers'),
(4,'Home Appliances'),
(5,'Fashion'),
(6,'Office Supplies'),
(7,'Groceries'),
(8,'Beauty & Personal Care');

INSERT INTO suppliers VALUES
(1,'Lagos Tech Distributors','Lagos','South West'),
(2,'Abuja Electronics Hub','Abuja','North Central'),
(3,'Kano General Supplies','Kano','North West'),
(4,'Port Harcourt Home Supplies','Port Harcourt','South South'),
(5,'Onitsha Wholesale Market','Onitsha','South East'),
(6,'Ibadan Office Supplies','Ibadan','South West'),
(7,'Lagos Fashion Distributors','Lagos','South West'),
(8,'Kaduna Consumer Goods','Kaduna','North West');

INSERT INTO products VALUES
(101,'HP Laptop 15',3,650000,560000,18,1,'Active'),
(102,'Dell Inspiron 14',3,580000,495000,22,2,'Active'),
(103,'Lenovo ThinkPad E14',3,720000,610000,12,1,'Active'),
(104,'Samsung Galaxy A15',2,280000,235000,35,1,'Active'),
(105,'iPhone 13',2,520000,450000,15,2,'Active'),
(106,'Tecno Spark 20',2,190000,155000,40,3,'Active'),
(107,'Wireless Mouse',3,15000,9500,100,1,'Active'),
(108,'Mechanical Keyboard',3,35000,23000,70,1,'Active'),
(109,'27-inch Monitor',3,210000,175000,25,2,'Active'),
(110,'Office Chair',6,120000,90000,30,6,'Active'),
(111,'Standing Desk',6,185000,145000,16,6,'Active'),
(112,'Printer',6,165000,130000,20,6,'Active'),
(113,'Air Conditioner',4,480000,390000,10,4,'Active'),
(114,'Microwave Oven',4,150000,115000,28,4,'Active'),
(115,'Electric Kettle',4,35000,22000,60,4,'Active'),
(116,'Mens Sneakers',5,45000,30000,80,7,'Active'),
(117,'Womens Handbag',5,38000,25000,90,7,'Active'),
(118,'Ankara Fabric',5,22000,14000,120,7,'Active'),
(119,'Office Notebook Pack',6,12000,7000,150,6,'Active'),
(120,'Wireless Earbuds',1,65000,42000,75,1,'Active'),
(121,'Bluetooth Speaker',1,85000,56000,45,1,'Active'),
(122,'Power Bank',1,45000,28000,90,2,'Active'),
(123,'Rice 25kg',7,65000,52000,50,3,'Active'),
(124,'Cooking Oil 5L',7,18000,13000,100,3,'Active'),
(125,'Breakfast Cereal',7,8500,6000,160,3,'Active'),
(126,'Facial Cleanser',8,18000,11000,70,8,'Active'),
(127,'Body Lotion',8,12500,7500,100,8,'Active'),
(128,'Perfume',8,55000,32000,50,7,'Active'),
(129,'Tablet',2,240000,195000,25,2,'Active'),
(130,'USB Flash Drive 64GB',1,12000,7000,200,1,'Inactive');

-- Customers 4 and 29 deliberately have no orders.
-- Customers 1, 2 and 3 deliberately have more than five orders.
INSERT INTO orders VALUES
(1001,1,'2026-01-05','Delivered','Transfer'),
(1002,1,'2026-01-12','Delivered','Card'),
(1003,1,'2026-01-19','Delivered','Transfer'),
(1004,1,'2026-01-28','Shipped','USSD'),
(1005,1,'2026-02-05','Delivered','Transfer'),
(1006,1,'2026-02-18','Delivered','Card'),
(1007,1,'2026-03-02','Pending','Transfer'),
(1008,1,'2026-03-15','Delivered','Transfer'),
(1009,2,'2026-01-07','Delivered','Card'),
(1010,2,'2026-01-22','Delivered','Transfer'),
(1011,2,'2026-02-04','Delivered','Transfer'),
(1012,2,'2026-02-20','Shipped','USSD'),
(1013,2,'2026-03-06','Delivered','Card'),
(1014,2,'2026-03-19','Delivered','Transfer'),
(1015,2,'2026-04-02','Pending','Transfer'),
(1016,3,'2026-01-09','Delivered','Transfer'),
(1017,3,'2026-01-25','Delivered','Card'),
(1018,3,'2026-02-10','Delivered','Transfer'),
(1019,3,'2026-02-26','Shipped','USSD'),
(1020,3,'2026-03-12','Delivered','Card'),
(1021,3,'2026-03-28','Delivered','Transfer'),
(1022,5,'2026-01-11','Delivered','Transfer'),
(1023,5,'2026-02-03','Delivered','Card'),
(1024,5,'2026-02-25','Shipped','Transfer'),
(1025,5,'2026-03-20','Delivered','USSD'),
(1026,6,'2026-01-15','Delivered','Card'),
(1027,6,'2026-02-08','Delivered','Transfer'),
(1028,6,'2026-02-27','Delivered','Transfer'),
(1029,6,'2026-03-18','Shipped','Card'),
(1030,6,'2026-04-05','Delivered','Transfer'),
(1031,7,'2026-01-18','Delivered','Transfer'),
(1032,7,'2026-02-14','Delivered','Card'),
(1033,7,'2026-03-10','Pending','Transfer'),
(1034,8,'2026-01-21','Delivered','Transfer'),
(1035,8,'2026-02-16','Delivered','Card'),
(1036,8,'2026-03-14','Delivered','Transfer'),
(1037,8,'2026-04-01','Shipped','USSD'),
(1038,8,'2026-04-18','Delivered','Transfer'),
(1039,9,'2026-02-01','Delivered','Card'),
(1040,9,'2026-03-01','Delivered','Transfer'),
(1041,10,'2026-01-30','Delivered','Transfer'),
(1042,10,'2026-02-22','Delivered','Card'),
(1043,10,'2026-03-17','Shipped','Transfer'),
(1044,10,'2026-04-10','Delivered','USSD'),
(1045,11,'2026-02-05','Delivered','Transfer'),
(1046,11,'2026-03-05','Delivered','Card'),
(1047,11,'2026-04-05','Delivered','Transfer'),
(1048,12,'2026-01-27','Delivered','Card'),
(1049,12,'2026-02-24','Delivered','Transfer'),
(1050,12,'2026-03-24','Shipped','Transfer'),
(1051,12,'2026-04-21','Delivered','USSD'),
(1052,13,'2026-01-29','Delivered','Transfer'),
(1053,13,'2026-02-19','Delivered','Card'),
(1054,13,'2026-03-11','Delivered','Transfer'),
(1055,13,'2026-04-03','Shipped','Card'),
(1056,13,'2026-04-25','Delivered','Transfer'),
(1057,14,'2026-02-06','Delivered','Transfer'),
(1058,14,'2026-03-22','Delivered','Card'),
(1059,15,'2026-01-17','Delivered','Transfer'),
(1060,15,'2026-02-15','Shipped','Card'),
(1061,15,'2026-03-25','Delivered','Transfer'),
(1062,16,'2026-01-24','Delivered','Transfer'),
(1063,16,'2026-02-21','Delivered','Card'),
(1064,16,'2026-03-21','Delivered','Transfer'),
(1065,16,'2026-04-15','Shipped','USSD'),
(1066,17,'2026-02-12','Delivered','Card'),
(1067,17,'2026-03-16','Delivered','Transfer'),
(1068,18,'2026-01-26','Delivered','Transfer'),
(1069,18,'2026-02-18','Delivered','Card'),
(1070,18,'2026-03-13','Delivered','Transfer'),
(1071,18,'2026-04-07','Shipped','USSD'),
(1072,18,'2026-04-28','Delivered','Transfer'),
(1073,19,'2026-02-09','Delivered','Card'),
(1074,19,'2026-03-09','Delivered','Transfer'),
(1075,19,'2026-04-09','Delivered','Transfer'),
(1076,20,'2026-01-31','Delivered','Transfer'),
(1077,20,'2026-03-02','Delivered','Card'),
(1078,21,'2026-02-13','Delivered','Transfer'),
(1079,21,'2026-03-27','Shipped','Card'),
(1080,21,'2026-04-20','Delivered','Transfer'),
(1081,22,'2026-01-16','Delivered','Transfer'),
(1082,22,'2026-02-17','Delivered','Card'),
(1083,22,'2026-03-19','Delivered','Transfer'),
(1084,22,'2026-04-22','Shipped','USSD'),
(1085,23,'2026-02-07','Delivered','Card'),
(1086,23,'2026-03-08','Delivered','Transfer'),
(1087,23,'2026-04-12','Delivered','Transfer'),
(1088,24,'2026-02-11','Delivered','Transfer'),
(1089,24,'2026-03-30','Delivered','Card'),
(1090,25,'2026-01-14','Delivered','Transfer'),
(1091,25,'2026-02-28','Delivered','Card'),
(1092,25,'2026-04-02','Shipped','Transfer'),
(1093,26,'2026-03-04','Delivered','Transfer'),
(1094,27,'2026-03-07','Delivered','Card'),
(1095,27,'2026-04-17','Delivered','Transfer'),
(1096,28,'2026-03-26','Pending','USSD'),
(1097,30,'2026-02-06','Delivered','Transfer'),
(1098,30,'2026-04-06','Delivered','Card');

-- Multiple products are deliberately placed in several orders.
INSERT INTO order_items VALUES
(1,1001,101,1,650000),
(2,1001,107,2,15000),
(3,1002,103,1,720000),
(4,1003,105,1,520000),
(5,1003,120,2,65000),
(6,1004,109,1,210000),
(7,1005,113,1,480000),
(8,1006,102,1,580000),
(9,1006,108,2,35000),
(10,1007,111,1,185000),
(11,1008,121,2,85000),
(12,1009,104,1,280000),
(13,1009,122,2,45000),
(14,1010,105,1,520000),
(15,1011,101,1,650000),
(16,1011,107,3,15000),
(17,1012,103,1,720000),
(18,1013,109,1,210000),
(19,1014,102,1,580000),
(20,1015,129,1,240000),
(21,1016,123,2,65000),
(22,1017,124,4,18000),
(23,1018,125,6,8500),
(24,1019,116,2,45000),
(25,1020,117,2,38000),
(26,1021,128,2,55000),
(27,1022,118,4,22000),
(28,1023,116,2,45000),
(29,1024,117,3,38000),
(30,1025,128,1,55000),
(31,1026,104,1,280000),
(32,1027,106,2,190000),
(33,1028,120,2,65000),
(34,1029,121,1,85000),
(35,1030,122,3,45000),
(36,1031,114,2,150000),
(37,1032,115,3,35000),
(38,1033,113,1,480000),
(39,1034,101,1,650000),
(40,1035,107,4,15000),
(41,1036,109,1,210000),
(42,1037,110,2,120000),
(43,1038,112,1,165000),
(44,1039,123,2,65000),
(45,1040,124,5,18000),
(46,1041,119,5,12000),
(47,1042,112,1,165000),
(48,1043,110,2,120000),
(49,1044,111,1,185000),
(50,1045,117,2,38000),
(51,1046,126,3,18000),
(52,1047,127,4,12500),
(53,1048,104,1,280000),
(54,1049,106,2,190000),
(55,1050,120,2,65000),
(56,1051,121,2,85000),
(57,1052,110,1,120000),
(58,1053,112,1,165000),
(59,1054,119,6,12000),
(60,1055,107,3,15000),
(61,1056,109,1,210000),
(62,1057,114,1,150000),
(63,1058,115,4,35000),
(64,1059,116,2,45000),
(65,1060,117,2,38000),
(66,1061,118,5,22000),
(67,1062,102,1,580000),
(68,1063,108,2,35000),
(69,1064,120,2,65000),
(70,1065,121,1,85000),
(71,1066,122,2,45000),
(72,1067,128,1,55000),
(73,1068,103,1,720000),
(74,1069,105,1,520000),
(75,1070,101,1,650000),
(76,1071,109,1,210000),
(77,1072,102,1,580000),
(78,1073,126,2,18000),
(79,1074,127,3,12500),
(80,1075,128,1,55000),
(81,1076,113,1,480000),
(82,1077,114,1,150000),
(83,1078,123,2,65000),
(84,1079,124,5,18000),
(85,1080,125,8,8500),
(86,1081,107,3,15000),
(87,1082,108,2,35000),
(88,1083,119,4,12000),
(89,1084,110,1,120000),
(90,1085,116,2,45000),
(91,1086,117,2,38000),
(92,1087,118,3,22000),
(93,1088,124,3,18000),
(94,1089,123,2,65000),
(95,1090,126,2,18000),
(96,1091,127,3,12500),
(97,1092,128,1,55000),
(98,1093,125,5,8500),
(99,1094,129,1,240000),
(100,1095,104,1,280000),
(101,1096,106,1,190000),
(102,1097,124,4,18000),
(103,1098,125,6,8500);

-- # ---------------------------------------------------------------------- #
-- #End#
-- # ---------------------------------------------------------------------- #
