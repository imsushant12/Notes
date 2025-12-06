### Database Commands:
#### Create database:
```SQL
CREATE DATABASE database_name;
```

#### Switch to a database:
```SQL
USE database_name;
```
---

### Table Commands:

#### Create a table:
``` SQL
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);
```
- Example: Create a student table with constraints:
    ``` SQL
    CREATE TABLE students (
        student_ID     INT            PRIMARY KEY,
        student_name   VARCHAR(20)    NOT NULL,
        roll_no        INT            AUTO_INCREMENT,
        bus_ID         INT            UNIQUE,
        section        VARCHAR(1)     DEFAULT 'A'
    );
    ```

> **NOTE**: We can also declare the primary key after the column names. 
> - Syntax: ``PRIMARY KEY (column_name);``

#### View or describe a table:
```SQL
DESCRIBE table_name;
```

#### Delete (Drop) a table:
```SQL
DROP TABLE table_name;
```

#### Modify a table:
#### a. Adding a column-
```SQL
ALTER TABLE table_name ADD column_name datatype;
```

##### b. Deleting a column-
```SQL
ALTER TABLE table_name DROP column_name;
```

##### c. Renaming a column-
```SQL
ALTER TABLE table_name RENAME COLUMN 
old_column_name TO new_column_name;
```

#### Set a Foreign Key:
```SQL
CREATE TABLE table_name (
    ...
    FOREIGN KEY (foreign_key_column) 
    REFERENCES primary_table (primary_key_column)
    ON DELETE SET NULL;
);
```

OR 

```SQL
ALTER TABLE table_name
ADD FOREIGN KEY (foreign_key_column) 
REFERENCES primary_table (primary_key_column)
ON DELETE SET NULL;
```


---
### Data Manipulation Commands:

#### Insert values into a table:
```SQL
INSERT INTO table_name 
VALUES(column1_value, column2_value...);
```

#### Insert values (in specified columns) into a table:
```SQL
INSERT INTO table_name 
(column1, column3,...) VALUES(column1_value, column3_value...);
```

#### View records of a table:
```SQL
SELECT * FROM table_name;
```

#### Update the record value(s):
```SQL
UPDATE table_name 
SET column_name = 'new_column_value'
WHERE ...;
```
- Example - Update the name of a student whose ID is 5:
    ```SQL
    UPDATE students 
    SET student_name = 'New Name'
    WHERE student_ID = 5;
    ```

#### Delete all the records (not the table):
```SQL
DELETE FROM table_name;
```

#### Delete specific record(s):
```SQL
DELETE FROM table_name
WHERE ...;
```

#### ORDER BY:
```SQL
SELECT *
FROM table_name
ORDER BY column_name; 
```

> **Note** If no value is specified, ordering is done in ascending order (ASC). We can specify descending ordering: 
> - Syntax: ``ORDER BY column_name DESC``;

#### LIMIT:
`LIMIT 5;` after the SELECT clause.

#### DISTINCT:
- Helps us to find all the different values in a column. 
- Example: find all different genders.
    ```SQL
    SELECT DISTINCT column_name FROM table_name;
    ```

#### SQL FUNCTIONS:
1. **COUNT()**
   - Example: find the number of students.
        ```SQL
        SELECT COUNT(column_name) FROM table_name;
        ```

2. **AVG()**
    ```SQL
    SELECT AVG(column_name) FROM table_name;
    ```

3. **SUM()**
    ```SQL
    SELECT SUM(column_name) FROM table_name;
    ```

4. **GROUP BY()**
    ```SQL
    SELECT * FROM table_name
    GROUP BY column_name;
    ```

#### OPERATORS:
1. **UNION()** - combines various SELECT statements.
    ```SQL
    SELECT * FROM table_name
    UNION
    SELECT * FROM table_name;
    ```

2. **UNION ALL()** - selects all the rows including the duplicates (repeated values) from both the queries.

#### JOINS:
- Combines rows from two or more tables. Joins uses the common column.
- Types of Joins:
1. **INNER JOIN()**
    ```SQL
    SELECT column1, column2, ....
    FROM table1_name
    JOIN table2_name
    ON table1.common_column = table2.common_column;
    ```

2. **LEFT JOIN()**
   - Returns Join as well as all the values of the left table i.e. table1.
   - Syntax: `JOIN` -> `LEFT JOIN`

3. **RIGHT JOIN()**
   - Returns Join as well as all the values of the right table i.e. table2.
   - Syntax: `JOIN` -> `RIGHT JOIN`

> **NOTE**: The fourth type of join i.e. FULL OUTER JOIN is not used in MySQL.
