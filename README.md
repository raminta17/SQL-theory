# SQL-theory

### DATA TYPES: 

1. **INT** - sveikieji skaiciai

2. **DECIMAL(M,N)** - M kiek skaiciu is viso, N - kiek skaiciu po kablelio.

3. **VARCHAR(1)** - text or string, number is the maximum length of the text it can store

4. **BLOB** - large data like images or files

5. **DATE** - yyyy-mm-dd

6. **TIMESTAMP** - yyyy-mm-dd HH:MM:SS

### command prompt connect to your database
![image](https://github.com/raminta17/SQL-theory/assets/62699647/2f4ba3ee-e6b7-4a94-9d5f-f37dc038f6a9)

> [!IMPORTANT]
> - finish sql commands with DELIMITER **;**

> [!TIP]
> - sql reserved words in capital letters for easier readability

### comparison operators: 
> =, < , > , <=. >=, <> (nelygu), AND, OR

## CREATING NEW DATABASES AND TABLES

1. **SHOW DATABASES;** - parodys visas sukurtas tavo duombazes
2. **CREATE DATABASE databaseName;** - sukurs nauja duomenu baze
3. **USE databaseName;** - pasirinkti duomenu bazei su kuria dirbsi;
4. **SELECT DATABASE ();** - parodys pasirinkta duomenu baze
5. sukurti naujai lentelej pasirinktoje duomenu bazeje -
   **CREATE TABLE tableName ( <br />
 nameOfTheFirstColumn INT PRIMARY KEY, <br />
nameOfTheSecondColumn VARCHAR(20) NOT NULL, <br />
nameOfTheThirdColumn VARCHAR(20) UNIQUE, <br />
nameOfTheForthColumn VARCHAR(20) DEFAULT 'default value', <br />
);**
6. **DESCRIBE tableName;**  - parodys pasirinktos lenteles duomenis;
7. **DROP TABLE tableName;** - istrins lentele
8. **SHOW TABLES;** - isvardins visas sukurtas lenteles pasirinktoje duomenu bazeje

## INSERTING, UPDATING AND DELETING ROWS
   
1.  **ALTER TABLE tableName ADD nameOfTheNewColumn DECIMAL(3,2);** - sukurs nauja stulpeli jau egzistuojancioj lentelej

2. **ALTER TABLE tableName DROP COLUMN nameOfTheColumnToDelete;**  - istrins stulpeli pasirinkooj lentelej
   
3. **INSERT INTO tableName VALUES (1, 'string', 'string');** - sukurs nauja eilute pasirinktoj lentelej, reiksmes rasomos is eiles. stringai - vinegubose kabutese ''
   
4. **SELECT * FROM tableName;** - parodys lentele
   
5. **INSERT INTO tableName(nameOfTheFirstColumn, nameOfTheSecondColumn) VALUES(2, 'string') ;** - sukurs nauja eilute lenteleje jei neturi kazkurios info, toj vietoj rasys NULL
   
6. Constrains (write when creating table after column data type:
    
- **NOT NULL** - turi but nurodyta reiksme,
- **UNIQUE** - turi but unikali reiksme,
- **DEFAULT** 'defulat value' - nurodoma default reiksme,
- **AUTO_INCREMENT** - naudinga for primary key automatiskai sukuria is eiles eiliu numeracija, nereikia kuriant eiles nurodinet primary key reiksmes
  
7. updating the table (pakeis visas reiksmes nurodytas where):
   
**UPDATE tableName <br />
SET columnName = 'new value' <br />
(SET columnName = 'new value', anotherColumnName = 'another new value') - this will change multiple column is selected row <br />
WHERE columnName = 'current value';** <br />
(WHERE columnName = 'current value' OR columnName = 'current value') - this would change all specified values to be changed

8. deleting rows:
   
**DELETE FROM tableName;** - this will delete all rows from the table
**DELETE FROM tableName <br />
WHERE columnName = 'value';** - will delete speficied row/s. <br />
WHERE columnName = 'value' AND anotherColumnName = 'value ; - will delete rows when both conditions met.

## SELECT 

1. **SELECT columnName, anotherColumnName <br />
FROM tableName;** - will give back only those columns from the table that you asked
2. **ORDER BY columnName DESC;** - will give back info order alphabetically of the spec column in descinding order (default is assending order)
3. **LIMIT 2;** - si eilute selectinant grazins tik pirmas dvi reiksmes is lenteles
4. **WHERE columnName = 'value;** - grazins lentele su nurodyta stulpelio reiksme
5. **WHERE columnName IN ('value1', 'value2');** - grazins lentele su nurodytom stulpelio reiksmemis
6. **SELECT columnName AS differentName <br />
FROM tableName;** - will show data from columnName but the name of the column will be differentName
7. **SELECT DISTINCT columnName** - will display all diferent values in the column;
8. **SELECT COUNT(columnName)** - will display how many values are in the selected column
9. **SELECT AVG(columnName)** - will count the avarage of the selected column
10. **SELECT SUM(columnName)** - grazins suma
11. **SELECT COUNT(sex), sex  <br />
FROM employee <br />
GROUP BY sex;** - grazins lentele kiek kokios lyties darbuotoju (sudeda nurodyto stulpelio skirtingas reiksmes)
   
## FOREIGN KEY AND COMBINED KEY

1. providing foreign key: <br />
**ALTER tableName <br />
ADD FOREIGN KEY(tableColumnName) <br />
REFERENCES otherTableName(otherTableColumnName) <br />
ON DELETE SET NULL;**

2.  table with combined key example: <br />
**CREATE TABLE works_with ( <br />
  emp_id INT, <br />
  client_id INT, <br />
  total_sales INT, <br />
  PRIMARY KEY(emp_id, client_id),  <br />
  FOREIGN KEY(emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE, <br />
  FOREIGN KEY(client_id) REFERENCES client(client_id) ON DELETE CASCADE <br />
);** 

3. inserting data in tables with foreign keys example: <br />
**INSERT INTO employee VALUES(100, 'David', 'Wallace', '1967-11-17', 'M', 250000, NULL, NULL); <br />
INSERT INTO branch VALUES(1, 'Corporate', 100, '2006-02-09');  UPDATE employee SET branch_id = 1WHERE emp_id = 100;**

- **ON DELETE SET TO NULL** - if primary key deleted in other table that it is referenced in this table - set that value to  NULL
- **ON DELETE CASCADE**  - if primary key deleted then delete the entire row with that foreign key (applicable in combined keys)

## WILD CARDS 

finding specific values in the table (like filter)

1. **%** example: <br />
**SELET * <br />
FROM tableName <br />
WHERE columnName LIKE '%valueEnd';** - will display a row from the table that columnName text ends with valueEnd.

**'%valueAnywhere%'** - will find the text anywhere in the seleted column value

2. **_** - any symbol, example: <br />
**SELET * <br />
FROM employee <br />
WHERE birth_date LIKE '____-10%';** - will show the employees that were born in October

## UNION OPERATOR

_it can combine columns from different tables into one, example:_

> SELECT columnName <br />
>   FROM tableName <br />
>   UNION <br />
>   SELECT columnName <br />
>   FROM otherTableName;

**RULES:**
1. select only one column from each table <br />
2. has to be similar data type


## JOIN OPERATOR

used to combine rows from tables based on the related column (useful when table has foreign keys that related to a different table), example:
> SELECT tableName.columnName, tableName.otherColumnName, otherTableName.columnName <br />
>   FROM tableName  <br />
>   JOIN otherTableName <br />
>   ON table.column = otherTable.relatedColumnName; (_columns that are related_)

the example above will display total of 3 columns that has related values

_types of join operator:_
1. **JOIN** - general, will give back only related values
2. **LEFT JOIN** - will give back all values from the first table and in not related values NULL will be displayed
3. **RIGHT JOIN** - same as left just will display all rows from the joining table
4. **FULL OUTER JOIN** - will display all values from both joining tables - _CANNOT BE DONE IN MYSQL_

## NESTED QUERIES

employee table:
![image](https://github.com/raminta17/SQL-theory/assets/62699647/3fef5322-2dc6-4bdc-8fd6-dcc1d153c327)
works_with table:
![image](https://github.com/raminta17/SQL-theory/assets/62699647/5b424133-c872-42cb-97f9-9c16ad045ebb)

 **task**:
> find names of all employees who sold more than 30000 to a single client

 **solution:**
> SELECT employee.first_name, employee.last_name <br />
>    FROM employee <br />
>    WHERE employee.emp_id IN ( <br />
>    SELECT works_with.emp_id <br />
>    FROM works_with <br />
>    WHERE works_with.total_sales > 30000 <br />
> );

**result:**
![image](https://github.com/raminta17/SQL-theory/assets/62699647/78183b9f-1f3a-46c8-a73f-3575df490302)


## TRIGGERS

_used to track changes before or after was created/updated/deleted etc in your database_

example (before new employee is added):

STEP 1:
> CREATE TABLE triggerTable ( <br />
>   message VARCHAR(100) <br />
> ); <br />

STEP 2: <br />
> DELIMITER $$  <br />

STEP 3:
> CREATE <br />
>   TRIGGER triggerName BEFORE INSERT  _----- BEFORE or AFTER //// INSERT or UPDATE or DELETE_ <br />
>   ON employee <br />
>   FOR EACH ROW BEGIN <br />
>   INSERT INTO triggerTable VALUES('new employee added'); <br />
> END$$ <br />

STEP 4:
> DELIMITER ;

Now before new entry to employee table we will get new trigger in trigger_test table about newly added employee

**To delete a trigger:**
**DROP TRIGGER triggerName;**
