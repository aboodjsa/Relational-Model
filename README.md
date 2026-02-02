# Hotel Management Database

## Relationship Model – dbdiagram.io README

---

## 1. Overview

This document explains the **relationship (relational) model** designed for a hotel management system and implemented using **dbdiagram.io**.

The model is derived directly from the provided **Entity Relationship (ER) diagram** and preserves all entities, attributes, and cardinalities.

The purpose of this database is to facilitate the management of:

* Hotels
* Rooms
* Employees
* Hotel types
* Room categories

---

## 2. Tool Used

* **dbdiagram.io**
* Schema language: **DBML (Database Markup Language)**

The DBML code defines tables, primary keys, and foreign keys, which dbdiagram.io automatically converts into a visual relationship diagram.

---

## 3. Database Tables Description

### 3.1 Type

The `Type` table stores hotel classifications (for example: resort, business, luxury).

* One type can be associated with many hotels.

**Primary Key:** `Type_Id`

---

### 3.2 Hotel

The `Hotel` table stores basic hotel information.

* Each hotel belongs to exactly one type.
* This relationship is implemented using a foreign key.

**Primary Key:** `Hotel_Id`

**Foreign Key:**

* `Type_Id` → Type(Type_Id)

---

### 3.3 Category

The `Category` table defines room categories such as standard, deluxe, or suite.

* A category can be assigned to many rooms.
* Pricing and bed information are stored at category level.

**Primary Key:** `Category_Id`

---

### 3.4 Room

The `Room` table represents rooms inside hotels.

* Each room belongs to one hotel.
* Each room belongs to one category.
* A hotel can have many rooms.
* A category can describe many rooms.

**Primary Key:** `Room_Id`

**Foreign Keys:**

* `Hotel_Id` → Hotel(Hotel_Id)
* `Category_Id` → Category(Category_Id)

---

### 3.5 Employee

The `Employee` table stores employee information.

* Each employee works in one hotel.
* A hotel can employ many employees.
* Employees can supervise other employees (recursive relationship).

**Primary Key:** `Employee_Id`

**Foreign Keys:**

* `Hotel_Id` → Hotel(Hotel_Id)
* `Leader_Id` → Employee(Employee_Id)

---

## 4. Relationships Summary

| Relationship        | Cardinality | Description                       |
| ------------------- | ----------- | --------------------------------- |
| Type → Hotel        | 1 : N       | One type classifies many hotels   |
| Hotel → Room        | 1 : N       | One hotel contains many rooms     |
| Category → Room     | 1 : N       | One category describes many rooms |
| Hotel → Employee    | 1 : N       | One hotel employs many employees  |
| Employee → Employee | 1 : N       | One employee leads many employees |

---

## 5. Design Rules Applied

* Each entity from the ER diagram is converted into a table.
* Primary keys uniquely identify records.
* One-to-many relationships are implemented using foreign keys on the many side.
* The recursive relationship is handled using a self-referencing foreign key.
* The database follows **Third Normal Form (3NF)** to avoid redundancy.

---

## 6. Integrity and Constraints

* Foreign keys ensure **referential integrity**.
* Mandatory relationships from the ER diagram are enforced using `NOT NULL` foreign keys.
* Recursive integrity is maintained within the Employee table.

---

## 7. Conclusion

This relationship model accurately represents the original ER diagram and is fully compatible with dbdiagram.io. The design is normalized, scalable, and suitable for implementation in relational database systems such as MySQL or PostgreSQL.

---
