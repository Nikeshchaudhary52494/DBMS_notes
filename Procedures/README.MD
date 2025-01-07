A **procedure** in PL/SQL is a named block of PL/SQL code that performs one or more specific tasks. Procedures are similar to functions but do not return a value directly. Instead, they may modify the values of OUT parameters or perform operations like database updates, logging, or business logic processing.

---

### **Structure of a Procedure in PL/SQL**

A procedure has three main sections:
1. **Header**: Includes the procedure's name and optional parameters.
2. **Declaration Section**: Declares variables, constants, and cursors (optional).
3. **Execution Section**: Contains the procedural logic (mandatory).
4. **Exception Section**: Handles exceptions or errors (optional).

---

### **Syntax for Creating a Procedure**

```sql
CREATE OR REPLACE PROCEDURE procedure_name (
    parameter_name [IN | OUT | IN OUT] data_type,
    ...
) IS
    -- Declarations (optional)
BEGIN
    -- Logic/SQL statements
EXCEPTION
    -- Exception-handling code (optional)
END procedure_name;
```

---

### **Components of the Syntax**

1. **Parameters:**
   - `IN`: Input parameter; passes a value into the procedure.
   - `OUT`: Output parameter; returns a value to the caller.
   - `IN OUT`: Both input and output parameter; passes a value into the procedure and returns a modified value.

2. **Declaration Section**:
   - Used to declare local variables, constants, or cursors.

3. **Execution Section**:
   - Contains SQL queries or PL/SQL statements that perform the procedure's intended task.

4. **Exception Section**:
   - Handles runtime errors or exceptions raised during execution.

---

### **Example 1: A Simple Procedure**

#### Use Case: Insert a new record into a table.

```sql
CREATE OR REPLACE PROCEDURE insert_employee (
    emp_id IN NUMBER,
    emp_name IN VARCHAR2,
    emp_salary IN NUMBER
) IS
BEGIN
    INSERT INTO employees (id, name, salary)
    VALUES (emp_id, emp_name, emp_salary);
    
    DBMS_OUTPUT.PUT_LINE('Record inserted successfully');
END insert_employee;
```

---

### **Example 2: Procedure with IN and OUT Parameters**

#### Use Case: Calculate and return the total salary of all employees.

```sql
CREATE OR REPLACE PROCEDURE calculate_total_salary (
    total_salary OUT NUMBER
) IS
BEGIN
    SELECT SUM(salary)
    INTO total_salary
    FROM employees;
END calculate_total_salary;
```

---

### **Example 3: Procedure with Exception Handling**

#### Use Case: Handle unique constraint violation during an insert.

```sql
CREATE OR REPLACE PROCEDURE safe_insert_employee (
    emp_id IN NUMBER,
    emp_name IN VARCHAR2,
    emp_salary IN NUMBER
) IS
BEGIN
    INSERT INTO employees (id, name, salary)
    VALUES (emp_id, emp_name, emp_salary);
    
    DBMS_OUTPUT.PUT_LINE('Employee inserted successfully');
EXCEPTION
    WHEN DUP_VAL_ON_INDEX THEN
        DBMS_OUTPUT.PUT_LINE('Error: Duplicate ID. Record not inserted.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END safe_insert_employee;
```

---

### **Executing a Procedure**

1. **Anonymous Block:**
   You can execute a procedure from an anonymous block using the `EXECUTE` statement or `CALL`.

```sql
BEGIN
    insert_employee(101, 'John Doe', 50000);
END;
```

2. **Using `EXECUTE`:**
```sql
EXECUTE insert_employee(101, 'John Doe', 50000);
```

3. **Calling a Procedure with OUT Parameters:**
   Use a variable to capture the OUT parameter.

```sql
DECLARE
    total_salary NUMBER;
BEGIN
    calculate_total_salary(total_salary);
    DBMS_OUTPUT.PUT_LINE('Total Salary: ' || total_salary);
END;
```

---

### **Key Features of PL/SQL Procedures**

1. **Reusable Code**: Procedures can be called multiple times, reducing code duplication.
2. **Modularization**: Procedures help organize code into smaller, manageable units.
3. **Improved Performance**: Stored procedures are precompiled, reducing execution time.
4. **Security**: Access control can be enforced by granting execute privileges.

---

### **Best Practices**
1. Use meaningful names for procedures and parameters.
2. Handle exceptions properly to avoid runtime errors.
3. Document procedures with comments for clarity.
4. Use OUT parameters only when necessary.
5. Avoid excessive logic inside a single procedure—opt for modularization.