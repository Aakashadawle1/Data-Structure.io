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

CREATE TABLE course
(course_id
VARCHAR (8),
title
VARCHAR (50),
dept_name
VARCHAR (20),
credits
NUMERIC (2,0) CHECK (credits > 0),
primary key (course_id),
foreign key (dept_name) references department
ON DELETE SET NULL);

CREATE TABLE instructor
( ID
VARCHAR (5),
name
VARCHAR (20) NOT NULL,
dept_name
VARCHAR (20),
salary
NUMERIC (8,2) CHECK (salary > 29000),
primary key ( ID ),
foreign key (dept_name) references department
ON DELETE SET NULL);

CREATE TABLE section
(course_id
VARCHAR (8),
sec_id
VARCHAR (8),
semester
VARCHAR (6) CHECK (semester IN
('Fall', 'Winter', 'Spring', 'Summer')),
year
NUMERIC (4,0) CHECK (year > 1701 AND year < 2100),
building
VARCHAR (15),
room_number VARCHAR (7),
time_slot_id VARCHAR (4),
primary key (course_id, sec_id, semester, year),
foreign key (course_id) references course
ON DELETE cascade,
foreign key (building, room_number) references classroom
ON DELETE SET NULL);

CREATE TABLE teaches
( ID
VARCHAR (5),
course_id
VARCHAR (8),
sec_id
VARCHAR (8),
semester
VARCHAR (6),
year
NUMERIC (4,0),
primary key ( ID , course_id, sec_id, semester, year),
foreign key (course_id, sec_id, semester, year) references section
ON DELETE cascade,
foreign key ( ID ) references instructor
ON DELETE cascade);

CREATE TABLE student
( ID
VARCHAR (5),
name
VARCHAR (20) NOT NULL,
dept_name
VARCHAR (20),
tot_cred
NUMERIC (3,0) CHECK (tot_cred >= 0),
primary key ( ID ),
foreign key (dept_name) references department
ON DELETE SET NULL);

CREATE TABLE takes
( ID
VARCHAR (5),
course_id
VARCHAR (8),
sec_id
VARCHAR (8),
semester
VARCHAR (6),
year
NUMERIC (4,0),
grade
VARCHAR (2),
primary key ( ID , course_id, sec_id, semester, year),
foreign key (course_id, sec_id, semester, year) references section
ON DELETE cascade,
foreign key ( ID ) references student
ON DELETE cascade);

CREATE TABLE advisor
(s_ID
VARCHAR (5),
i_ID
VARCHAR (5),
primary key (s_ID ),
foreign key (i_ID ) references instructor ( ID )
ON DELETE SET NULL,
foreign key (s_ID ) references student ( ID )
ON DELETE cascade);

CREATE TABLE prereq
(course_id
VARCHAR(8),
prereq_id
VARCHAR(8),
primary key (course_id, prereq_id),
foreign key (course_id) references course
ON DELETE cascade,
foreign key (prereq_id) references course);

CREATE TABLE timeslot
(time_slot_id VARCHAR (4),
day
VARCHAR (1),
start_hr
NUMERIC (2) CHECK (start_hr >= 0 AND end_hr < 24),
start_min
NUMERIC (2) CHECK (start_min >= 0 AND start_min < 60),
end_hr
NUMERIC (2) CHECK (end_hr >= 0 AND end_hr < 24),
end_min
NUMERIC (2) CHECK (end_min >= 0 AND end_min < 60),
primary key (time_slot_id, day, start_hr, start_min));
```
// Insert value init

``` sql

