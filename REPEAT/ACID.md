# ACID & TRANSACTION

Certainly! ACID stands for Atomicity, Consistency, Isolation, and Durability. These are the four key properties that ensure the reliability and integrity of transactions in a database management system (DBMS). Let's break down each property with examples:

1. **Atomicity**:
   - Atomicity ensures that a transaction is treated as a single unit of work. Either all of the operations within the transaction are completed successfully, or none of them are.
   - If any part of the transaction fails, the entire transaction is rolled back to its original state, as if it had never occurred.
   - Example: Consider a bank transfer where money is withdrawn from one account and deposited into another. Atomicity ensures that both the withdrawal and the deposit occur together. If the withdrawal is successful but the deposit fails (due to a system error, for instance), the entire transaction is rolled back, and the money is returned to the original account.

2. **Consistency**:
   - Consistency ensures that the database remains in a consistent state before and after the transaction, regardless of any concurrent transactions or system failures.
   - All constraints, rules, and relationships defined in the database schema must be maintained to ensure data integrity.
   - Example: If a database constraint specifies that every customer must have a valid email address, consistency ensures that no transaction can leave the database in a state where a customer record exists without a valid email address.

3. **Isolation**:
   - Isolation ensures that transactions operate independently of each other, even if they are executed concurrently.
   - Each transaction should be isolated from other transactions until it is completed and committed.
   - This prevents interference between transactions, ensuring that the outcome of one transaction does not affect the outcome of another.
   - Example: Suppose two users concurrently try to update the same bank account balance. Isolation ensures that each user sees the bank account balance as it was before the other user's transaction started. This prevents one user's transaction from being affected by the other user's updates until the transactions are completed.

4. **Durability**:
   - Durability ensures that the changes made by a committed transaction persist even in the event of a system failure or crash.
   - Once a transaction is committed, its changes are permanently saved to the database and cannot be lost.
   - This is typically achieved through mechanisms such as write-ahead logging or database backups.
   - Example: After a successful fund transfer in a banking system, the updated account balances must be permanently saved to the database. Even if the system crashes immediately after the transaction is committed, the changes should still be reflected when the system is restarted.

In summary, the ACID properties provide a set of guarantees that transactions in a DBMS should adhere to, ensuring data integrity, reliability, and consistency. These properties are essential for maintaining the correctness and reliability of database operations, particularly in systems where multiple transactions may occur concurrently.


## Transaction

A transaction in a database is a logical unit of work that consists of one or more database operations, such as inserts, updates, or deletes, that are treated as a single indivisible task. Transactions ensure the integrity, consistency, and durability of data in the database by adhering to the ACID properties:


**Example**:
Let's consider a scenario where a customer transfers funds from one account to another in a banking system. The transaction involves deducting funds from the sender's account and adding funds to the recipient's account. 

```sql
START TRANSACTION; -- Start of the transaction

-- Deduct funds from the sender's account
UPDATE accounts
SET balance = balance - 1000
WHERE account_number = 'sender_account_number';

-- Add funds to the recipient's account
UPDATE accounts
SET balance = balance + 1000
WHERE account_number = 'recipient_account_number';

COMMIT; -- End of the transaction, commit changes

```

In this example, the transaction ensures that both the deduction from the sender's account and the addition to the recipient's account occur together as a single unit of work. If any part of the transaction fails (e.g., due to insufficient funds or a system error), the entire transaction is rolled back, and both accounts return to their original state.

This ensures that the database remains in a consistent state, and changes made by the transaction are either fully applied or fully undone. Additionally, the changes are durable and persist even in the event of a system failure.


A transaction is a unit or sequence of work that is performed on a database. Transactions are accomplished in a logical order, whether in a manual fashion by a user or automatically by some sort of a database program.


A transaction is the propagation of one or more changes to the database. For example, if you are creating, updating or deleting a record from the table, then you are performing a transaction on that table. It is important to control these transactions to ensure the data integrity and to handle database errors.


Practically, you will club many SQL queries into a group and you will execute all of them together as a part of a transaction.


Transactional control commands are only used with the DML Commands such as - INSERT, UPDATE and DELETE. They cannot be used while creating tables or dropping them because these operations are automatically committed in the database. Following commands are used to control transactions.

COMMIT − to save the changes.

ROLLBACK − to roll back the changes.

SAVEPOINT − creates points within the groups of transactions in which to ROLLBACK.

SET TRANSACTION − Places a name on a transaction.

Sure, let's explain these concepts in the context of a transaction:

1. **COMMIT**:
   - `COMMIT` is a SQL command used to permanently save the changes made by a transaction to the database.
   - When a transaction is committed, all the changes made by the transaction become permanent and visible to other transactions.
   - Once committed, the changes cannot be rolled back, and they persist even in the event of a system failure.
   - Example:
     ```sql
     COMMIT;
     ```

2. **ROLLBACK**:
   - `ROLLBACK` is a SQL command used to undo the changes made by a transaction and restore the database to its previous state.
   - It is typically used when a transaction encounters an error or needs to be canceled for some reason.
   - When a transaction is rolled back, all the changes made by the transaction are undone, and the database returns to its state before the transaction began.
   - Example:
     ```sql
     ROLLBACK;
     ```

3. **SAVEPOINT**:
   - `SAVEPOINT` is a SQL command used to set a named point within a transaction to which you can later roll back.
   - It allows you to create intermediate points within a transaction so that you can roll back to a specific point without rolling back the entire transaction.
   - It is useful for implementing more complex rollback scenarios or for breaking a transaction into smaller, more manageable parts.
   - Example:
     ```sql
     SAVEPOINT sp1;
     ```

4. **SET TRANSACTION**:
   - `SET TRANSACTION` is a SQL command used to set properties for the current transaction, such as isolation level or transaction access mode.
   - It allows you to specify transaction-specific settings before beginning a transaction.
   - This command is typically used in advanced scenarios where you need to customize the behavior of transactions.
   - Example:
     ```sql
     SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
     ```

These commands are essential for managing transactions in a database system. They provide control over the behavior of transactions and ensure data integrity and consistency.
