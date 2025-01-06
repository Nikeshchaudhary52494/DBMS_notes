### **DML (Data Manipulation Language) Commands in DBMS**

DML commands are used to manipulate data within database objects, such as tables. These commands deal with retrieving, inserting, updating, and deleting data in the database. Unlike DDL, DML commands do not alter the database schema.

---

### **Key DML Commands**

1. **SELECT**
   - **Purpose**: Used to retrieve data from one or more tables in the database.
   - **Syntax**:
     ```sql
     SELECT column1, column2, ...
     FROM table_name
     [WHERE condition]
     [ORDER BY column_name [ASC|DESC]];
     ```
   - **Example**:
     ```sql
     SELECT Name, Age
     FROM Students
     WHERE Age > 18
     ORDER BY Name ASC;
     ```
   - **Key Points**: 
     - Non-destructive; it only fetches data.
     - Can include filtering (`WHERE`), sorting (`ORDER BY`), and aggregation functions (`COUNT`, `SUM`, etc.).

---

2. **INSERT**
   - **Purpose**: Used to add new rows of data into a table.
   - **Syntax**:
     ```sql
     INSERT INTO table_name (column1, column2, ...)
     VALUES (value1, value2, ...);
     ```
   - **Example**:
     ```sql
     INSERT INTO Students (StudentID, Name, Age, Grade)
     VALUES (1, 'John Doe', 20, 'A');
     ```
   - **Key Points**:
     - Inserts a single row or multiple rows.
     - If column names are not specified, all columns must have values in the specified order.

---

3. **UPDATE**
   - **Purpose**: Used to modify existing data in a table.
   - **Syntax**:
     ```sql
     UPDATE table_name
     SET column1 = value1, column2 = value2, ...
     WHERE condition;
     ```
   - **Example**:
     ```sql
     UPDATE Students
     SET Grade = 'B'
     WHERE Age < 18;
     ```
   - **Key Points**:
     - If no `WHERE` clause is used, all rows in the table will be updated (use cautiously).
     - Can update one or multiple columns at once.

---

4. **DELETE**
   - **Purpose**: Used to remove rows of data from a table.
   - **Syntax**:
     ```sql
     DELETE FROM table_name
     WHERE condition;
     ```
   - **Example**:
     ```sql
     DELETE FROM Students
     WHERE Grade = 'F';
     ```
   - **Key Points**:
     - Deletes specific rows when a `WHERE` clause is provided.
     - Without a `WHERE` clause, all rows in the table will be removed (table structure remains intact).

---

### **Key Characteristics of DML Commands**
1. **Data-Focused**: 
   - DML commands work exclusively on data, leaving the structure or schema unchanged.
   
2. **Transaction Control**: 
   - DML commands can be rolled back or committed when wrapped in a transaction (`COMMIT`/`ROLLBACK`).

3. **Impact on Tables**:
   - These commands manipulate rows within a table without affecting the table's structure.

4. **Classification**:
   - DML commands are often called **non-procedural queries** because they specify *what* data to manipulate rather than *how* to manipulate it.

---

### **DML and Transactions**
- DML commands like `INSERT`, `UPDATE`, and `DELETE` can be combined with **transaction control commands** for reliability:
  - `BEGIN TRANSACTION`: Starts a transaction.
  - `COMMIT`: Saves changes to the database.
  - `ROLLBACK`: Reverts changes made during a transaction.
  
**Example:**
```sql
BEGIN TRANSACTION;

UPDATE Students
SET Grade = 'A'
WHERE Name = 'John';

ROLLBACK; -- Reverts the change if needed
```

---

### **Difference Between DML and DDL**
| Feature               | DML (Data Manipulation Language)        | DDL (Data Definition Language)            |
|-----------------------|-----------------------------------------|-------------------------------------------|
| **Purpose**           | Manipulates data within database objects. | Defines or modifies database structure.    |
| **Commands**          | `SELECT`, `INSERT`, `UPDATE`, `DELETE`  | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`     |
| **Impact**            | Affects rows of data only.              | Affects schema and objects in the database. |
| **Transaction Control** | Changes can be rolled back.            | Changes are auto-committed (irreversible). |
| **Examples**          | `INSERT INTO Students ...`              | `CREATE TABLE Students ...`               |

---

### **Conclusion**
DML commands are essential for manipulating data in relational databases, enabling CRUD (Create, Read, Update, Delete) operations to ensure effective data handling in DBMS.