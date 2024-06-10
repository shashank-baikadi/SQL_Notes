
When discussing databases, it’s essential to understand the difference between SQL and NoSQL databases, as each has its own set of advantages and limitations. In this section, we’ll briefly compare and contrast the two, so you can determine which one suits your needs better.

## SQL Databases

SQL (Structured Query Language) databases are also known as relational databases. They have a predefined schema, and data is stored in tables consisting of rows and columns. SQL databases follow the ACID (Atomicity, Consistency, Isolation, Durability) properties to ensure reliable transactions. Some popular SQL databases include MySQL, PostgreSQL, and Microsoft SQL Server.

**Advantages of SQL databases:**

- **Predefined schema**: Ideal for applications with a fixed structure.
- **ACID transactions**: Ensures data consistency and reliability.
- **Support for complex queries**: Rich SQL queries can handle complex data relationships and aggregation operations.
- **Scalability**: Vertical scaling by adding more resources to the server (e.g., RAM, CPU).

1. **Atomicity (All or Nothing):** Imagine you have a toy box. When you play with your toys, you take all of them out, and when you're done, you put all of them back. If you can't put all the toys back (maybe you get called to dinner), then you don't put any toys back. This way, your room is either fully clean or fully messy, never halfway.
    
2. **Consistency (Rules are Followed):** Think of a game you play with your friends. There are rules that everyone follows, like taking turns. If someone doesn’t follow the rules, the game gets spoiled. Consistency means that even when you’re playing alone, you always follow the same rules so the game makes sense.
    
3. **Isolation (Play by Yourself):** Imagine you're building a puzzle. If your friend is building another puzzle next to you, you don’t want them to mix their pieces with yours. Isolation means that you each work on your own puzzle without mixing up the pieces, so you both can finish your puzzles correctly.
    
4. **Durability (Never Forget):** Think of a drawing you made. After you finish it, you show it to your parents and they put it on the fridge. Even if your drawing pad gets lost or you accidentally erase the picture, the drawing on the fridge stays safe. Durability means that once something is done and saved, it stays there even if things go wrong elsewhere.
    

So, in short:

- **Atomicity:** Either all your toys are put back or none at all.
- **Consistency:** Always follow the game rules.
- **Isolation:** Don’t mix your puzzle pieces with your friend’s.
- **Durability:** Your drawing stays safe on the fridge

### 1. Atomicity

**Definition:** Atomicity ensures that a series of database operations within a transaction are treated as a single, indivisible unit. This means that either all the operations are executed successfully, or none of them are. If any operation fails, the entire transaction is rolled back to its previous state, ensuring that partial updates do not occur.

**Example:**

`BEGIN TRANSACTION;  UPDATE Accounts SET balance = balance - 100 WHERE account_id = 1;  UPDATE Accounts SET balance = balance + 100 WHERE account_id = 2;  COMMIT;`

If any of the `UPDATE` statements fail (e.g., due to insufficient funds), the transaction will be rolled back, leaving both accounts unchanged.

### 2. Consistency
 
**Definition:** Consistency ensures that a transaction takes the database from one valid state to another, maintaining the integrity of the data. This means that all rules, such as constraints, cascades, triggers, and any combination thereof, are upheld throughout the transaction.

**Example:**

`-- Assuming a constraint that ensures balance cannot be negative  BEGIN TRANSACTION;  UPDATE Accounts SET balance = balance - 200 WHERE account_id = 1;  UPDATE Accounts SET balance = balance + 200 WHERE account_id = 2;  COMMIT;`

If the `balance` of `account_id = 1` becomes negative, the transaction will fail and rollback, ensuring that the database remains consistent.

### 3. Isolation

**Definition:** Isolation ensures that transactions occur independently without interference from concurrent transactions. This means that the intermediate state of a transaction is invisible to other transactions. SQL standards define different isolation levels to balance between performance and strict isolation.

**Example:**


`-- Isolation Level: Serializable SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;  BEGIN TRANSACTION;  SELECT balance FROM Accounts WHERE account_id = 1;  UPDATE Accounts SET balance = balance - 50 WHERE account_id = 1;  COMMIT;`

Under the Serializable isolation level, other transactions cannot access the `Accounts` table until the current transaction is complete, preventing dirty reads, non-repeatable reads, and phantom reads.

### 4. Durability

**Definition:** Durability ensures that once a transaction has been committed, it will remain so, even in the event of a system failure. This means that the results of a committed transaction are permanently recorded in the database.

**Example:**


`BEGIN TRANSACTION;  UPDATE Orders SET status = 'Shipped' WHERE order_id = 123;  COMMIT;`

Once the `COMMIT` statement is executed, the change to the `Orders` table (setting the status to 'Shipped') is guaranteed to be permanent, even if the system crashes immediately after the commit.

### Bringing It All Together

Consider a bank transfer transaction as an example to illustrate all ACID properties:


`-- Atomicity BEGIN TRANSACTION;  -- Consistency UPDATE Accounts SET balance = balance - 500 WHERE account_id = 1;  -- Isolation UPDATE Accounts SET balance = balance + 500 WHERE account_id = 2;  -- Durability COMMIT;`

- **Atomicity:** The transaction either fully completes (both updates are successful) or is fully rolled back if any update fails.
- **Consistency:** The transaction adheres to rules such as non-negative balances.
- **Isolation:** Other transactions cannot see the intermediate states of this transaction.
- **Durability:** Once committed, the changes are permanent.

This ensures the transaction is reliable, adheres to all rules, and is safely stored, reflecting the importance of ACID properties in SQL database management.

**Limitations of SQL databases:**

- **Rigid schema**: Data structure updates are time-consuming and can lead to downtime.
- **Scaling**: Difficulties in horizontal scaling and sharding of data across multiple servers.
- **Not well-suited for hierarchical data**: Requires multiple tables and JOINs to model tree-like structures.

## NoSQL Databases

NoSQL (Not only SQL) databases refer to non-relational databases, which don’t follow a fixed schema for data storage. Instead, they use a flexible and semi-structured format like JSON documents, key-value pairs, or graphs. MongoDB, Cassandra, Redis, and Couchbase are some popular NoSQL databases.

**Advantages of NoSQL databases:**

- **Flexible schema**: Easily adapts to changes without disrupting the application.
- **Scalability**: Horizontal scaling by partitioning data across multiple servers (sharding).
- **Fast**: Designed for faster read and writes, often with a simpler query language.
- **Handling large volumes of data**: Better suited to managing big data and real-time applications.
- **Support for various data structures**: Different NoSQL databases cater to various needs, like document, graph, or key-value stores.

**Limitations of NoSQL databases:**

- **Limited query capabilities**: Some NoSQL databases lack complex query and aggregation support or use specific query languages.
- **Weaker consistency**: Many NoSQL databases follow the BASE (Basically Available, Soft state, Eventual consistency) properties that provide weaker consistency guarantees than ACID-compliant databases.

## MongoDB: A NoSQL Database

This guide focuses on MongoDB, a popular NoSQL database that uses a document-based data model. MongoDB has been designed with flexibility, performance, and scalability in mind. With its JSON-like data format (BSON) and powerful querying capabilities, MongoDB is an excellent choice for modern applications dealing with diverse and large-scale data.

- [NoSQL vs. SQL Databases](https://www.mongodb.com/nosql-explained/nosql-vs-sql)