A **trigger** in SQL is a database object that automatically executes a specified action or a block of SQL code in response to certain events on a table or view. These events include operations like `INSERT`, `UPDATE`, or `DELETE`.

Triggers are commonly used to enforce business rules, maintain audit trails, and perform automatic updates.

---

**Types of Triggers in DBMS**

Triggers in a Database Management System (DBMS) are special stored procedures that automatically execute in response to specific events on a table or view. These events can include data modification operations (DML), data definition operations (DDL), or system events. Here's a breakdown of the main types:

**1. DML (Data Manipulation Language) Triggers**

* **Triggered by:** INSERT, UPDATE, DELETE statements on a table.
* **Purpose:** Enforce business rules, maintain data integrity, and perform actions based on data changes.
* **Types:**
    * **Row-level triggers:** Execute for each row affected by the DML statement.
        * Example: Updating an inventory count for each product sold.
    * **Statement-level triggers:** Execute once for the entire SQL statement, regardless of the number of rows affected.
        * Example: Logging the time and user who executed a bulk update.

**2. DDL (Data Definition Language) Triggers**

* **Triggered by:** CREATE TABLE, ALTER TABLE, DROP TABLE, and other schema-altering statements.
* **Purpose:** Monitor and control changes to the database schema, such as table creation, modification, or deletion.
* **Example:** Creating a backup of a table before it is dropped.

**3. Logon Triggers**

* **Triggered by:** User login events.
* **Purpose:** Perform actions when a user logs into the database, such as setting session variables or executing security checks.

**4. System Triggers**

* **Triggered by:** Specific system events, such as database startup or shutdown.
* **Purpose:** Perform system-level tasks, such as initializing or cleaning up resources.

**Key Considerations:**

* **Timing:** Triggers can be defined to execute **before** or **after** the triggering event.
* **Scope:** Triggers can be associated with specific tables, views, or even the entire database.
* **Complexity:** Triggers can range from simple to very complex, depending on the business logic they implement.

**Example Scenarios:**

* **DML Trigger (Row-level):** In an e-commerce system, a trigger on the `Orders` table could update the `quantity_in_stock` in the `Products` table for each order item.
* **DML Trigger (Statement-level):** A trigger on the `Employees` table could log the time and user who performed a bulk update to employee salaries.
* **DDL Trigger:** A trigger on the `CREATE TABLE` event could automatically create indexes on specific columns of new tables.

By understanding these different types of triggers, database administrators and developers can effectively leverage this powerful feature to enhance data integrity, automate tasks, and improve the overall efficiency of their database systems.

### **Syntax for Creating a Trigger**

```sql
CREATE TRIGGER trigger_name
[BEFORE | AFTER] [INSERT | UPDATE | DELETE]
ON table_name
[FOR EACH ROW]
BEGIN
    -- Trigger body (SQL statements)
END;
```

---

### **Example**

#### BEFORE INSERT Trigger:
```sql
CREATE TRIGGER before_insert_example
BEFORE INSERT
ON employees
FOR EACH ROW
BEGIN
    -- Automatically set the created_at column to the current timestamp
    SET NEW.created_at = NOW();
END;
```

#### AFTER DELETE Trigger:
```sql
CREATE TRIGGER after_delete_example
AFTER DELETE
ON orders
FOR EACH ROW
BEGIN
    -- Log the deletion in a separate audit table
    INSERT INTO audit_log (action, table_name, action_time)
    VALUES ('DELETE', 'orders', NOW());
END;
```

---

### **Key Points to Remember**
1. **Triggers cannot be called explicitly.** They are invoked automatically.
2. Use triggers judiciously, as they can impact performance.
3. Avoid writing triggers that result in infinite recursion (e.g., a trigger that modifies the same table it is triggered on).