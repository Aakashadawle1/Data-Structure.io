# Table Creattion and Insert init

// Create Database
``` sql
CREATE DATABASE university;
```
// For use the database
``` sql
USE university;
```

// Create Table
``` sql
CREATE TABLE classroom
(building
VARCHAR (15),
room_number VARCHAR (7),
capacity
NUMERIC (4,0),
primary key (building, room_number));

CREATE TABLE department
(dept_name
VARCHAR (20),
building
VARCHAR (15),
budget
NUMERIC (12,2) CHECK (budget > 0),
primary key (dept_name));
```
