# Database management System notes

## DDL
DDL (Data Definition Language) commands in DBMS are used to define, modify, and manage the structure of database objects such as tables, schemas, indexes, and more. These commands are primarily used to define the database schema. 

### Common DDL Commands:

1. **CREATE**  
   Used to create new database objects such as tables, indexes, views, or databases.  
   **Syntax:**
   ```sql
   CREATE TABLE table_name (
       column1 datatype constraints,
       column2 datatype constraints,
       ...
   );
   ```
   **Example:**
   ```sql
   CREATE TABLE Students (
       StudentID INT PRIMARY KEY,
       Name VARCHAR(50),
       Age INT,
       Grade CHAR(1)
   );
   ```

2. **ALTER**  
   Used to modify the structure of an existing database object, such as adding, deleting, or modifying columns in a table.  
   **Syntax:**
   ```sql
   ALTER TABLE table_name
   ADD column_name datatype;

   ALTER TABLE table_name
   DROP COLUMN column_name;

   ALTER TABLE table_name
   MODIFY COLUMN column_name new_datatype;
   ```
   **Example:**
   ```sql
   ALTER TABLE Students
   ADD Address VARCHAR(100);

   ALTER TABLE Students
   DROP COLUMN Grade;

   ALTER TABLE Students
   MODIFY COLUMN Age TINYINT;
   ```

3. **DROP**  
   Used to delete database objects like tables, views, or entire databases.  
   **Syntax:**
   ```sql
   DROP TABLE table_name;
   DROP DATABASE database_name;
   ```
   **Example:**
   ```sql
   DROP TABLE Students;

   DROP DATABASE SchoolDB;
   ```

4. **TRUNCATE**  
   Used to delete all rows from a table, effectively resetting the table, while retaining its structure.  
   **Syntax:**
   ```sql
   TRUNCATE TABLE table_name;
   ```
   **Example:**
   ```sql
   TRUNCATE TABLE Students;
   ```

5. **RENAME**  
   Used to rename a database object, such as a table.  
   **Syntax:**
   ```sql
   RENAME TABLE old_table_name TO new_table_name;
   ```
   **Example:**
   ```sql
   RENAME TABLE Students TO Learners;
   ```

6. **COMMENT**  
   Used to add descriptive comments to database objects for documentation purposes.  
   **Syntax:**
   ```sql
   COMMENT ON TABLE table_name IS 'Description of the table';
   ```
   **Example:**
   ```sql
   COMMENT ON TABLE Students IS 'Stores student information';
   ```

### Key Points:
- DDL changes the database schema permanently.
- Unlike DML commands, DDL commands are auto-committed, meaning changes are saved immediately and cannot be rolled back.
- DDL commands focus on defining the database structure rather than manipulating data.

These commands are essential for creating and maintaining a database's structure in any relational database management system (RDBMS).