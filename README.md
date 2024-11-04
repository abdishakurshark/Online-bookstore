# Online-bookstore
Overview

This database schema is designed for a bookstore system that tracks customers, books, categories, and purchase records. The schema includes four main tables: Customer, Categories, Books, and CustomerBook, structured to handle customer information, book inventory, categories, and purchase history.

Database Tables

1. Customer

This table stores information about each customer.

CustomerID: Primary key, unique identifier for each customer, auto-incremented.

FirstName: First name of the customer.

LastName: Last name of the customer.

Email: Customer's email address, unique to avoid duplicates.

PhoneNumber: Contact number of the customer.

Address: Customer's address.


2. Categories

This table stores book categories.

CategoryID: Primary key, unique identifier for each category, auto-incremented.

CategoryName: Name of the category, unique to avoid duplicates.


3. Books

This table contains details of each book.

BookID: Primary key, unique identifier for each book, auto-incremented.

Title: Title of the book.

Author: Author of the book.

Publisher: Publisher of the book.

Price: Price of the book in decimal format.

ISBN: Unique ISBN number for the book.

CategoryID: Foreign key linked to Categories.CategoryID, representing the category of the book.


4. CustomerBook

This table is a junction table that records the relationship between customers and books they purchased, enabling a many-to-many relationship between Customer and Books.

CustomerID: Foreign key referencing Customer.CustomerID.

BookID: Foreign key referencing Books.BookID.

PurchaseDate: Timestamp of when the book was purchased.


# Relationships

One-to-Many: Each book is associated with one category (through CategoryID), but a category can have multiple books.

Many-to-Many: Each customer can purchase multiple books, and each book can be purchased by multiple customers. This relationship is managed through the CustomerBook junction table.


Usage

This schema is ideal for a basic bookstore application, supporting:

Customer Management: Tracking customers and their information.

Inventory Management: Organizing books by categories and keeping track of book details.

Sales Tracking: Recording purchase transactions to track which customers bought which books and when.


SQL Setup

To set up the database schema, use the following SQL code:

CREATE TABLE Customer (
    CustomerID INT PRIMARY KEY AUTO_INCREMENT,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100) UNIQUE,
    PhoneNumber VARCHAR(20),
    Address TEXT
);

CREATE TABLE Categories (
    CategoryID INT PRIMARY KEY AUTO_INCREMENT,
    CategoryName VARCHAR(50) UNIQUE
);

CREATE TABLE Books (
    BookID INT PRIMARY KEY AUTO_INCREMENT,
    Title VARCHAR(100),
    Author VARCHAR(100),
    Publisher VARCHAR(100),
    Price DECIMAL(10, 2),
    ISBN VARCHAR(20) UNIQUE,
    CategoryID INT,
    FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID)
);

CREATE TABLE CustomerBook (
    CustomerID INT,
    BookID INT,
    PurchaseDate TIMESTAMP,
    PRIMARY KEY (CustomerID, BookID),
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID),
    FOREIGN KEY (BookID) REFERENCES Books(BookID)
);

This schema provides a strong foundation for a bookstore application with straightforward customer and book management features.