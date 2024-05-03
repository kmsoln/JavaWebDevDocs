# **Introduction to Transactions**

## **What are transactions?**
Transactions are units of work performed within a database management system (DBMS) that must be executed as a whole. They represent a sequence of database operations (such as reads, writes, updates, and deletes) that are treated as a single logical unit. Transactions ensure data integrity by either completing all of their operations successfully (committing) or reverting any changes made if an error occurs (rolling back).

## **Why are transactions important in databases?**
Transactions are crucial in databases because they ensure data consistency and integrity, even in the presence of concurrent access and system failures. By grouping database operations into transactions, it's possible to maintain the ACID properties, which guarantee that transactions are executed reliably and predictably.

## **When we use transactions?**
Transactions are used in database systems to ensure data integrity and consistency when performing multiple related operations.  Here are some situations where you might need to use transactions from a logical standpoint:

1. **Maintaining Data Integrity**: If your application performs operations that involve modifying multiple records or tables in a way that they must remain consistent with each other, you would use a transaction. For example, if you're updating a customer's order and also deducting inventory from the product stock, you want these operations to happen together to maintain data integrity.

2. **Ensuring Consistency**: When you need to enforce business rules that involve multiple steps, transactions help ensure that all steps are completed successfully or none at all. For instance, when processing an online order, you may need to verify the customer's payment, update inventory, and send a confirmation email. Transactions ensure that either all of these steps are completed, or none are, maintaining consistency.

3. **Preventing Race Conditions**: In multi-user environments where multiple users might access and modify the same data concurrently, transactions help prevent race conditions by ensuring that each operation is isolated from others until it's completed. This isolation prevents conflicts and ensures that each transaction sees a consistent view of the data.

4. **Rollback on Failure**: Transactions provide a mechanism to rollback changes if an error occurs during the execution of any operation within the transaction. This rollback capability helps maintain data integrity by reverting the database to its original state if something goes wrong.

5. **Complex Business Processes**: In applications with complex business processes involving multiple steps, transactions help ensure that the entire process is completed successfully or rolled back if any part fails. This guarantees that the system remains in a consistent state regardless of failures.

## **ACID properties of transactions**
ACID is an acronym that stands for:
  - **Atomicity**: Transactions are atomic, meaning that either all of their operations are completed successfully, or none of them are. There are no partial or intermediate states.
  - **Consistency**: Transactions maintain the consistency of the database by transforming it from one valid state to another valid state. Constraints, such as foreign key constraints and uniqueness constraints, are enforced during transactions.
  - **Isolation**: Transactions are isolated from each other to prevent interference or inconsistency caused by concurrent transactions. Isolation ensures that each transaction sees a consistent snapshot of the database.
  - **Durability**: Once a transaction is committed, its changes are permanent and will survive system failures. Durability is achieved through mechanisms like transaction logs and database backups.

## **Transaction Isolation Levels**

### **Read Uncommitted**
In the Read Uncommitted isolation level, transactions can read data that has been modified by other transactions but not yet committed. This level offers the lowest level of isolation and can lead to phenomena such as dirty reads.

### **Read Committed**
In the Read Committed isolation level, transactions can only read data that has been committed by other transactions. This level prevents dirty reads but allows non-repeatable reads and phantom reads.

### **Repeatable Read**
In the Repeatable Read isolation level, transactions maintain a consistent view of the data throughout their execution. This level prevents non-repeatable reads but allows phantom reads, where new rows matching the search conditions may appear during the transaction.

### **Serializable**
In the Serializable isolation level, transactions are executed as if they were the only transactions running on the database. This level provides the highest level of isolation, preventing dirty reads, non-repeatable reads, and phantom reads.

### **Choosing the appropriate isolation level**
The choice of isolation level depends on the specific requirements of the application and the trade-offs between consistency and concurrency. It's essential to consider factors such as data access patterns, transaction throughput, and the risk of concurrency-related anomalies when selecting the appropriate isolation level. 

## **Transaction Management**

### **Beginning and ending transactions**
Transactions begin with the execution of a transaction-start command (e.g., BEGIN TRANSACTION) and end with either a commit or rollback operation. Beginning a transaction marks the start of a logical unit of work, while ending a transaction either confirms or discards the changes made during the transaction.

### **Committing and rolling back transactions**
Committing a transaction applies all of its changes to the database, making them permanent. Rolling back a transaction undoes all of its changes, restoring the database to its state before the transaction began. Commit and rollback operations are crucial for maintaining data consistency and integrity.

### **Savepoints**
Savepoints allow transactions to be divided into smaller units of work, enabling partial rollback and recovery. By setting savepoints within a transaction, it's possible to roll back to a specific point in the transaction without undoing all of its changes. Savepoints provide flexibility and granularity in transaction management.

## **Transaction Logs**

### **Importance of transaction logs**
Transaction logs record all changes made to the database during transactions, providing a durable record of transactional activity. Transaction logs are essential for ensuring durability, enabling recovery from system failures, and supporting features such as point-in-time recovery and replication.

### **Redo and undo operations**
Redo and undo operations are used during transaction recovery to bring the database back to a consistent state after a failure. Redo operations reapply committed transactions from the transaction log to recreate changes made since the last checkpoint, while undo operations roll back uncommitted transactions to discard their changes.

## Annotations
in annotation folder you will find a set of files that represents every annotation. we should add the mentioned titles under this text, as you see why explain everything and then we add an example for usage
1. **`@EnableTransactionManagement`**:
    - **Explanation**: This annotation is used to enable Spring's annotation-driven transaction management capability in a Spring application. It typically goes on the main configuration class of a Spring Boot application. Once enabled, Spring will scan for `@Transactional` annotations on classes and methods and automatically apply transactional behavior to those methods.
    - **Properties**: This annotation doesn't have any specific properties, but it enables Spring's annotation-driven transaction management capability in a Spring application.
    - **When to Use**: Use this annotation in your Spring Boot application's main configuration class to enable Spring's annotation-driven transaction management capability. Use it when you want Spring to automatically manage transactions based on `@Transactional` annotations.

2. **`@TransactionalEventListener`**:
    - **Explanation**: This annotation is used to mark methods as event listeners for transactional events. These methods are invoked when a transaction completes successfully or fails. The `phase` attribute can be used to specify when the event listener should be invoked relative to the transaction phase. Phases include `AFTER_COMMIT`, `AFTER_ROLLBACK`, and `AFTER_COMPLETION`.
    - **Properties**: This annotation doesn't have specific properties, but it's often used with the `phase` attribute to specify when the event listener should be invoked relative to the transaction phase. Phases include `AFTER_COMMIT`, `AFTER_ROLLBACK`, and `AFTER_COMPLETION`.
    - **When to Use**: Use this annotation when you need to perform additional actions based on the outcome of a transaction. For example, you might want to send notifications or trigger other business processes after a transaction completes successfully or fails.

3. **`@Transactional(propagation)`**:
      - **Explanation**: This annotation is used to specify the propagation behavior of the transaction. Propagation defines how transactions should behave when multiple methods are invoked within the same transactional context.
      - **Propagation Types**:
        - `REQUIRED`: If a transaction exists, use it. Otherwise, create a new one.
        - `REQUIRES_NEW`: Always create a new transaction.
        - `NESTED`: Execute within a nested transaction if a current transaction exists, otherwise behave like `REQUIRED`.
      - **When to Use**: Use this annotation to specify the propagation behavior of the transaction. Choose the appropriate propagation type based on how you want transactions to behave when multiple methods are invoked within the same transactional context. For example:
        - Use `REQUIRED` when you want methods to share the same transaction if one exists, otherwise create a new transaction.
        - Use `REQUIRES_NEW` when you always want to create a new transaction, regardless of whether one exists.
        - Use `NESTED` when you want to execute within a nested transaction if a current transaction exists, otherwise behave like `REQUIRED`.

4. **`@Transactional(isolation)`**:
     - **Explanation**: This annotation is used to specify the isolation level of the transaction. Isolation levels determine how transactions should interact with concurrent transactions accessing the same data.
     - **Isolation Levels**:
        - `READ_UNCOMMITTED`: Allows dirty reads, non-repeatable reads, and phantom reads.
        - `READ_COMMITTED`: Prevents dirty reads, allows non-repeatable reads, but may allow phantom reads.
        - `REPEATABLE_READ`: Prevents dirty reads and non-repeatable reads, but may allow phantom reads.
        - `SERIALIZABLE`: Prevents dirty reads, non-repeatable reads, and phantom reads by ensuring serializable transactions.
     - **When to Use**: Use this annotation to specify the isolation level of the transaction based on your concurrency requirements. Choose the appropriate isolation level to control how transactions interact with concurrent transactions accessing the same data. For example:
       - Use `READ_COMMITTED` if dirty reads are not acceptable and you can tolerate non-repeatable reads.
       - Use `SERIALIZABLE` if you need the highest level of isolation to prevent dirty reads, non-repeatable reads, and phantom reads.
     
5. **`@Transactional(timeout)`**:
    - **Explanation**: This annotation is used to specify the timeout for the transaction in seconds. If the transaction takes longer than the specified timeout, it will be automatically rolled back. This is useful for preventing long-running transactions that may cause performance issues or deadlock situations.
    - **Properties**: Specifies the timeout for the transaction in seconds. If the transaction takes longer than the specified timeout, it will be automatically rolled back.
    - **When to Use**: Use this annotation to specify a timeout for the transaction in seconds. Use it when you want to prevent long-running transactions that may cause performance issues or deadlock situations. For example, you might set a timeout for transactions involving external services or complex operations to ensure they don't block resources indefinitely.

6. **`@Transactional(readOnly)`**:
    - **Explanation**: This annotation is used to mark a transaction as read-only. When set to `true`, it indicates that the transaction only reads data and does not perform any write operations. This can provide performance benefits because it allows the underlying database to optimize read operations.
    - **Properties**: Marks a transaction as read-only, allowing the underlying database to optimize read operations. It's a boolean attribute with a default value of `false`.
    - **When to Use**: Use this annotation to mark a transaction as read-only when you only need to read data and don't perform any write operations. Use it to optimize read operations and improve performance. For example, you might use it for read-only operations like fetching data for display purposes or reporting.

7. **`@Rollback`**:
    - **Explanation**: This annotation is typically used in conjunction with `@Transactional` in integration tests. It controls the rollback behavior of a test method. If `@Rollback` is set to `true`, the transaction will be rolled back after the test method completes, ensuring that the test environment remains unchanged. This is useful for ensuring that tests do not have side effects on the database.
    - **Properties**: This annotation is typically used in conjunction with `@Transactional` in integration tests. It controls the rollback behavior of a test method. If `@Rollback` is set to `true`, the transaction will be rolled back after the test method completes, ensuring that the test environment remains unchanged.
    - **When to Use**: Use this annotation in integration tests when you want to control the rollback behavior of a test method. Set `@Rollback(true)` to ensure that the transaction is rolled back after the test method completes, ensuring that the test environment remains unchanged. Use it to prevent side effects on the database caused by test execution.

    