# SQL Performance

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

## Indexing

## Query performance statistics

## Profiling in SQL server

## Application practices


