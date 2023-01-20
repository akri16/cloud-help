Engine
	- Initializes a Pool of DBAPI connections
	- This is created once for the lifetime of the application
	- Connection returned under engine.Connection is a proxy to the actual DBAPI connection

	- Using the python context manager with engine.connect() as conn: the closing of connection is automatically managed
	- Engine.connect() is rolled back once the context manager exits, engine.begin auto commits and rollbacks in case of an error
	

User Defined Session variables
Use  SET @<var_name> = '<value>';

	
Transactions and Locking

Transaction Isolation Levels
	1. Dirty Read: Occurs when one client views uncommited data of another transaction and when the transaction rolls back, the client with the data has "dirty data"
	2. Repeatable Reads: A client in a transaction won't see the commited changes made by other transactions until it exits and starts a new transaction
	3. Phantom Read: Here, the client will see the commited changes from other transactions when the changes result in new matches to your wheer clause


MySQL supports the following transaction isolation levels:
READ UNCOMMITTED
The transaction allows dirty, nonrepeatable, and phantom reads.
READ COMMITTED
The transaction does not allow dirty reads, but allows nonrepeatable and phantom reads. 
REPEATABLE READ
The transaction allows committed, repeatable reads and phantom reads. Nonrepeatable reads are not allowed. 99.99% time you need this
SERIALIZABLE
The transaction allows only committed, repeatable reads. Phantom reads are specifically not allowed.
From <https://learning.oreilly.com/library/view/managing-using/0596002114/ch08s02s02.html#msql2-CHP-8-SECT-2.2.2> 


	- MYSQL has autocommit set on by default, which means it automatically commits after every statement.

SLA - ACID
	1. Atomicity - All or Nothing
	2. Consistency - Doesn't violate the constraints
	3. Isolated - Results are independent in concurrent transactions
	4. Durable: Sustains disk/power failures

Transaction lifecycle
	1. Begin
	2. Save Point
	3. Commit - To finalize. (Has some cost if done frequently)
	4. Rollback - To rollback to initial state or to a save point
	


Transaction handling while using REPEATABLE-READ isolation method
	
	- When you execute an update in a transaction, by default, it locks the row you have updated/inserted for further updates in other sessions until the transaction is committed.
	- However you can still:
		○ Read from an updated row
		○ Read rows without locking them
	- If you are selecting a value for updating something inside a transaction and you don't want the record to be changed after the select you can use FOR UPDATE. This statement will also not run if there is an uncommitted update pending. For eg. You can use this for increasing monetary values. This solves the lost update problem in DBMS
	- You can combine FOR UPDATE with NO WAIT if you want it to fail in case there is an uncommitted change on that record

Pagination
	- You can implement pagination using the LIMIT and OFFSET clauses
![image](https://user-images.githubusercontent.com/54491362/213761956-0779f805-74e5-4ac4-a790-9fda47933677.png)
