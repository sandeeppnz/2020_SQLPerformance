# SQL Performance and Optimisation

## Tools and concepts
- SQL Server client
- Data in a table is stored in a tree like structure called Clustered Index Structure

![Capture10](https://user-images.githubusercontent.com/5715815/88490453-e4253b00-cfef-11ea-913e-4607d8593d9e.PNG)

- Leaf nodes store datarows known as a page (8KB)
- Data is stored in sorted order by the Cluster Key (by default primary key will be cluster key)
- Avoid scan operations by introducing indexes (e.g. student name)
- Uses RowPointers (RP) points back to the rows   

![image](https://user-images.githubusercontent.com/5715815/88501230-f10d5300-d01e-11ea-80c0-70d70cc04c4f.png)

![image](https://user-images.githubusercontent.com/5715815/88501328-3d589300-d01f-11ea-9129-f17500846f1c.png)


## How SQL Server executes them

- Generate an execution plan (this does not run the execution): Execution plan (watch out for Clustered Index Scan) however Clustered Index Seek, Estimated Operator Cost, 
![image](https://user-images.githubusercontent.com/5715815/88502441-82ca8f80-d022-11ea-9756-c63f2b402be6.png)

- Adding a command (this runs a execution): 
SET Statistics IO ON
SET Statistics TIME ON
* Should be careful with DML (updates and delete statements). This is going run the queries. 

- Pay attention to the Logical reads (a read of a page): when sql server has to read a page from memory or disk to process the statement
- 12023 x 8 KB data to process as shown below:
![image](https://user-images.githubusercontent.com/5715815/88622834-bc20ff00-d0f7-11ea-9f26-b1cac6d8ea93.png)
- if the CPU time is larger than the elapsed time, that indicates that SQL server has used parallel execution 
- So minimise a logical reads

- Reading an execution plan

![image](https://user-images.githubusercontent.com/5715815/88761948-3d45c800-d1c4-11ea-8448-f6e376c90415.png)

The solution is given below, create the index:
![image](https://user-images.githubusercontent.com/5715815/88761971-50589800-d1c4-11ea-9b6a-b4642e172bb1.png)

Next, check the execution plan again:
![image](https://user-images.githubusercontent.com/5715815/88762047-8007a000-d1c4-11ea-8b90-5500dbe10eda.png)

Now the logical reads have decreased:
![image](https://user-images.githubusercontent.com/5715815/88762141-bb09d380-d1c4-11ea-95b0-a488cb9f4183.png)


### Re-writing the Query
![image](https://user-images.githubusercontent.com/5715815/88762678-c1e51600-d1c5-11ea-9d66-0bdb538afd8c.png)

vs 

![image](https://user-images.githubusercontent.com/5715815/88762708-d32e2280-d1c5-11ea-87cc-be16dda93848.png)


Scan vs Seek: need to question why the scan is used

- Nested Loops Join: For each value in the first data set, SQL server loops through the second data set looking for matches. 
- Merge Joins are efficient, but need to be sorted first. Used to join two datasets that are already sorted using the same key. A row from each source is obtained. If the rows match they are joined. If the rows do not match, the lower value row is discarded and a new row is obtained from that source.
- Hash Match: (expensive operation, for larger dataset is involved, signifies a missing index key, add a where clause, missing a foreign key) A hashable of the smaller data set is create, then SQL server loops thorough the data larger data set probing the hashable for matching values. Used when two large datasets must be joined.

- Refer: SQL Server Execution Plans by Grant Fritchey https://assets.red-gate.com/community/books/sql-server-execution-plans-3rd-edition.pdf
- https://www.red-gate.com/simple-talk/books/sql-server-execution-plans-third-edition-by-grant-fritchey/






## Indexing

## Query performance statistics

## Profiling in SQL server

## Application practices


