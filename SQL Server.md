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
**This is sample table tblEmployee:**  
> ![image](https://user-images.githubusercontent.com/58625165/210435701-1f4de7e0-2711-48e8-bbca-99f12347b5ad.png)
>###### The aggregate functions:
>```sql
>Select SUM(Salary) from tblEmployee
>Select MAX(Salary) from tblEmployee
>Select MIN(Salary) from tblEmployee
>
>-- If we use Aggregate function with other column in a select query then its mandatory to use GROUP BY clause otherwise SQL Server will throw an error.
>Select City, SUM(Salary) as TotalSalary FROM tblEmployee;   
>-- this will throw an error: "Column 'tblEmployee.City' is invalid in the select list because it is not   
>--contained in either an aggregate function or the GROUP BY clause."   
>--In short, if used an aggregate function in a query then all the columns should either have  
>--aggregate function applied on them or should be part of GROUP BY clause.   
>--So, the correct form is:  
> Select City, SUM(Salary) as TotalSalary FROM tblEmployee GROUP BY City;  
> Select COUNT(*) FROM tblEmployee;  
> Select COUNT(ID) FROM tblEmployee; --- This is better as compared to using * when look performance-wise.
>```
**Lets see an example for filtering the data:**
>```sql
>Select Gender, City, SUM(Salary) as TotalSalary, COUNT(ID) as [Total Employees]  
>from tblEmployee  
>Where Gender = 'Male'    
>Group By Gender, City;    
>```
>or you can also use like this using "HAVING" clause:
>```sql
>
>Select Gender, City, SUM(Salary) as TotalSalary, COUNT(ID) as [Total Employees]  
>from tblEmployee      
>Group By Gender, City  
>Having Gender = 'Male'    
>```
*The difference between above two queries is: the having clause can only be used after "Group By" clause.
*So with the "Where" query aggregations will be done only on the rows which have "Male" gender, where as in case of "Having" clause, aggregate functions will be applied all the records and then will be filtered by Gender (Male). 
>*Difference between WHERE and HAVING clauses:
> 1. WHERE clause can be used with - Select, Insert, and Update statements, where as HAVING clause can only be used with the Select statement.
> 2. WHERE filters rows before aggregation (GROUPING), where as, HAVING filters groups, after the aggregations are performed.
> 3. Aggregate functions cannot be used in the WHERE clause, unless it is in a sub query contained in a HAVING clause, whereas, aggregate functions can be used in  
> HAVING clause. See below example:
> ```sql
> Select Gender, City, SUM(Salary) as TotalSalary, COUNT(ID) as TotalEmployees  
> from tblEmployees  
> Group By Gender, City  
> Having SUM(Salary) > 5000; --- here we have used aggregate function (SUM) in HAVING clause, which we cannot do with WWHERE clause.
> ``` 

### Joins in sql server
*Join in SQL Server are used to retrieve data from 2 or more related tables. In general tables are related to each other using foreign key constraints.
*In SQL server, there are different types of JOINS:
 1. INNER JOIN
 2. OUTER JOIN
 3. CROSS JOIN

*Outer joins are again divided into:
 1. Left Join or Left Outer Join
 2. Right Join or Right Outer Join
 3. Full Join or Full Outer Join

> *We have two tables:  
> ![image](https://user-images.githubusercontent.com/58625165/210447384-7e10e754-4846-4585-b7ab-f6193bd11031.png)  
> ![image](https://user-images.githubusercontent.com/58625165/210447414-478bd45a-d27c-4da8-bbfe-23ffdcecc61f.png)   

*If we apply INNER JOIN on two tables then it only will select the columns that are NOT NULL. To include NULL columns as well we can use Outer JOIN.
* LEFT JOIN- returns all the matching rows + non matching rows from the left table.
* Let's see the outputs of these JOINS:
  1. LEFT JOIN/ LEFT OUTER JOIN:  
      ![image](https://user-images.githubusercontent.com/58625165/210450277-429d2fff-18ee-4113-a058-ab327f27d716.png)  
   
  2. RIGHT JOIN/ RIGHT OUTER JOIN:  
     ![image](https://user-images.githubusercontent.com/58625165/210450365-c79a4906-c3a2-4f73-aab1-cdb18b5d6fd3.png)  
     
  3. FULL JOIN/ FULL OUTER JOIN:  
     ![image](https://user-images.githubusercontent.com/58625165/210450463-d5feff6e-caab-42dc-8da3-4dbadf55671c.png)  
     _So, note that FULL JOIN will return matching records + non-matching records from the LEFT table + non-matching records from the RIGHT table_  
  
  4. CROSS JOIN:  
     *Cross join shouldn't have a ON clause.  
     ```sql  
     SELECT Name, Gender, Salary, DepartmentName    
     FROM tblEmployee  
     CROSS JOIN tblDepartment;  
     ```
   **Def:** Cross Join produces the Cartesian product of the 2 tables involved in the join.  
   For example, in the Employees table we have 10 rows and in the Department table we have  
   4 rows. So, a cross join between these 2 tables produce 40 rows.  

### Advanced or intelligent joins in sql server  
  1. LEFT JOIN excluding common area  
   ![image](https://user-images.githubusercontent.com/58625165/210453551-2e012882-e5f2-4a3d-8ab1-5ff5ba286e91.png)  

  2. RIGHT JOIN excluding common area  
   ![image](https://user-images.githubusercontent.com/58625165/210453597-faea5e65-0fa1-4aca-88b2-0b324867dcee.png)  
  
  3. LEFT and RIGHT JOIN excluding common area  
    ![image](https://user-images.githubusercontent.com/58625165/210453626-9caf7d3b-fa0d-488a-8cdf-a2eb76e778cb.png)  
**Note:** _To compare values with NULL in SQL Server we cannot use equal to operator (=) but instead we should use IS NULL_  

### Self join in SQL Server  
 **Def:** _Joining a table with itself is called **Self Join.**_    
>* Self JOIN is **not** a different type of JOIN.    
>* The demo tables  
>* It can be classified under any type of JOIN:    
>  1. INNER,  
>  2. OUTER (LEFT, RIGHT, FULL)    
>  3. CROSS Joins    
>  ```sql  
>  -- Left Outer Self Join  
>  SELECT E.Name AS Employee, M.Name AS Manager    
>  FROM tblEmployee E  
>  LEFT JOIN tblEmployee M  
>  ON E.ManagerId = M.EmployeeId  
>  
>  -- Inner Self Join  
>  SELECT E.Name AS Employee, M.Name AS Manager    
>  FROM tblEmployee E  
>  INNER JOIN tblEmployee M  
>  ON E.ManagerId = M.EmployeeId  
>  ```  
>  
>  -- Cross Self Join  
>  SELECT E.Name AS Employee, M.Name AS Manager    
>  FROM tblEmployee E  
>  CROSS JOIN tblEmployee M  
>  ```  
 
### Different ways to replace NULL in SQL Server  
> ```sql
> Select     E.name as Employee, ISNULL(M.Name, 'No Manager') as Manager  
> from       tblEmployee E    
> LEFT JOIN  tblEmployee M  
> ON         E.ManagerID = M.EmployeeID      
> ```
> It will output the following:  
> ![image](https://user-images.githubusercontent.com/58625165/210460861-dbb1ba45-3dd3-4ca2-b304-50f6dcf68ded.png)    
> * So, ISNULL('expression', 'replacement value') accepts two params: expression and replacement value  
> There's same function exists like ISNULL():  
> 
> ```sql
> Select     E.name as Employee, COALESCE(M.Name, 'No Manager') as Manager  
> from       tblEmployee E    
> LEFT JOIN  tblEmployee M  
> ON         E.ManagerID = M.EmployeeID      
> ```
> 
* The alternative way is to use THEN ELSE condition in query:
>```sql
>SELECT        E.Name as Employee,  
>              CASE  
>                   WHEN M.Name IS NULL THEN 'No Manager' ELSE M.Name  
>              END   
>              as Manager  
>FROM          tblEmployee E  
>LEFT JOIN     tblEmployee M  
>ON            E.ManagerID = M.EmployeeID;                      
>```

### COALESCE function in SQL Server
* **COALESCE() Function:-** Returns the first NON NULL value  
* The sample table:  
![image](https://user-images.githubusercontent.com/58625165/210463764-6b686ae7-a7b9-456c-92ac-8a80d57efdff.png)  
> ```sql
> SELECT  Id, COALESCE(FirstName, MiddleName,LastName) as Name  
> FROM    tblEmployee; 
> ```

### Union and union all in SQL Server
> * **Difference between UNION and UNION ALL**  
>  1. UNION removes duplicate rows, where as UNION ALL does not  
>  2. UNION has to perform distinct sort to remove duplicates, which makes it less faster than UNION ALL  
> Note: Estimated query execution plan - CTRL + L  
 
 >* **Sorting results of a UNION or UNION ALL**  
 > _ORDER BY clause should be used only on the last SELECT statement in the UNION query_  
 
 >* **Difference between UNION and JOIN**  
 > UNION combines the result-set of two or more select queries into a single result-set which includes  
 > all the rows from all the queries in the UNION, whereas JOINS, retrieve data from two or more tables  
 > based on logical relationships between the tables.  
 > 
 > In short, UNION combines rows from 2 or more tables, where JOINS combine columns from 2 or more tables.  

### Stored procedures in SQL Server  
> * **Def:** _A stored procedure is group of T-SQL (Transact SQL) statements If you have a situation,   
>where you write the same query over and over again, you can save that specific query as a stored  
>procedure and call it by it's name._   

> 1. Use CREATE PROCEDURE or CREATE PROC statment to create SP  
> **Note:** When naming user defined stored procedures, Microsoft recommends not to use **sp_** as a prefix.   
> All system stored procedures, are prefixed with **sp_**. This avoids any ambiguity between user defined and     
> system defined stored procedures and any conflicts, with some future system procedure.  

> * **To execute the stored procedure**  
>   1. spGetEmployees  
>   2. EXEC spGetEmployees  
>   3. Execute spGetEmployees  
> **Note:** You can also right click on the procedure name, in object explorer in SQL Server Management Studio and select EXECUTE STORED PROCEDURE.

>* The syntax of Store Procedure:  
> ```sql
>  CREATE PROCEDURE spProcedureName  
>  AS  
>  BEGIN  
>      Query Definition goes here...
>  END    
> ``` 

> ```sql
>  CREATE PROCEDURE spGetEmployees  
>  AS  
>  BEGIN  
>     Select Name, Gender from tblEmployee  
>  END    
> ```   
> And to execute it just write name of the SP or with EXEC or EXECUTE command:   
> ```sql   
> spGetEmployees  --or  
> EXEC spGetEmployees  --or  
> EXECUTE spGetEmployees  
> ```    

> * **Stored Procedure with Parameters:**  
> - Parameters and variables have an @ prefix in their name.   
> 
> * **To view the text, of the stored procedure**   
>   1. Use system stored procedure sp_helptext 'SPName'  
>                     OR                    
>   2. Right Click the SP in Object Explorer -> Scrip Procedure as -> Create To -> New Query Editor Window   

> * The SQL query can be defined as:  
> ```sql   
> Create Proc spGetEmployeesByGenderAndDepartment   
> @Gender nvarchar(20),  
> @DepartmentId int   
> as   
> Begin   
>      Select Name, Gender, DepartmentId from tblEmployee Where Gender = @Gender  
>      and DepartmentId = @DepartmentId  
> End        
> ```                     
> 
> To Execute:   
> ```sql  
>  EXECUTE spGetEmployeesByGenderAndDepartment 'Male',1     --- the order matters if don't using param names  
>  EXECUTE spGetEmployeesByGenderAndDepartment @DepartmentId=1, @Gender = 'Male'     --- the order doesn't matter if passing params with param names  
> ```   

>* To change the stored procedure, use ALTER PROCEDURE statment.  
>* To delete the SP, use DROP PROC 'SPName' or DROP PROCEDURE 'SPName'  
>* To encrypt the text of the SP, use WITH ENCRYPTION option. It is not possible to view the text of an encrypted SP.   
>```sql
>  Alter Proc spGetemployeesByGenderAndDepartment   
>  @Gender nvarchar(20),  
>  @DepartmentId int   
>```


### Stored procedures with output parameters
* **To create  an SP with output parameter, we use the keywords OUT or OUTPUT.**  
  ![image](https://user-images.githubusercontent.com/58625165/210635893-fd6590bc-6104-4a50-a2bc-b93e6f20b7aa.png)  
  
> ```sql 
> Create Procedure spGetEmployeeCountByGender  
> @Gender nvarchar(20),  
> @EmployeeCount int Output  -- notice this "Output" option   
> as  
> Begin  
>     Select  @EmployeeCount  = COUNT(Id)   
>     from    tblEmployee  
>     where   Gender = @Gender 
> End      
> ```  
> 
> * **To execute the stored procedure with output parameters**    
> ```sql  
>  Declare     @EmployeeTotal int  
>  Execute     spGetEmployeeCountByGender 'Male',  @EmployeeTotal Output  
>  Print       @EmployeeTotal  
> ```
> 
> ```sql   
>  Declare     @EmployeeTotal int  
>  Execute     spGetEmployeeCountByGender @EmployeeCount = @EmployeeTotal OUT, @Gender = 'Male'  
>  Print       @EmployeeTotal  
> ```   
> _If you don't specify the OUTPUT keyword, when executing the stored procedure, the   
> @EmployeeTotal variable will be NULL._  
> 
> * **Useful system stored procedures:**   
> 1. **sp_help procedure_name**  View the information about the stored procedure, like   
> parameter names, their datatypes etc. _sp_help_  can be used with any database object,  
> like tables, views, SP's, triggers etc. Alternatively, you can also press ALT+F1, when  
> the name of the object is highlighted.  
> ![image](https://user-images.githubusercontent.com/58625165/210639575-cb455459-dd05-4f4a-be22-455b5b7785e1.png)  
> 
> 2. **sp_helptext procedure_name**  View the text of the stored procedure  
> ![image](https://user-images.githubusercontent.com/58625165/210639842-cc3c861b-58e2-4464-ab8f-1bee7441b141.png)  
> 
> 3. **sp_depends procedure_name**  View the dependencies of the stored procedure.  
> This system SP is is very useful, especially if you want to check, if there are  
> any procedures that are referencing table that you are about to drop. sp_depends   
> can also be used with other database objects like tables etc.   
> ![image](https://user-images.githubusercontent.com/58625165/210639937-5a8c5f6e-3a77-4307-a888-e965a998e69c.png)  

 
### Stored prodedures output paramerters or return values
* Whenever you executes a stored procedure, it returns an integer status variable. Usually, zero indicates success, and non-zero indicates failure.   
![image](https://user-images.githubusercontent.com/58625165/210689501-35c3ceaf-e431-4598-8998-c63618c9f210.png)  
> ```sql
>  Create Procedure spGetTotalCountOfEmployees1  
>  @TotalCount int output  
>  as  
>  Begin  
>     Select   @TotalCount = COUNT(ID) from tblEmployee   
>  End       
> ```
> 
> ```sql  -- call the stored procedure  
> Declare  @TotalEmployees int  
> Execute  spGetTotalCountOfEmployees  @TotalEmployees Output  
> Select   @TotalEmployees
> ```
> * So, the above SP is with Output params and the below is using return values:   
> ```sql  
>  Create Procedure spGetTotalCountOfEmployees2     
>  as   
>  Begin    
>    return  (Select COUNT(ID) from Employees)     
>  End    
> ```   
>   
> ```sql  -- call the stored procedure    
> Declare  @TotalEmployees int  
> Execute  @TotalEmployees = spGetTotalCountOfEmployees2    
> Select   @TotalEmployees  
> ```  
> * See the following table:  
> ![image](https://user-images.githubusercontent.com/58625165/210691884-76eb32fb-a33e-4179-bc87-afe0f732f94b.png)  
> ```sql  
> Create Procedure spGetNameById1  
> @Id int,   
> as   
> Begin   
>   Select  @Name = Name  from  tblEmployee Where  Id= @Id  
> End     
> ```  
> ```sql  -- call the stored procedure    
> Declare  @EmployeeName nvarchar(20)  
> Execute  spGetNameById1 3, @EmployeeName Out  
> Print   'Name of the Employee = ' +  @EmployeeName  
> ```  
> 
> ```sql
>   Create Procedure spGetNameById2  
>   @Id int  
>   as   
>   Begin  
>       return  (Select Name from tblEmployee Where Id = @Id)  
>   End  
> ```
> ```sql  -- call the stored procedure  
> Declare  @EmployeeName nvarchar(20)  
> Execute  @EmployeeName = spGetNameById2 1  
> Print    'Name of the Employee = ' + @EmployeeName    
> ```    
> * _Executing spGetNameById2 returns an error stating 'Conversion failed when converting the nvarchar value 'Sam' to data type int.'_   
> * So, keep in mind we can only use "return values" only to return an integer value, it fails for non-integer values.   
> * Difference between Return Status Value and Output Parameters:  
> ![image](https://user-images.githubusercontent.com/58625165/210694455-0aae1624-51b1-4951-b3f6-e8418aba3c39.png)   

### Advantages of stored procedures
> * The following are advantages of Stored Procedures:  
>   1.  Execution plan retention and reusability  
>   2.  Reduces network traffic  
>   3.  Code reusability and better maintainability (in case of ad-hoc queries we have same queries in 1000 places, and we want to change the logic of those queries, as they are designed to used for the same thing, we need to make changes in 1000 place which is not good maintainability)    
>   4.  Better Security  
>   5.  Avoids SQL Injection attack  

> * When we issue a query to SQL Server, 3 things happen:  
>   1. It checks the syntax of the query,  
>   2. It compiles that query,  
>   3. It generates an execution plan   
>   - The execution plan means for the query to retrieve the data what is the best possible way available.  
>   - When next time we issue the query, since the execution plan is already generated it will be cached by SQL Server so Next time when you run the query, it's gonna reuse that execution plan. The same thing happens with SP.  
>   - When executing simple queries more than once, the SQL Server will use already generated execution plan, but if minor change like change in parameter or a space will generate new execution plan when we re-issue query next time.    
>   The simple query also called as ad-hoc SQL Query :)      

### Built in string functions in SQL Server  
> * String Functions:  
> ![image](https://user-images.githubusercontent.com/58625165/210697203-3f80e957-e69b-47e3-b3f7-737110aaeeff.png)   
> ```sql
> Select ASCII('ABC')
> ```  
> The above query will return the output:   
> ![image](https://user-images.githubusercontent.com/58625165/210697476-3086bb51-eced-456a-ace7-987cb5ca1f8a.png)  
> * Let's print A to Z by looping and using CHAR():   
> ```sql  
>  Declare @Start int  
>  Set     @Start = 65  
>  While(@Start <= 90)  
>  Begin   
>     Print  CHAR(@Start)  
>     Set    @Start = @Start + 1  
>  End   
> ```
> * We can use LTRIM and RTRIM to remove white spaces on left and right sides respectively. If we want to remove the spaces from both the sides then we can combine/concat them like:  
> ```sql 
> Select LTRIM(FirstName) as FirstName, MiddleName, LastName,  
> RTRIM(LTRIM(FirstName)) + ' ' + MiddleName + ' ' + LastName as FullName  
> from tblEmployee   
> ```
> * The LEN() counts all white spaces of a word/string which are in the beggining or in the middle of it, but it excludes the spaces at the end of the word/string.  
> 

### LEFT, RIGHT, CHARINDEX and SUBSTRING function  
* String functions:   
![image](https://user-images.githubusercontent.com/58625165/210699759-a1f50d43-d7a2-4af5-92a5-b99e9aad5411.png)   
>  ```sql
>   Select SUBSTRING(Email, CHARINDEX('@', Email) + 1,  
>   LEN(Email) - CHARINDEX('@', Email)) as EmailDomain,  
>   COUNT(Email)  as Total  
>   from tblEmployee    
>   Group By SUBSTRING(Email, CHARINDEX('@', Email) + 1,  
>   LEN(Email) - CHARINDEX('@', Email))  
>  ```  
>  The output will be:  
>  ![image](https://user-images.githubusercontent.com/58625165/210825194-8a26413d-4df2-4084-9bf2-b73313130b27.png)  


### Replicate, space, Patindex, Replace and Stuff string functions
> * **Syntax:**   
>   REPLICATE(String_To_Be_Replicated, Number_Of_Times_To_Replicate)   
>   _Repeats the given string, for the specified number of times._   
>   ![image](https://user-images.githubusercontent.com/58625165/210826399-6f4f1a31-52e0-4011-b074-eeda9674ae9d.png)   
>   ```sql
>     Select   FirstName, LastName,   
>              SUBSTRING(Email, 1, 2) + REPLICATE('*', 5)  +   
>              SUBSTRING(Email, CHARINDEX('@', Email),  LEN(Email)  - CHARINDEX('@', Email) + 1)  as Email   
>     from     tblEmployee            
>   ```  

>   SPACE(Number_Of_Spaces)     
>   _Returns number of spaces, specified by the Number_Of_Spaces argument._     
>   ![image](https://user-images.githubusercontent.com/58625165/210827187-a8261132-32a6-48e2-8577-21c0f4aa79e0.png)  
>   ```sql
>     Select   FirstName, SPACE(5) + LastName as FullName       
>     from     tblEmployee              
>   ```  

>   PATINDEX('%Pattern%', Expression)       
>   _Returns the starting position of the first occurences of a pattern in a specified expression. It takes two arguments, the pattern to be searched and the expression. PATINDEX() is similar to CHARINDEX(). With CHARINDEX() we cannot use wildcards, where as PATINDEX() provides this capability. If the specified pattern is not found, PATINDEX() returns ZERO._ 
>       
>   ![image](https://user-images.githubusercontent.com/58625165/210828294-b8501d81-4a66-4b0d-9d2b-49db4f1a91c3.png)    
>   ```sql
>     Select   Email, PATINDEX('%@aaa.com', Email) as FirstOccurence          
>     from     tblEmployee   
>     Where    PATINDEX('%@aaa.com', Email) > 0                
>   ```  

>   REPLACE(String_Expression_Pattern, Replacement_Value)         
>   _Replaces all occurences of a specified string value with another string value._   
>       
>   ![image](https://user-images.githubusercontent.com/58625165/210829497-1a556762-80dc-4ac2-bf9a-ffecf2224263.png)       
>   ```sql
>     Select   Email, REPLACE (Email, '.com', '.net') as ConvertedEmail            
>     from     tblEmployee                   
>   ```    

>   STUFF(Original_Expression, Start, Length, Replacement_expression)             
>   _STUFF() function inserts Replacement_expression, at the start position specified, along with removing the characters specified using Length parameter._   
>       
>   ![image](https://user-images.githubusercontent.com/58625165/210830420-c8ff231e-849d-45dd-b306-f6af791a93f3.png)          
>   ```sql
>     Select   FirstName, LastName, Email,   
>              STUFF(Email, 2, 3, '*****')  as StuffedEmail               
>     from     tblEmployee                   
>   ```    


### DateTime functions in SQL Server    

![image](https://user-images.githubusercontent.com/58625165/210834251-3e71c2cc-c325-4673-91e7-441151e5b4c8.png)   

> * UTC stands for Coordinated Universal Time, based on which, the world regulates clocks and time. There are slight differences between GMT and UTC, but for most common purposes, UTC is synonymous with GMT.   
> ![image](https://user-images.githubusercontent.com/58625165/210839078-a44a2772-17fa-465b-b435-251946feb5a9.png)   
> 


### IsDate, Day, Month, Year and DateName DateTime functions in SQL Server  
* **ISDATA()** - _Checks if the given value, is a valid date, time, or datetime. Returns 1 for success, 0 for failure._  
> * **Examples:**  
> ```sql
> Select   ISDATE('PRAGIM')  -- returns 0  
> Select   ISDATE(Getdate())  -- retuns 1  
> Select   ISDATE('2012-08-31 21:02:04.167')  -- returns 1  
> Select   ISDATE('2012-09-01 11:34:21.1918447')  -- returns 0  
> **Note:** _For datetime2 values, IsDate returns ZERO for valid dates._  
> ```

> * **Day, Month, Year:**
> Day() - Returns the 'Day number of the month' of the given date  
> Month() - Returns the 'Month number of the year' of the given date  
> Year() - Returns the 'Year number' of the given date     
> _Examples:_  
> ```sql
>  Select DAY(GETDATE())      -- Returns the current date day number of the month  
>  Select DAY('01/31/2012')   -- Returns 31 
>   
>  Select Month(GETDATE())    -- Returns the current date, Month number of the year  
>  Select Month('01/31/2012') -- Returns 1  
>  
> ```  
> **DateName(DatePart, Date):** - Returns a string, that represents a part of the given date. This functions takes 2 parameters. The first parameter DatePart specifies, the part of the date, we want. The second parameter, is the actual date, from which we want the part of the date.  
> ``sql
> Select DATENAME(Day, '2012-09-30 12:43:46.837')     -- Returns 30     
> Select DATENAME(WEEKDAY, '2012-09-30 12:43:46.837') -- Returns Sunday  
> Select DATENAME(MONTH, '2012-09-30 12:43:46.837')   -- Returns Sepetember   
> ```  
> The other datepart and its abbreviations are listed below:  
> ![image](https://user-images.githubusercontent.com/58625165/210854924-5e8cea91-12e9-49d7-818d-226c55052b04.png)  
> 


### DatePart, DateAdd and DateDiff funcitons in SQL Server
> * **DatePart(DatePart, Date):** - Retuns an integer representing the specified DatePart. This function is similar to DateName(). DateName() returns nvarchar, where as DatePart() returns an integer.  
> ```sql  
>   Select   DATEPART(WEEKDAY, '2012-08-30 19:45:31.793')   -- Returns 5  
>   Select   DATENAME(WEEKDAY, '2012-08-30 19:45:31.793')   -- Returns Thursday   
> ``` 
> 
> * **DATEADD(DatePart, NumberToAdd, date):**  - Returns the DateTime, after adding specified NumberToAdd, to the datepart specified of the given date.  
> ```sql  
> Select    DATEADD(DAY, 20,  '2012-08-30 19:45:31.793')  -- Returns 2012-09-19 19:45:31.793  
> Select    DATEADD(DAY, -20,  '2012-08-30 19:45:31.793')  -- Returns 2012-08-10 19:45:31.793      
> ```  
>   
> * **DATEDIFF(DatePart, StartDate, EndDate):**  - Returns the count of the specified datepart boundaries crossed between the specified startdate and enddate.  
> ```sql  
> Select DATEDIFF(MONTH, '11/30/2005', '01/31/2006')    -- Returns 2   
> Select DATEDIFF(DAY, '11/30/2005', '01/31/2006')    -- Returns 62   
> ```  
> **Calculating the age:** -  
> The DATEDIFF() function fails to calculate the actual diffence between some dates:  
> ```sql  
> Select DATEDIFF('11/30/2005','01/31/2006') -- The actual difference is 31 days but it will return 62 (see below):      
> ![image](https://user-images.githubusercontent.com/58625165/210860054-c776134b-42f9-40f7-a1c8-d8ee1f488034.png)     
> ```  
> The other example is:  
> ```sql  
> Select DATEDIFF('11/30/2005','01/31/2006')  -- returns 1,but the actual difference is 0 years and 2 months   
> ![image](https://user-images.githubusercontent.com/58625165/210860418-5460469d-4ef4-4cc7-8a8c-65606fcef18c.png)       
> ```   
> So, to keep in mind above miscalculations of DATEDIFF(), we have to add a CASE. See below example, (Note that we have used function here):      
> ```sql  
>    Create function fnComputeAge(@DOB  DateTime)  
>    retuns nvarchar(50)   
>    as   
>    Begin   
>      
>    DECLARE @tempdate datetime, @years int, @months int, @days int       
>      
>    SELECT @tempdate = @DOB  
>      
>    SELECT @years = DATEDIFF( YEAR, @tempdate, GETDATE() )  -  
>                    CASE   
>                        WHEN  (MONTH(@DOB) > MONTH(GETDATE())) OR  
>                        (MONTH(@DOB) = MONTH(GETDATE())  AND DAY(@DOB) > DAY(GETDATE())  
>                        THEN 1 ELSE 0   
>                    END   
>    SELECT @tempdate =  DATEADD(YEAR, @years, @tempdate)   
>      
>    SELECT @months = DATEDIFF(MONTH, @tempdate, GETDATE())  -  
>                     CASE   
>                         WHEN  DAY(@DOB)  > DAY(GETDATE())  
>                         THEN 1 ELSE 0  
>                     END   
>    SELECT @tempdate = DATEADD(YEAR, @years, @tempdate)   
>       
>    SELECT @months = DATEDIFF(MONTH, @tempdate, GETDATE())  -   
>                     CASE   
>                         WHEN DAY(@DOB)  > DAY(GETDATE())  
>                         THEN 1 ELSE 0 
>                     END   
>    SELECT @tempdate = DATEADD(MONTH, @months, @tempdate)   
>       
>    SELECT @days = DATEDIFF(DAY, @tempdate, GETDATE())  
>    
>       DECLARE @Age nvarchar(50)  
>       Set     @Age = Cast(@years as nvarchar(4)) + ' Years' + Cast(@months as nvarchar(2)) + ' Months' + Cast(@days as nvarchar(2) + ' Days Old'   
>       
>       return  @Age      
>    END                                                                  
> ```  
> To call the function we can do it as follows:   
> ```sql  
> Select dbo.fnComputAge('11/30/2005')     
> ```  
> Or, we can use the function in a query like follows:   
> ```sql  
>  Select Id, Name, DateOfBirth, dbo.fnComputeAge(DateOfBirth) as Age from tblEmployees    -- note that we have passed name of column (DateOfBirth) as param  
> ```


### Cast and Convert functions in SQL Server
>* **To convert one data type to another, CAST and CONVERT functions can be used.**  
>* _Syntax:_    
>  ```sql  
>   CAST(expression AS data_type[(length)])   
>   CONVERT( data_type [(length)], expression [, style] )   
>   So, above syntax is from MSDN documentation, the square brackets means the argument is _optional._   
>  ``` 
>  So, for example we have two tables given below, we have to convert 1st into 2nd with additional **ConvertDOB** column:  
>  ```sql  
>  Select Id, Name, DateOfBirth, CAST(DateOfBirth as nvarchar)  as ConvertedDOB from tblEmployees   -- either CAST()        
>  Select Id, Name, DateOfBirth, CONVERT(nvarchar, DateOfBirth)  as ConvertedDOB from tblEmployees  -- or we can use CONVERT() as alternative  
>  ```   
>  So, we can use following query to get desired output table:   
>  ```sql  
>   Select Id, Name, DateOfBirth,    
>   Convert(nvarchar, DateOfBirth, 103)  as ConvertedDOB   -- note the 3rd argument is 103(style), which can be well understood by following table   
>   from tblEmployees     
>  ```  
>  Refer the following **style**  table:   
>  ![image](https://user-images.githubusercontent.com/58625165/210868226-e2840e88-3217-4ff9-b7c1-78c9ffc60e80.png)   
>  And the final output of the above query will be as follows:   
>  ![image](https://user-images.githubusercontent.com/58625165/210868337-d0983a5b-b533-481d-8e87-4c93b67ffd44.png)   
>  So, for converting a date into other "date format", we can only use CONVERT() but we cannot use the CAST() for it :).   
>  Note: Don't memorize the styles as MSDN has around 20 styles but few are listed in above picture. (If you will memorize the styles, then what's the use of Google then? :D ).   
>  Practical Example:   
>  We need to convert the following left table into the right table:   
>  ![image](https://user-images.githubusercontent.com/58625165/210877295-f1ea797d-2ab9-47e3-9bc7-0fdd2b8347b4.png)   
>  ```sql  
>  Select     CAST(RegisteredDate as DATE) as RegistrationDate, COUNT(ID) as TotalRegistrations   
>  from       tblRegistrations   
>  Group By   CAST(RegisteredDate as DATE)     
>  ```
>  What should not be done? See the following query:    
>  Select     RegisteredDate as RegistrationDate, COUNT(ID) as TotalRegistrations   
>  from       tblRegistrations   
>  Group By   RegisteredDate        
>  ```    
>   The above query will have output like this:    
>   ![image](https://user-images.githubusercontent.com/58625165/210877911-0adb7b1c-7bff-4af9-9d1e-7e79a2f46d3f.png)   
>   **Differences between CAST() and CONVERT() :**  
>       1. CAST is based on ANSI standard and Convert is specific to SQL Server. So, if portability is a concern and if you want to use the script with other database applications, use CAST().   
>       2. CONVERT provides more flexibility than CAST. For example, it's possible to control how you want DateTime datatypes to be converted using styles with convert function.   
>       **Note:**  _The general guideline is to use CAST(), unless you want to take advantage of style functionality in CONVERT()._   
>        

    
### Mathematical functions in SQL Server
> * ABS( numeric_expression ) - 
> _ABS stands for absolute and returns, the absolute (positive) number._   
> ```sql  
>  Select ABS(-101.5)   -- Returns 101.5, without the - sign  
      
> ```
> * CEILING( numeric_expression ) and FLOOR( numeric_expression ) -   
> _CEILING and FLOOR functions accept a numeric expression as a single parameter. CEILING() returns the smallest and integer value greater than or equal to the parameter, whereas FLOOR() returns the largest integer less than or equal to parameter._   
> ```sql  
>   Select CEILING(15.2)  -- Returns 16  
>   Select CEILING(-15.2) -- Returns 15  
>      
>   Select FLOOR(15.2)    -- Returns 15    
>   Select FLOOR(-15.2)   -- Returns -16
> ```   

> * POWER(expression, power) -  
> _Returns the power value of the specified expression to the specified power._   
>      
> ```sql  
>   Select POWER(2, 3)    -- Returns 8  
> ```  
   
> * SQUARE( Number ) -    
> _Returns the square of the given number._         
> ```sql  
> Select SQUARE(9)        -- Returns 81        
> ```

> * SQRT( Number ) -   
> _Returns the square root of the given number._    
> ```sql  
> Select SQRT(81)        -- Returns 9        
> ```  

> * RAND([Seed_Value]) -   
> _Returns a random float number between 0 and 1. Rand() function takes an optional seed parameter. When seed value is supplied the RAND() function always returns the same value of the same seed._    
> ```sql  
> Select RAND(1)        -- Always returns the same value           
> ```
> * Generate a random number between 1 and 100:    
> ```sql  
>   Select  FLOOR(RAND() * 100 )  
> ```  
> * Print 10 random numbers between 1 and 100:  
> ```sql  
>    Declare   @Counter  INT  
>    Set       @Counter = 1   
>    While(@Counter <= 10)  
>    Begin   
>        Print  FLOOR(RAND() * 100 )  
>        Set    @Counter = @Counter + 1  
>    End      
> ```  

> * ROUND() -   
> _Rounds the given numeric expression based on the given length. This function takes 3 parameters._   
>  1. **Numeric_Expression**  is the number that we want to round.  
>  2. **Length**  parameter, specifies the number of digits that we want to round to. If the length is a positive number, then the rounding is applied for the decimal part, where as if the length is negative, then the rounding is applied to the number before the decimal.   
>  3. **The optional function parameter**, is used to indicate or truncation operations. 0 indicates rounding, non-zero indicates trucation. Default, if not specified is 0.   
>  ```sql   
>  -- Round to 2 places after (to the right) the decimal point  
>    Select ROUND(850.556, 2)      -- Returns 850.560   
>       
>  -- Truncate anything after 2 places, after (to the right) the decimal point  
>     Select ROUND(850.556, 2, 1)  -- Returns 850.550   
>        
>  -- Round to 1 place after (to the right) the decimal point   
>     Select ROUND(850.556, 1)  -- Returns 850.600     
>     
>  -- Truncate anything after 1 place, after (to the right) the decimal point  
>     Select ROUND(850.556, 1, 1)  -- Returns 850.500           
>         
>  -- Round the last 2 places before (to the left) the decimal point  
>     Select ROUND(850.556, -2)  -- Returns 900.000      
>         
>  -- Round the last 1 place before (to the left) the decimal point  
>     Select ROUND(850.556, -1)  -- Returns 850.000      
>  ```
>  

### Scalar user defined functions in SQL Server  
>* **In SQL there are 3 types of User Defined Functions:**  
>  1. Scalar functions  
>  2. Inline table-valued functions   
>  3. Multi-statement table-valued functions  

> **Scalar functions** may or may not have parameters, but always return a single(scalar) value. The returned value can be of any data type, except **text, ntext, image, cursor, and timestamp**.   
> ```sql  
>    CREATE FUNCTION Function_Name(@Parameter1 DataType, @Parameter2 DataType, ..., @ParameterN DataType)   
>    RETURNS  Return_Datatype   
>    AS   
>    BEGIN  
>        --- Function Body  
>            Return  Return_Datatype  
>    END          
> ```  
> An example of function:   
> ```sql  
>   CREATE FUNCTION CalculateAge(@DOB Date)   
>   RETURNS INT  
>   AS  
>   BEGIN   
>      
>   DECLARE  @DOB DATE   
>   DECLARE  @Age INT   
>   SET      @DOB = '11/08/2011'   
>      
>   SET      @Age = DATEDIFF(YEAR, @DOB, GETDATE())  -   
>                CASE   
>                   WHEN  (MONTH(@DOB)  > MONTH(GETDATE()) )  OR   
>                         (MONTH(@DOB)  = MONTH(GETDATE())  AND DAY(@DOB) > DAY(GETDATE()) )   
>                   THEN  1   
>                   ELSE  0  
>                END   
>                   
>  SELECT  @Age   
>  END  
>                             
> ```
> To invoke the above function:  
>  ```sql  
>    Select CalculateAge('10/08/1982')  -- this won't work and will throw an error (see below)
>  ```      
>  ![image](https://user-images.githubusercontent.com/58625165/210890047-a9130644-7a80-4d8d-9425-18378d1af313.png)  
>  To invoke user-defined functions we call it in two parts (the first part is dbo) : 
>   ```sql   
>      Select dbo.CalculateAge('10/08/1982')   
>   ```
> The created functions stored in database folder (see below):   
> ![image](https://user-images.githubusercontent.com/58625165/210888885-218cbf16-bae5-4319-bafa-a8413e654b17.png)    
> * A stored procedure also can accept **DateOfBirth** and **return Age**, but you cannot use stored procedures in a select or where clause. This is just one difference between a function and a stored procedure. There are several other differences, which we will talk about in a later section.  
> * To alter a function we use **ALTER FUNCTION FunctionName** statement and to delete it, we use **DROP FUNCTION FunctionName**.   
>  


### Infinite table-valued functions in SQL Server    
> * **SCALAR function**   
> _Returns a Scalar value_   
> * **INLINE TABLE VALUED function**     
> _Returns a table_   
> ![image](https://user-images.githubusercontent.com/58625165/210892245-6450b450-8be9-4149-9bb0-806a9983cfaa.png)   
>  ```sql  
>    CREATE FUNCTION fn_EmployeesByGender(@Gender nvarchar(10))   
>    RETURNS TABLE   
>    AS   
>    RETURN   (Select   Id, Name, DateOfBirth, Gender, DepartmentId   
>              from     tblEmployees   
>              Where    Gender = @Gender)   
>  ```    
>  1.  We specify TABLE as the return type, instead of any scalar data type  
>  2.  The function body is not enclosed between BEGIN and END block.   
>  3.  The structure of the table that gets returned, is determined by the SELECT statement with in the function.  
> Now, to call/invoke this function we use the following command:   
> ```sql  
>  Select * from fn_EmployeesByGender('Male')    
> ```  
> * Where can we  use inline Table Valued functions:       
>     1. Inline Table Valued functions can be used to achieve the functionality of parameterized views. We will talk about views, in a letter section.   
>     2. The table returned by the table valued function, can also be used in joins with other tables.   
> * Using an inline function with Join:   
> ```sql   
>     SELECT    Name,  Gender,  DepartmentName   
>     FROM      fn_EmployeesByGender('Male')    E  
>     JOIN      tblDepartment  D   
>     ON  D.Id = E.DepartmentId     
> ```       
> _Why it's possible to use inline function with join?  Because the inline functions return a table and on a table we can perform a join :D._  
> 

### Multi statement table valued functions in SQL Server   
> * "Multi statement table valued functions" are very similar to Inline Table valued functions, with a few differences.   
> ![image](https://user-images.githubusercontent.com/58625165/211051545-3a3d0a5f-96b6-45f4-96bd-50db6e1e9ece.png)   
> ```sql  
>   -- Inline Table Valued Function  
>      CREATE    Function fn_ILTVF_GetEmployees()  
>      Returns   Table   
>      as   
>      Return    (Select Id, Name, Cast(DateOfBirth as Date) as DOB From tblEmployees)      
>        
>   -- Multi-statement Table Valued Function   
>      CREATE    Function fn_MSTVF_GetEmployees()   
>      Returns   @Table Table (Id int, Name nvarchar(20), DOB Date)  
>      as    
>      Begin     
>           Insert into @Table  
>           Select Id, Name, Cast(DateOfBirth as Date)  From tblEmployees  
>              
>           Return  
>      End  
> ```        
> So, the main difference between Inline and multi statement- table valued function is:   
>   1.  In an Inline Table Valued function, the RETURNS clause cannot contain the structure of the table, the function returns. Where as, with the multi-statement table valued function, we specify the structure of the table that gets returned.      
>   2.  Inline Tabe Valued function cannot have BEGIN and END block, where as the multi-statement table valued function can have.   
>   3.  Inline Tabe Valued functions are better for performance, than multi-statement table valued functions. If the given task, can be acheieved using an inline table valued function, always prefer to use them, over multi-statement table valued functions.  
>   4.  It's possible to update the underlying table, using an inline valued function, but not possible using multi-statement table valued function.      
>  * Reason for improved performance for an inline table valued function:   
>  Internally, SQL Server treats an inline table valued function much like it would a view and treats a multi-statement table valued function similar to how it would a stored procedure.   
>  ```sql  
>   -- issue an update query against ILTVF:   
>      Update fn_ILTVF_GetEmployees() set Name = 'Sam'  Where Id = 1;   -- this will udpate the record as expected   
>   -- now issue an update query against MSTVF:   
>      Update fn_MSTVF_GetEmployees() set Name = 'Sam 1'  Where Id = 1; -- it will throw an error     
>  ```  
>  ![image](https://user-images.githubusercontent.com/58625165/211062335-e29daba8-0010-4f89-ae3f-e20c3953e106.png)   
>       


### Important concepts related to functions in SQL Server   
> * **Deterministic functions**  
>   DFs always return the same function at any time they are called with a specific set of input values and give the same state of the database.  
>   **Examples:**  Square(), Power(), Sum(), AVG(), and Count()    
>      
>   **Note:**  _All aggregate functions are deterministic functions._   

> * **Nondeterministic functions:**   
>   It may return different results each time they are called with a specific set of input values even if the database state that they access remain the same.  
>   **Examples:**  GetDate() and CURRENT_TIMESTATMP   
>   **Rand() Function**  is a Non-deterministic function, but if you provide the seed value, the function becomes deterministic, as the same value gets returned for the same seed value.  

> * **Encrypting a function definition using WITH ENCRYPTION OPTION:**    
> We have learnt how to encrypt Stored procedure text using WITH ENCRYPTION OPTION in former section. Along the same lines, you can also encrypt a function text. Once, encrypted, you cannot view the text of the function, using **sp_helptext**  system stored procedure. If you try to, you will get a message stating '_The text for object is encrypted._'  There are ways to decrypt, which is beyond the scope of this section.  
> 
>   USE **WITH ENCRYPTION**    
>   
>   ```sql  
>    Alter function fn_GetNameById(@Id int)   
>    Returns nvarchar(30)  
>    WITH ENCRYPTION       --- this is the flag   
>    as  
>    Begin   
>        Return (Select Name from tblEmployees Where Id = @Id )  
>    End        
>   ```        
>   To remove encryption issue above query by removing WITH ENCRYPTION statement/flag and then you can see the function by **sp_helptext**   
>   
      
>   **Creating a function WITH SCHEMABINDING option:**     
>     Schemabinding, specifies that the function is bound to the database that it references. When SCHEMABINDING is specified, the base objects cannot be modified in any way that would affect the function definition. The function definition itself must first be modified or dropped to remove dependencies on the object that is to be modified.   
>        
>   USE **WITH SCHEMABINDING**
>   ```sql  
>    Alter function fn_GetNameById(@Id int)   
>    Returns nvarchar(30)  
>    WITH SCHEMABINDING       --- this is the flag   
>    as  
>    Begin   
>        Return (Select Name from dbo.tblEmployees Where Id = @Id )  --note, here we have to use two part name (dbo.tblEmployee)       
>    End        
>   ```   
>   The SCHEMABINDING specifies that the function fn_GetNameById() is bound with the table tblEmployees in **dbo** schema   
>   After executing schemabinding query, if you try to drop the tblEmployees table it will throw an error:   
>   ![image](https://user-images.githubusercontent.com/58625165/211068884-628d3b30-aba2-4ba2-9faf-4fc3611b90f7.png)   
>   

 
### Temporary tables in SQL Server
>* **What are temporary tables?**   
> _Temporary tables, are very similar to the permanent tables. Permanenet tables get created in the database you specify, and remain in the database permanently, until you delete(drop) them. On the other hand, temporary tables get created in the TempDB and are automatically deleted, when they are no longer used._  
> **Different Types of Temporary Tables:**  
>  1. Local Temporary Tables  
>  2. Global Temporary Tables  

> * **Local Temporary Tables**   
>  ```sql  
>       -- Create Local Temporary Table (use # for creating temporary table)   
>          CREATE Table #PersonDetails(Id int, Name nvarchar(20))   
>       -- Insert Data into the Temporary Table  
>          Insert into   #PersonDetails Values (1, 'Mike')  
>          Insert into   #PersonDetails Values (2, 'John')    
>          Insert into   #PersonDetails Values (3, 'Todd')    
>       -- Select data from the Temporary Table:   
>          Select * from #PersonDetails      
>  ``` 

> * Check if the local temporary table is created:  
> Temporary tables are created in the TEMPDB. Query the sysobjects system table in TEMPDB. The name of the table, is suffixed with lot of underscores and a random number. For this reason you have to use the LIKE operator in the query.  
> ```sql  
>   Select   name from tempdb..sysobjects  
>   Where    name LIKE '#PersonDetails%'   
> ```  
> A local temporary table is available, only for the connection that has created the table.   
> A local temporary table is automatically dropped, when the connection that has created it, is closed.  
> If the user wants to explicitly drop the temporary table, he can do so using:   
> ```sql   
>    DROP TABLE #Persondetails    
> ``` 
> With GUI, we can check temporary table through database folders(see below image):      
> ![image](https://user-images.githubusercontent.com/58625165/211072044-dc983207-fd0c-46d6-9f3c-b96ff120a706.png)   

>  **If the temporary table, is created inside the stored procedure, it get's dropped automatically upon the completion of stored procedure execution.**  
>  ```sql  
>     Create Procedure spCreateLocalTempTable   
>     as   
>     Begin   
>     Create Table   #PersonDetails(Id int, Name nvarchar(20))   
>       
>     Insert into #PersonDetails  Values(1,  'Mike')   
>     Insert into #PersonDetails  Values(2,  'John')   
>     Insert into #PersonDetails  Values(3,  'Todd')   
>        
>     Select * from #PersonDetails   
>     End     
>  ```   
>  -It is also possible for different connections, to create a local temporary table with the same name.  
>  -For example, User1 and User2, both can create a local temporary table with the same name #PersonDetails   

> * **Global Temporary Tables**   
> _To create a Global Temporary Table, prefix the name of the table with 2 pound(##) symbols._   
> * **Global temporary tables are visible to all the connections** of the sql server, and are only destroyed when the last connection referencing the table is closed.   
> ```sql  
>    Create Table ##EmployeeDetails(Id int, Name nvarchar(20));           
> ```   
> **Multiple users, across multiple connections** can have local temporary tables with the same name, but, a global temporary table name has to be unique, and if you inspect to the name of the global temp table, in the object explorer, there will be no random numbers suffixed at the end of the table name.   

> * **Difference Between Local and Global Temporary Tables:**   
>   1. **Local Temp Tables** are prefixed with single pound(#) symbol, where as global temp tables are prefixed with 2 pound(##) symbols.  
>   2. **SQL Server appends some random numbers** at the end of the local temp table name, where this is not done for global temp table names.  
>   3. **Local temporary tables are only visible** to that session of the SQL Server which has created it, where as Global tables are visible to all the SQL server sessions.  
>   4. **Local temporary tables are automatically dropped**, when the session that created the temporary table is closed, where as Global temporary tables are destroyed when the last connection that is referencing the global temp table is closed.   
>       
 

### Indexes in SQL Server   
* **Why Indexes?**  
- _Indexes are used by queries to find data from tables quickly. Indexes are created on tables and views. Index on a table or a view, is very similar to an index that we find in a book._  
- If you don't have an index, and I ask you to locate a specific chapter in the book, you will have to look at every page starting from the first page of the book.  
- On, the other hand, if you have the index, you lookup the page number of the chapter in the index, and then directly go to that page number to locate the chapter.  
- Obviously, the book index is helping to drastically reduce the time it takes to find the chapter.  
- In a similar way, Table and View indexes, can help the query to find data quickly.  
- In fact, the existence of the right indexes, can drastically improve the performance of the query. If there is no index to help the query, then the query engine, will check every row in the table from beginning to the end. This is called a Table Scan. Table Scan is bad for performance.   

> * Let's see why we need index in action. The following is a problem:    
> ![image](https://user-images.githubusercontent.com/58625165/211077934-ff69bcde-9028-443d-8318-cf32cc42423a.png)  
> At the moment, the Employees table, does not have an index on SALARY column.  
> ```sql  
>   Select * from tblEmployee   
>   Where  Salary > 5000 and Salary < 7000   
> ```   
> _To find all the employees, who has salary between 5000 and 7000, the query engine has to check each and every row in the table, resulting in a table scan, which can adversely affect the performance, especially if the table is large. Since there is no index to help the query, the query engine performs an entire table scan._   

> * To create an index:   
> ```sql   
>    CREATE INDEX  IX_tblEmployee_Salary   
>    ON     tblEmployee  (SALARY ASC)      
> ```   
> **The index stores salary of each employee, in the ascending order as shown below. The actual index may look slightly different.**   
> ![image](https://user-images.githubusercontent.com/58625165/211078748-e3880896-eafb-472c-8ea7-98e571292acd.png)   
> (_The main table(on the left side) and the index(on the right side)_)   
> - Now, when the SQL Server has to execute the same query, it has an index on the salary column to help this query. Salaries between the range of 5000 and 7000 are usually present at the bottom, since the salaries are arranged in an ascending order. SQL server picks up the row addresses from the index and directly fetch the records from the table, rather than scanning each row in the table. This is called as Index Seek.  
> To see the created index, we use the **sp_Helpindex**:   
> ```sql  
>  sp_HelpIndex tblEmployee  -- note, here we have to use the name of the table, "tblEmployee"         
> ```   
> To delete/drop the index:    
> ```sql   
>    drop index tblEmployee.IX_tblEmployee_Salary   -- note, we have to provide "table name.indexName"       
> ```   
> 


### Clustered and nonclustered indexes in SQL Server   
> * The types of Index:       
>  1. Clustered   
>  2. Nonclustered     
>  3. Unique    
>  4. Filtered    
>  5. XML    
>  6. Full text    
>  7. Spatial    
>  8. Columnstore    
>  9. Index with included columns    
>  10.Index on computed columns  
>  _In this section, we will see Clustered and Nonclustered index_      

> * A _Clustered index_ determines the physical order of data in a table. For this reason, a table can have only one clustered index.   

**1. Clustered Index:**    
> ```sql  
>    CREATE TABLE [tblEmployee]  
>    (   
>     [Id] int Primary Key,     
>     [Name] nvarchar(50),   
>     [Salary]  int,  
>     [Gender]  nvarchar(10),  
>     [City] nvarchar(50)  
>    )     
> ```       
> Note, that Id column is marked as primary key. Primary key, constraint create clustered indexes automatically if no clustered index already exists on the table.  
> To confirm:   
> ```sql  
>   Execute sp_helpindex  tblEmployee     
> ```  
> _Note that, the values for Id column are not in a sequential order:_  
> ```sql   
>    Insert into tblEmployee Values(3, 'John', 4500, 'Male', 'New York')     
>    Insert into tblEmployee Values(1, 'Sam', 'Male', 'London')    
>    Insert into tblEmployee Values(4, 'Sara', 'Female', 'Tokyo')     
>    Insert into tblEmployee Values(5, 'Todd', 'Male', 'Toronto')     
>    Insert into tblEmployee Values(2, 'Pam', 'Female', 'Sydney')       
> ```   
> It will result into this table:   
> ![image](https://user-images.githubusercontent.com/58625165/211082879-78c8f3bf-a6f8-4af4-8a70-a0d546ce60ad.png)   
> _A Clustered Index is analogous to a telephone directory, where the data is arranged by the last name. We just learnt that, a table can have only one clustered index. However, the index can contain multiple columns (a composite index), like the way a telephone directory is organized by last name and first name._  
> Create a composite clustered index on the Gender and Salary columns   
> ```sql   
>   Create Clustered Index IX_tblEmployee_Gender_Salary   
>   ON tblEmployee(Gender DESC, Salary ASC)      
> ```   
> And the employee table is as follows:   
> ![image](https://user-images.githubusercontent.com/58625165/211086235-6e9aa0d8-d35a-4639-b479-86d096dac848.png)   
> So, clustered index also affects how the table will be displayed. See, it is now not sorted ID wise.   

**2. Nonclustered Index:**   
>  ```sql   
>     Create NonClustered Index IX_tblEmployee_Name   
>     ON tblEmployee(Name)     
>  ```   
>  ![image](https://user-images.githubusercontent.com/58625165/211087107-4d195bd8-c01c-4255-811e-7b5b3640460a.png)    
>  - A nonclustered index is analogous to an index in a textbook. The data is stored in one place, the index in another place. The index will have pointers to the storage location of the data.    
>  - Since, the nonclustered index is stored separately from the actual data, a table can have more than one non cluster index, just like how a book can have an index by common terms at the end.  
>  - In the index itself, the data is stored in an ascending or descending order of the index key, which doesn't in any way influence the storage of data in the table.   

> * **Difference b/w Clustered and NonClustered:**    
>   1. **Only one clustred index** per table, where as you can have more than one non clustered index   
>   2. **Clustered index is faster** than a non-clustered index, because, the clustered index has to refer back to the table, if the selected column is not present in the index.  
>   3. **Clustered index determines the storage order** of rows in the table, and hence doesn't require additional disk space, but where as NonClustered index is stored separately from the table, additional storage space is required.  
>    


### Unique and Non Unique Indexes in SQL Server   
> * **Unique index is used to enforce uniqueness of key values in the index**   
> ```sql   
>     CREATE TABLE [tblEmployee]   
>     (     
>          [Id] int Primary Key,       
>          [FirstName] nvarchar(50),   
>          [LastName] nvarchar(50),   
>          [Salary] int,   
>          [Gender] nvarchar(10),   
>          [City] nvarchar(50),   
>     )       
> ```   
> **Note:** By default, PRIMARY KEY constraint, creates a unique clustered index.   
> - **UNIQUENESS is a property of an index**, and both CLUSTERED and NON-CLUSTERED indexes can be UNIQUE.   
> ```sql   
>     Create Unique NonClustered Index   
>     UIX_tblEmployee_FirstName_LastName   
>     ON   tblEmployee(FirstName, LastName)     
> ```     
> * **Differences between Unique Constraint and Unique Index**   
> _There are no major differences between a unique constraint and a unique index. In fact, when you add a unique constraint, a unique index gets created behind the scenes._
> For adding a unique constraint to a table:     
> ```sql  
>       ALTER TABLE    tblEmployee   
>       ADD CONSTRAINT UQ_tblEmployee_City  
>       UNIQUE CLUSTERED(City)   -- or you can pass NONCLUSTERED flag to create the non-clustered constraint      
> ```      

>* **When should you be creating a Unique constraint over a unique index?**   
>_To make our intentions clear, create a unique constraint, when data integrity is objective. This makes the objective of the index very clear. In either cases, the data is validated in the same manner, and the query optimizer does not differentiate between a unique created by a unique constraint or manually created._  
>    
>  - **Useful pointers to remember:**   
>  **1. By default,** a PRIMARY KEY constraint, creates a unique clustered index, where as a UNIQUE constraint creates a unique Non-Clustered index. These defaults can be changed if you wish to.   
>  **2. A UNIQUE constraint or a UNIQUE index** cannot be created on an existing table, if the table contains duplicate values in the key columns. Obviously, to solve this, remove the key columns from the index definition or delete or update the duplicate values.   
>  


### Advantages and disadvantages of indexes in SQL Server
**1. Advantages:**    
> The following operations benefited by indexes:   
> ```sql   
>       --SELECT statement with a WHERE clause   
>       Select * from tblEmployee where Salary > 4000 and Salary < 8000 
>         
>       -- DELETE and UPDATE statement    
>       Delete from tblEmployee where Salary = 2500  
>       Update tblEmployee Set Salary = 9000 where Salary = 7500    
>         
>       -- ORDER BY ASCENDING  
>       Select * from tblEmployee order by Salary Desc   
>          
>       -- GROUP BY    
>       Select Salary, COUNT(Salary) as Total   
>       from tblEmployee  
>       Group By Salary     
> ```     
> So, while performing the above operations, SQL will only scan the index table and from the **row addresses** it will get respective data from the main tblEmployee table     

**2. Disadvantages:**     
> **Additional Disk Space:**  Clustered Index does not, require any additional storage. Every non-clustered index require additional space as it is stored separately from the table. The amount of the space required will depend on the size of the table, and the number and types of the columns used in the index.    
> **Insert Update and Delete statements becomes slow:**  When DML(Data Manipulation Language) statements (INSERT, UPDATE, DELETE) modifies data in a table, the data in all the indexes also needs to be updated. Indexes can help, to search and locate the rows, that we want to delete, but too many indexes to update can actually hurt the performance of data modifications.     


> **What is a covering query:**  If all the columns that you have requested in the SELECT clause of query, are present in the index, then there is no need to lookup in the table again. The requested column data can simply be returned from the index.  
> **A clustered index, always covers a query**,  since it contains all of the data in a table. A composite index is an index on two or more columns. Both clustered and non-clusered indexes can be composite indexes. To a certain extent, a composite index, can cover a query.   
>


### View in SQL Server  
> * **What is a View?**   
> _A view is nothing more than a saved SQL query. A view can also be considered as a virtual table._  
> ![image](https://user-images.githubusercontent.com/58625165/211096763-e0cbad8b-2752-4ba9-9c32-0e1a6b9f6f21.png)  
> ```sql  
>   Select Id, Name, Salary, Gender, DeptName  
>   from   tblEmployee   
>   join   tblDepartment  
>   on     tblEmployee.DepartmentId = tblDepartment.DeptId      
> ```  
> Now, to create a view we can issue this query:    
> ```sql   
>    Create View vWEmployeesByDepartment  
>    as   
>    Select Id, Name, Salary, Gender, DeptName   
>   from   tblEmployee   
>   join   tblDepartment  
>   on     tblEmployee.DepartmentId = tblDepartment.DeptId        
> ```    
> To execute the view, we can use the following query:    
> ```sql   
>       Select * from vWEmployeesByDepartment   
> ```    
> **Note:**  _A view don't store data, but it stores a SQL query._   
> ```sql  
>   sp_helptext  vWEmployeesByDepartment  
> ```  
> This will output the following:    
> ![image](https://user-images.githubusercontent.com/58625165/211098010-08987ea2-cdd6-4f12-a76f-16de5dd1ec9d.png)   

* **Advantages of Views**   
* - Views can be used to reduce the **complexity of the database schema.**     
* - Views can be used as a mechanism to implement **row and column level security.**      
* - views can be used to **present aggregate data** and hide detailed data.    
  
* **To modify a view-** ALTER VIEW statement
* **To drop a view-**  DROP VIEW vWName    
> Other thing is that view can be used to limit the access to data. Let's say we need to provide limited access to a person that can only see IT department's data, (In this we gonna implement **row-level security**):   
> ```sql   
>    Create View vWITEmployees   
>    as    
>    Select   Id, Name, Salary, Gender, DeptName   
>    from     tblEmployee   
>    join     tblDepartment   
>    on       tblEmployee.DepartmentId = tblDepartment.DeptId   
>    Where    tblDepartment.DeptName   = 'IT'       
> ```  
> Then you can issue a Select query to see the data for IT department via this view:   
> ```sql   
>     Select * from vWITEmployees     
> ```  
> The other case is to hide some specific columns (**column-level security**):      
> ```sql    
>    Create View vWNonConfidentialData   
>    as   
>    Select Id, Name, Gender, DeptName   
>    from   tblEmployee    
>    join   tblDepartment   
>    on     tblEmployee.DepartmentId =  tblDepartment.DeptId    
> ```   
> Then, we can have only 4 columns displayed, other columns will be hidden(here, Salary is hidden column):    
> ```sql  
>    Select * from vWNonConfidentialData       
> ```    
> ![image](https://user-images.githubusercontent.com/58625165/211100141-a637bdb9-c21a-4311-96d6-9afd29806de4.png)     
> Now, to **present aggregate data** only, we can have following view:    
> ```sql    
>    Create View vWSummerizedData   
>    as   
>    Select   DeptName, COUNT(Id) as TotatlEmployees     
>    from     tblEmployee    
>    join     tblDepartment   
>    on       tblEmployee.DepartmentId =  tblDepartment.DeptId      
>    Group by DeptName  
> ```      
> And select the view:   
> ```sql  
>   Select * from  vWSummerizedData  
> ```  
> ![image](https://user-images.githubusercontent.com/58625165/211100586-f5eb4b51-694b-4442-8ec6-483526f0014b.png)  
>


### Updatable views in SQL Server   
>* Is it possible to update a view?   **YES**    
>- This is underlying table tblEmployee for the view we created in previous section   
>![image](https://user-images.githubusercontent.com/58625165/211101187-783cba41-4ecf-4d85-a7ae-c765bd458e04.png)   
>```sql  
>   Update  vWEmployeesDataExceptSalary  
>   Set     Name = 'Mikey'  
>   Where   Id = 2;    
>```    
> So, the above query will update both the view and the underlying table:   
> ```sql  
>    Select  * from vWEmployeesDataExceptSalary  
>    Select  * from tblEmployee   
> ```   
> The updated view will be like:   
> ![image](https://user-images.githubusercontent.com/58625165/211101724-77cac46f-63aa-4b14-b602-e71854f70c3a.png)   
> And, the updated table will be:   
> ![image](https://user-images.githubusercontent.com/58625165/211101769-c521c3f9-6892-4fc0-b260-5351f1403143.png)   
> Same we can execute the following queries and it will update both the view(vWEmployeesDataExceptSalary) and the underlying table(tblEmployee)  
> ```sql   
>       Delete from vWEmployeesDataExceptSalary Where Id = 2  
>       Insert into vWEmployeesDataExceptSalary Values (2, 'Mikey', 'Male', 2)  
> ```   
> So, even though a view is not a table and only stores a SQL query, but by these behaviours it is considered as a **Virtual table**.   
> Behind the scenes, if we update a view it updates the underlying table(s). And sometime in weird way:   
> ```sql    
>   Update  vwEmployeeDetailsByDepartment  
>   Set     DeptName = 'IT'  
>   Where   Name  = 'John'  
> ```   
> Then then if we select the tables:   
> ```sql  
>   Select * from tblEmployees   
>   Select * from tblDepartment         
> ```
> It will output the following:   
> ![image](https://user-images.githubusercontent.com/58625165/211103335-2626e9a6-c93f-4cd3-b1b0-c0ae144d98df.png)   
> So, we wanted to update John's department from "HR" to "IT", but it has updated "Ben" department also. :)   
> So, the updating the view has also updated department table where ID = 3 from "HR" to "IT" and it affects all the employees which has DepartmentId as 3 :D.
>


### Indexed views in SQL Server   
> * **What is an Indexed View?**  or **What happens when you create an index on a view?**   
> _A standard or Non-indexed view, is just a stored SQL query. When, we try to retrieve data from the view, the data is actually retrieved form the underlying tables._  
> - So, a view is just a virtual table, it does not store any data, by default.  
> - However, when you create an index, on a view, the view gets materialized. This means, the view is now, capabe of storing data.  
> - In SQL server, we call them Indexed views and in Oracle, Materialized views.   
> ![image](https://user-images.githubusercontent.com/58625165/211104637-0b3b9796-c9c4-4e16-813b-791161a8adea.png)   
> We have ProductDetails and ProductSales tables:   
> ```sql   
>    Create View vWTotalSalesByProduct  
>    With SchemaBinding   
>    as   
>    Select Name,  
>    SUM(ISNULL((QuauntitySold * UnitPrice), 0)) as TotalSales,  
>    COUNT_BIG( * ) as TotalTransactions  
>    from  dbo.tblProductSales  
>    join  dbo.tblProduct  
>    on    dbo.tblProduct.ProductId = dbo.tblProductSales.ProductId   
>    Group By Name   
> ```    

>  **Guidelines for creating Indexed Views:**  
>  1. The view should be created with SchemaBinding option  
>  2. If an Aggregate function in the SELECT LIST, references an expression, and if there is a possibility for that **expression to become NULL**, then, a replacement value should be specified.  
>  3. If GROUP BY is specified, the view select list must contain a COUNT_BIG( * ) expression.   
>  4. The base tables in the view, should be referenced with 2 part name.   
>  ```sql    
>   Create Unique Clustered Index UIX_vWTotalSalesByProduct_Name   
>   on     vWTotalSalesByProduct_Name   
>  ```   
>  ```sql  
>   Create Unique Clustered Index UIX_vWTotalSalesByProduct_Name    
>   on     vWTotalSalesByProduct(Name)     
>  ```   
 

### View limitations in SQL Server    
>  1. You cannot pass parameters to a view. Table Valued functions are an excellent replacement for parameterized views.  
>  2. Rules and Defaults cannot be associated with views.     
>  3. The ORDER BY clause is invalid in views unless TOP or FOR XML is also specified.    
>  4. Views cannot be based on temporary tables.   
>  

### DML triggers in SQL Server
* **Triggers**   
> **In SQL server there are 3 types of triggers:**    
> 1. DML triggers   
> 2. DDL triggers   
> 3. Logon trigger   
> - DML triggers are fired automatically in response to DML events (INSERT, UPDATE & DELETE)  
> - DML triggers can be again classified into 2 types:    
> 1.  After triggers (Sometimes called as FORtriggers)  
> 2.  Instead of triggers   
> **After triggers, fires after the triggering action.**  The INSERT, UPDATE & DELETE statements, causes an after trigger to fire after the respective statements complete execution.   
> **INSTEAD of triggers, fires instead of the triggering action.**  The INSERT, UPDATE, and DELETE statements, causes an INSTEAD OF trigger to fire INSTEAD OF the respective statement execution.   
> ```sql   
>      CREATE TRIGGER tr_tblEmployee_ForInsert   
>      ON tblEmployee   
>      FOR INSERT   
>      AS    
>      BEGIN   
>            Declare @Id int   
>            Select  @Id = Id from inserted    
>                  
>            insert into tblEmployeeAudit   
>            values ('New employee with Id = ' +   
>                     Cast(@Id as nvarchar(5))  +   
>                     '  is added at ' +   
>                     cast(Getdate() as nvarchar(20))   
>            )   
>      END         
> ```    
> The above query will be triggered when insert operation will be performed on tblEmployee.    
> It will receive column values from **inserted**  
> So, for the following query it will receive ID - 8 from **inserted**:    
> ```sql    
>       Insert into tblEmployee values  (8, 'Ben', 4800, 'Male', 3)       
> ```      
> ```sql     
>      CREATE TRIGGER tr_tblEmployee_ForDelete      
>      ON tblEmployee   
>      FOR DELETE     
>      AS    
>      BEGIN   
>            Declare @Id int   
>            Select  @Id = Id from deleted       
>                  
>            insert into tblEmployeeAudit   
>            values ('An existing employee with Id = ' +   
>                     Cast(@Id as nvarchar(5))  +   
>                     '  is deleted at ' +   
>                     cast(Getdate() as nvarchar(20))   
>            )   
>      END
> ```   
> Same as for the INSERT operation, the below DELETE query will trigger the above trigger (tr_tblEmployee_ForDelete)   
> ```sql    
>   Delete from tblEmployee where Id = 3     
> ```     
> **Note:**  _inserted_ table will only available in scope of a trigger.   
> 


### After update trigger
### Instead of insert trigger 
### Instead of update trigger in SQL Server
### Instead of delete trigger in SQL Server
### Derived tables and common table expressions in SQL Server
### CTE in SQL Server
### Updatable common table expressions in SQL Server
### Recursive CTE in SQL Server
### Database normalization
### Second normal form and third normal fom
### Pivot in SQL Server
### Error handling in SQL Server
### Transactions in SQL Server
### Transactions in SQL Server and ACID Tests
### Subqueries in SQL Server
### Correlated subquery in SQL Server
### Creating a large table with random data for performance testing
### What to choose for performance SubQuery or Joins
### Cursors in SQL Server
### Replacing cursors using joins in SQL Server
### List all tables in a SQL Server database using a query
### Writing a runnable SQL Server scripts
### After database table columns without dropping table
### Optional parameters in SQL SERVER stored procedures
### Merge in SQL Server
### SQL SERVER concurrent transactions
### SQL SERVER dirty read example
### SQL SERVER lost update
### Non repeatable read example in SQL Server
### Phantom reads example in SQL Server
### Snapshot isolation level in SQL Server
### Read committed snapshot isolation level in SQL Server
### Difference between snapshot isolation and read committed
### SQL Server deadlock example
### SQL SERVER Deadlock victim selection
### Logging deadlocks in SQL Server
### SQL SERVER deadlock analysis and prevention
### Capturing deadlocks in SQL Server
### SQL SERVER deadlock error handling
### Handling deadlocks in ADO NET
### Retry logic for deadlock exceptions
### How to find blocking queries in SQL Server
### SQL SERVER except operator
### Difference between EXCEPT and NOT in SQL Server
### Intsect operator in SQL Server
### Difference between UNION, INTERSECT, and EXCEPT in SQL Server
### Cross apply and outer apply in SQL Server
### DDL Triggers in SQL Server
### Server scoped DDL triggers
### SQL SERVER trigger execution order
### Audit table changes in SQL Server
### Logon Triggers in SQL Server
### Select into in SQL Server
### Difference between wehre and having in SQL Server
### Table valued parameteres in SQL Server
### Send datatable as parameter to stored procedure
### Grouping Sets in SQL Server
### Rollup in SQL Server
### Cube in SQL Server
### Difference between cube and rollup in SQL Server
### Grouping function in SQL Server
### grouping ID funciton in SQL Server
### Debugging SQL Server stored procedures
### Over clause in SQL Server
### Row number function in SQL Server
### Rank and Dense Rank in SQL Server
### Difference between rank dense rand and row number in SQL Server
### Calculate running total in SQL Server 
### NTLE function in SQL Server
### Lead and Lag functions in SQL Server 2012
### FIRST VALUE function in SQL Server
### Window funcitons in SQL Server
### Difference between row and range
### LAST VALUE function in SQL Server
### UNPIVOT in SQL Server
### Reverse PIVOT table in SQL Server
### Choose function in SQL Server
### IIF function in SQL Server
### TRY PARSE FUNCTION IN SQL Server 2012
### TRY CONVERT funciton in SQL Server 2012
### EOMONTH funciton in SQL Server 2012
### DATAEFROMPARTS fucntion in SQL Server
### Difference between DatTime and SmallDateTime in SQL Server
### DateTime2FromParts function in SQL Server
### Difference between DateTime and DateTime2 in SQL Server
### Offset fetch next in SQL Server 2012
### Identifying object dependencies in SQL SERVER
### Sys DM SQL referencing entities in SQL SERVER
### SP depends in SQL Server
### Sequence object in SQL Server 2012
### Difference between sequence and identity in SQL Server
