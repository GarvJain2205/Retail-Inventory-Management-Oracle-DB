# Retail-Inventory-Management-Oracle-DB

## Project Overview

This project focuses on the design and implementation of a **real-world supermarket database using SQL and PL/SQL in Oracle Database**. The objective was to build a realistic database model that represents the operations of a retail grocery business and to implement several PL/SQL constructs that automate business processes within the system.

The database structure was created to simulate how supermarkets manage product inventories, suppliers, employees, and billing operations. In addition, the project demonstrates how database procedures, packages, and triggers can support business logic and maintain data consistency.

Although the database design was inspired by a supermarket chain in Trinidad, it was created strictly for academic purposes and is not officially connected to the company.

---

# Project Structure

### Database Creation Script

**JTA_Create_Database.sql**
Contains SQL statements used to create all database tables and insert sample records for testing the system.

### PL/SQL Packages and Triggers

**JTA_Packages.sql**
Defines multiple PL/SQL packages, procedures, and triggers used to automate various operations in the database. Each construct is labeled with a comment to identify its functionality.

### Testing Scripts

**JTA_Test_Code.sql**
Includes SQL queries and anonymous PL/SQL blocks that can be used to test the functionality of each procedure and trigger implemented in the system.

### Database Design Diagram

**ERD_High_quality.png**
Provides a visual representation of the database schema, showing the relationships between tables and entities.

---

# Business Context

The database represents a supermarket organization that operates multiple retail locations. The system is designed to support the information requirements of these branches, including product management, supplier interactions, employee records, and billing transactions. The architecture was also designed with scalability in mind so that additional branches or warehouses can be added in the future without major structural changes.

---

# Key Business Rules

## Product Management

* Purchase orders are usually prepared by sales staff and reviewed by the purchasing department before approval.
* Orders may not always be fulfilled due to supplier stock limitations.
* Products are subject to tax rates that may change over time.
* Prices of products frequently change and updates normally occur before the store opens each day.
* The system maintains minimum stock levels to ensure consistent product availability.
* Certain products are identified using standard barcodes, while others such as fresh produce or meats use price lookup codes.

## Supplier Relationships

* Most product brands are supplied by a single wholesaler.
* Multiple contacts may exist for each supplier.
* Supplier payments may occur after goods are delivered.
* Branch locations can order products independently while the head office processes payments.
* Purchase prices may vary over time.

## Employee Management

* Employee information such as name, contact details, and address is stored in the system.
* Staff members may be paid weekly, bi-weekly, or monthly.
* Some employees receive fixed salaries while others are compensated based on hourly work.
* Hourly employees may receive overtime or additional pay depending on working hours and conditions.
* Employees may occasionally work at more than one branch location.

## Billing and Transactions

* Every bill must include the cashier responsible for the transaction and the checkout lane used.
* The amount of cash issued to and returned by cashiers during shifts must be recorded.
* Payments may be made using cash or electronic methods such as debit cards or credit cards.
* In rare cases, customers may settle payments at a later time.

---

# Database Design Considerations

### Immutable Data

Certain information must remain unchanged once a transaction is completed. For example, the tax rate applied to a product at the time of sale should remain fixed even if tax policies change later. Storing these values directly ensures historical accuracy and improves database performance.

### Controlled Redundancy

In large transactional systems, storing certain calculated values directly in tables can improve query speed and simplify reporting. This design decision prioritizes faster data access over minimal storage usage.

### Index Strategy

Indexes were not included in the design because many tables are frequently updated or contain relatively small datasets. According to Oracle guidelines, indexing may not always improve performance in such cases.

### Numeric Storage

Oracle stores numeric values internally in a flexible format, so strict limits on precision are not required for storage optimization. However, constraints were applied to monetary values to prevent incorrect data entry.

### Transaction Handling

Many database procedures perform automatic commits once operations are completed successfully. This approach reduces the risk of losing pending transactions during unexpected events such as system failures.

### Trigger Usage

Instead of relying heavily on triggers to automatically update related tables, most automated tasks are implemented through PL/SQL procedures. These procedures call other functions when needed to maintain consistency across the system.

---

# Barcodes and Price Lookup Codes

Retail products often use barcode systems provided by the global standards organization **GS1**. These codes uniquely identify products and are commonly used for pre-packaged goods.

However, certain products such as fresh meat or produce are priced based on weight, meaning each package may have a different price. For these items, **Price Lookup (PLU) codes** are used.

A PLU resembles a barcode and allows the point-of-sale system to determine both the product identity and its price when scanned.

### Structure of a PLU Code

A typical PLU contains:

1. A prefix digit indicating that the code represents a PLU.
2. A set of digits identifying the product.
3. A validation digit used for verification.
4. A section representing the price value.
5. A final check digit to confirm the code was scanned correctly.

This system allows variable-priced items to be efficiently processed during checkout.
