# The-Python-Project-with-MySQL-Server-Language.

**Description:**


The Python Programming Project with the help of MySQL Server Language.


**Creating Databases in MySQL**

### Create MySQL Connection

import mysql.connector as sql

connection = sql.connect(
  host="localhost",
  user="root",
  password="12345"
)

print(connection)
<mysql.connector.connection.MySQLConnection object at 0x000002A103852C88>
Creating Databases
cursor = connection.cursor()

cursor.execute("CREATE DATABASE student")
cursor.execute('SHOW DATABASES')
for database in cursor:
    print(database)
('information_schema',)
('krish',)
('krish1',)
('krish2',)
('mydatabase',)
('mysql',)
('performance_schema',)
('sakila',)
('student',)
('sys',)
('world',)


**Creating Tables And Inserting Records**

### Create MySQL Connection And Connect

import mysql.connector as sql

connection = sql.connect(
  host="localhost",
  user="root",
  password="12345",
  database="student"
)

print(connection)
<mysql.connector.connection.MySQLConnection object at 0x0000028D7250C708>
Create Table In MySQL using Python
cursor = connection.cursor()

cursor.execute("CREATE TABLE studentinfo (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255), subject VARCHAR(255))")
Insert Records in Table
query = "INSERT INTO studentinfo (name, subject) VALUES (%s, %s)"
value = ("John", "Stats")
cursor.execute(query,value)
print("Row inserted",cursor.lastrowid)
Row inserted 1

### Insert multiple records in Table

query = "INSERT INTO studentinfo (name, subject) VALUES (%s, %s)"
values = [("Krish", "Stats"),
        ("Joe", "Maths"),
        ("Ankur","Data Science"),
        ("Paul","Data Science"),
        ("Vishal","Maths"),
        ("Krish","Data Science")]
cursor.executemany(query,values)
print("Row inserted",cursor.lastrowid)
Row inserted 2
Select All
cursor = connection.cursor()
cursor.execute("Select * from studentinfo")

### Fetch All the Data

cursor.fetchall()
[(1, 'John', 'Stats'),
 (2, 'Krish', 'Stats'),
 (3, 'Joe', 'Maths'),
 (4, 'Ankur', 'Data Science'),
 (5, 'Paul', 'Data Science'),
 (6, 'Vishal', 'Maths'),
 (7, 'Krish', 'Data Science')]

### Fetch One Record At A time

cursor.fetchone()
lst=cursor.fetchall()
for records in lst:
    print(records)
(1, 'John', 'Stats')
(2, 'Krish', 'Stats')
(3, 'Joe', 'Maths')
(4, 'Ankur', 'Data Science')
(5, 'Paul', 'Data Science')
(6, 'Vishal', 'Maths')
(7, 'Krish', 'Data Science')
Selecting Particular Rows
cursor.execute("Select * from studentinfo where name='Krish'")

### Fetch All the Data

cursor.fetchall()
[(2, 'Krish', 'Stats'), (7, 'Krish', 'Data Science')]
Select Particular Columns
cursor.execute("Select subject from studentinfo")

#### Fetch All

cursor.fetchall()
[('Stats',),
 ('Stats',),
 ('Maths',),
 ('Data Science',),
 ('Data Science',),
 ('Maths',),
 ('Data Science',)]

## Select Distinct Columns

cursor.execute("SELECT DISTINCT subject from studentinfo")

#### Fetch All

cursor.fetchall()

cursor.execute("SELECT name, subject FROM studentinfo WHERE name = 'Krish' OR subject = 'Data Science'") 
#### Fetch All
cursor.fetchall()
[('Krish', 'Stats'),
 
 ('Paul', 'Data Science'),
 ('Krish', 'Data Science')]
Drop Table
cursor.execute("DROP TABLE studentinfo") 
