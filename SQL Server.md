### Creating altering and dropping a database
* A SQL Server database can be created, altered and dropped
 1. Graphically using SQL Server Management Studio (SSMS) or
 2. Using a Query
 
* To Create the database using a query

>  ```sql
> Create database DatabaseName
>```
* Whether, you create a database graphically using the designer or, using a query, the following 2 files gets generated

  **.MDF file - Data File (Contains actual data)   
  .LDF file - Transaction Log File (Used to recover the database)**

* To alter a database, once it's created
  
> ```sql
>   Alter database DatabaseName   
>   Modify Name = NewDatabaseName
> ```

* Alternatively, you can also use system stored procedure
 Execute the following:
 
>```sql
> sp_renameDB 'OldDatabaseName','NewDatabaseName'
>```
 
 #### Deleting or Dropping a database
 
 * To Delete or Drop a database

>```sql
>  Drop Database DatabaseThatYouWantToDrop
>```
 
* Dropping a database, deletes the LDF and MDF files.
* You cannot drop a database, if it is currently in use. You get an error starting - _Cannot drop because "NewDatabaseName" because it is currently in use._ 
* So, if other users are connected, you need to put the database in single user mode and then drop the database.

>```sql
> Alter Database DatabaseName  
> Set SINGLE_USER   
> With Rollback Immediate
>```

* With Rollback Immediate option, will rollback all incomplete transactions and closes the connection to the database.
* **Note: System databases cannot be dropped.**

     ![image](https://user-images.githubusercontent.com/58625165/210257644-16d03262-b9e9-4c35-a895-88e41058ea75.png)
    
From GUI we can do it by checking _Close existing connections_ checkbox while deleting the database.
![image](https://user-images.githubusercontent.com/58625165/210257920-86e01763-8042-4080-983e-a6327dda7a27.png)


### Creating and working with tables

##### The aim of this section is to create tblPerson and tblGender tables and establish primarykey and foreign key constraints

![image](https://user-images.githubusercontent.com/58625165/210279960-2c4d9128-3118-4baa-b5ec-b8cacb093965.png)

> **In SQL Server, tables can be created graphically using SQL Server Management Studio (SSMS) or using a query. Foreign key references can be added graphically using SSMS or using a query**

>```sql
> Alter table ForeignKeyTable add constraint ForeignKeyTable_ForeignKeyColumn_FK  
> FOREIGN KEY (ForeignKeyColumn) references PrimaryKeyTable (PrimaryKeyColumn)
>```
>E.g.,
>```sql
>Alter table tblPerson add constraint tblPerson_GenderID_FK  
>Foreign Key (GenderId) references tblGender (ID)
>```

>_Foreign keys are used to enforce **database integrity**. In layman's terms, a Foreign key in one table points to primary key in another table. The foreign key constraint prevents invalid data form being inserted into the foreign key column. The values that you enter into the foreign key column, has to be one of the values contained in the table it points to._

>**For creating a table**
> ```sql
> Use [Sample]  
> Go  
> Create Table tblGender  
> (  
> ID int NOT NULL Primary Key,  
> Gender nvarchar(50) NOT NULL  
> )
> ```

### Adding a default constraint
> A column default can be specified using Default constraint. The DEFAULT constraint is used to insert a default value into a column. The default value will be added to all new records, if no other value is specified, including NULL.

> **Altering an existing column to add a default constraint:**
> ```sql
> ALTER TABLE _tablename_  
> ADD CONSTRAINT _constraint_name_  
> DEFAULT _default_value_ FOR _existing_column_value_
> ```
> E.g.,
> ```sql
> ALTER TABLE tblPerson  
> ADD CONSTRAINT DF_tblPerson_GenderId  
> DEFAULT 3 FOR GENDERID
> ```
 
> **Altering an new column, with default value, to an existing table:**
> ```sql
> ALTER TABLE _tablename_  
> ADD _column_name_ _data_type_ _NULL | NOT NULL_  
> CONSTRAINT _constraint_name_ DEFAULT _default_value_
> ```

> **Dropping a constraint:**
> ```sql
> ALTER TABLE _tablename_  
> DROP CONSTRAINT _constraint_name_
> ```
> E.g.,
> ```sql
> ALTER TABLE tblPerson  
> DROP CONSTRAINT DF_tblPerson_GenderId
> ```


### Cascading referential integrity constraint
> _Cascading refential integrity constraint allows to define the actions Microsoft SQL Server should take when a user attempts to delete or update a key to which an existing foreign key points._
> **For example,** If you delete row with ID = 1 from tblGender table, then row with ID = 3, from tblPerson table becomes an orphan record. You will not be able to tell the Gender for this row. So, Cascading referential integrity constraint can be used to define actions Microsoft SQL Server should take when this happens. By default, we get an error and the DELETE or UPDATE statement is rolled back.

> * Options when setting up Cascading refrential integrity constraint:
>
>  **1. No Action:** This is the default behaviour. No Action specifies that if an attempt is made to delete or update a row with a key referenced by foreign keys in existing rows in other tables, an error is raised and the DELETE or UPDATE is rolled back.
>  
>  **2. Cascade:** Specifies that if an attempt is made to delete or update a row with a key referenced by foreign keys in existing rows in other tables, all rows containing those foreign keys are also deleted or updated.
>
> **3. Set NULL:** Specifies that if an attempt is made to delete or update a row with a key referenced by foreign key in existing rows in other tables, all rows containing those foreign keys are set to NULL.
> 
> **4. Set Default:** Specifies that if an attempt is made to delete or update a row with a key referenced by foreing key in existing rows in other tables, all rows containing those foreign keys are set to default values.
> 
> 


### Adding a check constraint
> **DEF:** _CHECK constraint is used to limit the the range of the values, that can be entered for a column._
> **The general formula for adding check constraint in SQL Server:**
> ```sql
> ALTER TABLE _table_name_
> ADD CONSTRAINT _constraint_name_ CHECK _boolean_expression_
> ```
> If the BOOLEAN_EXPRESSION returns true, then the CHECK constraint allows the value, otherwise it doesn't. Since, AGE is a nullable column, it's possible to pass null for this column, when inserting a row. When you pass NULL for the AGE column, the boolean expression evaluates to UNKNOWN, and allows the value.
> **To drop the CHECK constraint:**
> ```sql
> ALTER TABLE tblPerson  
> DROP CONSTRAINT CK_tblPerson_Age
> ```
> E.g.,
> ```sql
> Alter Table tblPerson  
> Add Constraint CK_tblPerson_Age CHECK (AGE > 0 AND AGE < 150)
> ```

### Identity Column in SQL Server
> If we look GUI wise we have this option: 
> ![image](https://user-images.githubusercontent.com/58625165/210294265-8843da32-8bcf-4d74-87ed-bd7110ccd07d.png)
> So, in **Identity Specification** we have 2 properties: _Identity Increment_ (the value by which column value needs to be incremented) and _Identity Seed_ (the value by which column value needs to be started from).
> An explicit value for the identity column in table 'dbo.tblPerson1' can only be specified when a column list is used and IDENTITY_INSERT is ON.
> To turn IDENTITY_INSERT on, we can use the following command:
> ```sql
>  SET IDNTITY_INSERT tblPerson1 ON
> ```

> * If a column is marked as an identity column, then the values for this column are automatically generated, when you insert a new row into the table.
> ```sql
> Create Table tblPerson  
> (  
> PersonId int identity(1,1) Primary Key,  
> Name nvarchar(20)  
> )  
> ```
> **Note:** Seed and Increment values are optional. If you don't specify the identity and seed they both default to 1.

>* To explicitly supply a value for identity column
>  1. First turn on identity insert
>  ```sql
>   SET Identity_Insert tblPerson ON
>  ```
>  2. In the insert query specify the column list
>  ```sql
>   Insert into tblPerson(PersonId, Name) values(2, 'John')
>  ```

> * If you have deleted all the rows in a table, and you want to reset the identity column value, use **DBCC CHECKIDENT** command
> ```sql
>  DBCC CHECKIDENT ('tblPerson', RESEED, 0)
> ```

### How to get the last generated identity column value in SQL

**From the previous session, we understood that identity column values are auto generated. There are several ways in SQL Server, to retrieve the last identity value that is generated. The most common ways is to use SCOPE_IDENTITY() built in function.**  

**Note:** You can also use @@IDENTITY and IDENT_CURRENT('TableName')  

**Difference:**  
**SCOPE_IDENTITY()-** Same session and the same scope.  
**@@IDENTITY-** Same session and across any scope.  
**IDENT_CURRENT('TableName')-** Specific table across any session and any scope.

### Unique key constraint
> ##### We use UNIQUE constraint to enforce uniqueness of a column i.e. the column shouldn't allow any duplicate values. We can add a Unique constraint through the designer or using a query.
>* To create the unique key using a query:
>```sql
>Alter Table Table_Name  
>Add Constraint Constraint_Name Unique(Column_Name)
>```

> ##### Both primary key and unique key are used to enforce, the uniqueness of a column. So, when do you choose one over the other?
> * A table can have, only one primary key. If you want to enforce uniqueness on 2 or more columns, then we use unique key constraint.

> ##### What is the difference between Primary key constraint and Unique key constraint?
> 1. A table can have only one primary key, but more than one unique key
> 2. Primary key does not allow nulls, where as unique key allows one null (only one)

>**Syntax:**
>```sql
>Alter Table tblPerson  
>Add Constraint UQ_tblPerson_Email Unique(Email)
>```

### Select statment in sql server
> **Using DISTINCT Keyword with multiple columns:**
> ```sql
>  Select DISTINCT City from tblPerson
> ```
> _The above query will return distinct city names_
> On the other hand, the below query will return distinct values across given column names (not across same column)
> ```sql
>  Select DISTINCT Name, City from tblPerson
> ```
> ![image](https://user-images.githubusercontent.com/58625165/210430722-93231a13-1fee-4215-abeb-80db7ff11318.png)

>**Not equal to operator: <> or != in SQL Server:** 
>```sql
> Select * from tblPerson Where City != 'London';
> Select * from tblPerson Where City <> 'London'; 
>```

###### Operators and Wild cards:
>![image](https://user-images.githubusercontent.com/58625165/210431457-ca974a1e-2447-42ea-baa0-65102192f7d1.png)

>```sql
> Select * from tblPerson Where Age IN (20,23,29);
> Select * from tblPerson Where Age BETWEEN 20 AND 25;
> --- The boundary conditions in above BETWEEN query has 20 and 25 inclusive.
> --- Now, let's see the LIKE operator use:
> Select * from tblPerson Where City LIKE 'L%'; --- Which means that select all the cities which starts from the letter "L", and "%" is called a Wild Card
> Select * from tblPerson Where Email LIKE '_@_.com'
> Select * from tblPerson Where Name LIKE '[MST]%' -- The chracters in bracket means either M or S or T - is the first letter and then % means that there are letters > > ---after either of these three. 
> ---to get opposite of the above query, which is to get all the names doesn't start with letters M, S or T:
> Select * from tblPerson Where Name LIKE '[^MST]%' --- We have added the negate symbol (^);
> Select top 10 * from tblPerson; --- it will select first 10 records from the table (just change num in "top num")
> Select top 1 Percent * from tblPerson; --- it will select first 1 percent rows from the table 
>  Select top 1 * from tblPerson Order By Age DESC; --- it will return the person with the highest age (can be asked in an interview) 
>```
***Note:***_Any character value or a string value used in SQL Server should be wrapped inside single quote('')_


### Group by in sql server
### Joins in sql server
### Advanced or intelligent joins in sql server
### Self join in sql server
### Different ways to replace NULL in sql server
### Coalesce function in sql server
### Union and union all in sql server 
### Stored procedures in sql server
### Stored procedures with output parameters
### Stored prodedures output paramerters or return values
### Advantages of stored procedures
### Built in string functions in sql server 
### LEFT, RIGHT, CHARINDEX and SUBSTRING function
### Replicate, space, Patindex, Replace and Stuff string functions
### DateTime funcitons in SQL SERVER
### IsDate, Day, Month, Year and DateName DateTime functions in SQL SERVER
### DatePart, DateAdd and DateDiff funcitons in SQL SERVER
### Cast and Convert functions in SQL SERVER
### Mathematical funcitons in SQL SERVER
### Scalar user defined functions in SQL SERVER
### Infinite table valued funcitons in SQL SERVER
### Multi statement table valued functions in SQL SERVER
### Important concepts related to functions in SQL SERVER
### Temporary tables in SQL SERVER
### Indexes in SQL SERVER
### Clustered and nonclustered indexes in SQL SERVER
### Unique and Non Unique Indexes in SQL SERVER
### Advantages and disadvantages of indexes in SQL SERVER
### View in SQL SERVER
### Updatable views in SQL SERVER
### Indexed views in SQL SERVER
### View limitations in SQL SERVER
### DML triggers in SQL SERVER
### After update trigger
### Instead of insert trigger 
### Instead of update trigger in SQL SERVER
### Instead of delete trigger in SQL SERVER
### Derived tables and common table expressions in SQL SERVER
### CTE in SQL SERVER
### Updatable common table expressions in SQL SERVER
### Recursive CTE in SQL SERVER
### Database normalization
### Second normal form and third normal fom
### Pivot in SQL SERVER
### Error handling in SQL SERVER
### Transactions in SQL SERVER
### Transactions in SQL SERVER and ACID Tests
### Subqueries in SQL SERVER
### Correlated subquery in SQL SERVER
### Creating a large table with random data for performance testing
### What to choose for performance SubQuery or Joins
### Cursors in SQL SERVER
### Replacing cursors using joins in SQL SERVER
### List all tables in a SQL SERVER database using a query
### Writing a runnable SQL SERVER scripts
### After database table columns without dropping table
### Optional parameters in SQL SERVER stored procedures
### Merge in SQL SERVER
### SQL SERVER concurrent transactions
### SQL SERVER dirty read example
### SQL SERVER lost update
### Non repeatable read example in SQL SERVER
### Phantom reads example in SQL SERVER
### Snapshot isolation level in SQL SERVER
### Read committed snapshot isolation level in SQL SERVER
### Difference between snapshot isolation and read committed
### SQL Server deadlock example
### SQL SERVER Deadlock victim selection
### Logging deadlocks in SQL SERVER
### SQL SERVER deadlock analysis and prevention
### Capturing deadlocks in SQL SERVER
### SQL SERVER deadlock error handling
### Handling deadlocks in ADO NET
### Retry logic for deadlock exceptions
### How to find blocking queries in SQL SERVER
### SQL SERVER except operator
### Difference between EXCEPT and NOT in SQL SERVER
### Intsect operator in SQL SERVER
### Difference between UNION, INTERSECT, and EXCEPT in SQL SERVER
### Cross apply and outer apply in SQL SERVER
### DDL Triggers in SQL SERVER
### Server scoped DDL triggers
### SQL SERVER trigger execution order
### Audit table changes in SQL SERVER
### Logon Triggers in SQL SERVER
### Select into in SQL SERVER
### Difference between wehre and having in SQL SERVER
### Table valued parameteres in SQL SERVER
### Send datatable as parameter to stored procedure
### Grouping Sets in SQL SERVER
### Rollup in SQL SERVER
### Cube in SQL SERVER
### Difference between cube and rollup in SQL SERVER
### Grouping function in SQL SERVER
### grouping ID funciton in SQL SERVER
### Debugging SQL SERVER stored procedures
### Over clause in SQL SERVER
### Row number function in SQL SERVER
### Rank and Dense Rank in SQL SERVER
### Difference between rank dense rand and row number in SQL SERVER
### Calculate running total in SQL SERVER 
### NTLE function in SQL SERVER
### Lead and Lag functions in SQL SERVER 2012
### FIRST VALUE function in SQL SERVER
### Window funcitons in SQL SERVER
### Difference between row and range
### LAST VALUE function in SQL SERVER
### UNPIVOT in SQL SERVER
### Reverse PIVOT table in SQL SERVER
### Choose function in SQL SERVER
### IIF function in SQL SERVER
### TRY PARSE FUNCTION IN SQL SERVER 2012
### TRY CONVERT funciton in SQL SERVER 2012
### EOMONTH funciton in SQL SERVER 2012
### DATAEFROMPARTS fucntion in SQL SERVER
### Difference between DatTime and SmallDateTime in SQL SERVER
### DateTime2FromParts function in SQL SERVER
### Difference between DateTime and DateTime2 in SQL SERVER
### Offset fetch next in SQL SERVER 2012
### Identifying object dependencies in SQL SERVER
### Sys DM SQL referencing entities in SQL SERVER
### SP depends in SQL SERVER
### Sequence object in SQL SERVER 2012
### Difference between sequence and identity in SQL SERVER
