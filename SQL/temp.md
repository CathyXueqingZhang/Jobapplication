# Temporary Table
Temporary tables are created in tempdb. The name "temporary" is slightly misleading, for even though the tables are instantiated in tempdb, they are backed by physical disk and are even logged into the transaction log. They act like regular tables in that you can query their data via SELECT queries and modify their data via UPDATE, INSERT, and DELETE statements. <br/>
Temporary table name started with a "#" sign. <br/>
```
CREATE TABLE dbo.#Cars 
   (   
   Car_id int NOT NULL, 
   ColorCode varchar(10), 
   ModelName varchar(20), 
   Code int, 
   DateEntered datetime 
   ) 
INSERT INTO dbo.#Cars (Car_id, ColorCode, ModelName, Code, DateEntered) 
VALUES (1,'BlueGreen', 'Austen', 200801, GETDATE()) 

SELECT Car_id, ColorCode, ModelName, Code, DateEntered FROM dbo.#Cars 

DROP TABLE dbo.[#Cars]
```
we need to execute a DROP TABLE statement against #Cars. This is because the table persists until the session ends or until the table is dropped.

```
--Table Variable: 
DECLARE Cars TABLE 
   ( 
   Car_id int NOT NULL, 
   ColorCode varchar(10), 
   ModelName varchar(20), 
   Code int , 
   DateEntered datetime 
   ) 

INSERT INTO Cars (Car_id, ColorCode, ModelName, Code, DateEntered) 
VALUES (1,'BlueGreen', 'Austen', 200801, GETDATE()) 

SELECT Car_id, ColorCode, ModelName, Code, DateEntered FROM Cars
```
