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

**Advantages of Procedures in PL/SQL:**

* **Performance:**
    * **Reduced Network Traffic:** Stored procedures execute on the database server, minimizing data transfer between the application and the database. This significantly reduces network traffic and improves performance.
    * **Pre-compiled Code:** Procedures are compiled once and stored in the database. This eliminates the need for repeated compilation, leading to faster execution times.
    * **Optimized Execution:** The database engine can optimize the execution plan for a stored procedure, resulting in more efficient processing.

* **Reusability:**
    * **Modular Design:** Procedures encapsulate specific tasks, making them reusable across different applications and parts of the same application. This reduces code duplication and improves code maintainability.

* **Security:**
    * **Centralized Access Control:** Database administrators can grant or deny access to specific procedures, enhancing data security.
    * **Reduced Exposure:** By encapsulating business logic within procedures, you minimize the exposure of sensitive data to the application layer.

* **Maintainability:**
    * **Easier to Modify:** Changes to business logic can be made in one place (the procedure) and easily propagated to all applications that use it.
    * **Improved Code Organization:** Procedures promote a structured and modular approach to database development, making code easier to understand and maintain.

* **Data Integrity:**
    * **Enforce Business Rules:** Procedures can be used to enforce complex business rules and constraints, ensuring data consistency and integrity.

**Disadvantages of Procedures in PL/SQL:**

* **Complexity:**
    * **Development and Debugging:** Developing and debugging complex procedures can be more challenging than writing simple SQL statements.
    * **Maintenance:** Maintaining large and complex procedures can be time-consuming and error-prone.

* **Portability:**
    * **Database Dependency:** Procedures are typically specific to the database system they are created in. Porting procedures to another database system can be difficult and may require significant modifications.

* **Performance Issues:**
    * **Overly Complex Procedures:** Inefficiently designed procedures can negatively impact database performance.
    * **Resource Consumption:** Procedures consume database resources, and excessive use can lead to performance bottlenecks.

* **Debugging Challenges:**
    * **Limited Debugging Tools:** Debugging stored procedures can be more challenging compared to client-side code due to limited debugging tools and environments.

* **Security Risks:**
    * **Vulnerabilities:** Poorly written procedures can introduce security vulnerabilities, such as SQL injection.

In summary, PL/SQL procedures offer significant advantages in terms of performance, reusability, security, and maintainability. However, they also have potential drawbacks, including complexity, portability issues, and potential performance impacts if not designed and implemented carefully. 

The decision to use procedures should be based on a thorough evaluation of the specific needs and requirements of the application.

## Exaple of procedure

```sql
CREATE OR REPLACE PROCEDURE calculate_total_price(
    product_id IN NUMBER,
    quantity IN NUMBER,
    total_price OUT NUMBER
)
IS
    unit_price NUMBER; 
BEGIN
    -- Declare and initialize local variable
    unit_price := 0; 

    SELECT price 
    INTO unit_price
    FROM products
    WHERE product_id = product_id;

    total_price := unit_price * quantity;
END calculate_total_price;
/
```

**Explanation:**

1. **Procedure Definition:**
   - `CREATE OR REPLACE PROCEDURE`: Defines a procedure named `calculate_total_price`.
   - `product_id IN NUMBER`: Input parameter for the product ID.
   - `quantity IN NUMBER`: Input parameter for the quantity.
   - `total_price OUT NUMBER`: Output parameter to store the calculated total price.

2. **Local Variable Declaration:**
   - `unit_price NUMBER;`: Declares a local variable named `unit_price` of type `NUMBER` to store the unit price of the product.

3. **Procedure Body:**
   - `SELECT price INTO unit_price ...`: Retrieves the unit price of the product from the `products` table and stores it in the `unit_price` variable.
   - `total_price := unit_price * quantity;`: Calculates the total price by multiplying the `unit_price` with the `quantity` and assigns the result to the `total_price` output parameter.

**How to Execute the Procedure:**

```sql
DECLARE
    l_total_price NUMBER;
BEGIN
    calculate_total_price(101, 5, l_total_price); -- Call the procedure with input values
    DBMS_OUTPUT.PUT_LINE('Total Price: ' || l_total_price); 
END;
/
```

**Explanation:**

1. **DECLARE Block:**
   - `l_total_price NUMBER;`: Declares a local variable to store the result of the procedure call.

2. **Procedure Call:**
   - `calculate_total_price(101, 5, l_total_price);`: Calls the `calculate_total_price` procedure with the following arguments:
      - `product_id`: 101
      - `quantity`: 5
      - `l_total_price`: The variable to receive the calculated total price.

3. **Output:**
   - `DBMS_OUTPUT.PUT_LINE(...)`: Displays the calculated `l_total_price` on the console.

This example demonstrates how to declare and use local variables within a PL/SQL procedure, as well as how to execute the procedure and retrieve the output value.
