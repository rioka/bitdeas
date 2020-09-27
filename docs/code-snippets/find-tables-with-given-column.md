---
title: Find tables with specific column 
# tags: [sql]
---

# Find all tables with a specific column

The following code returns all tables with a column whose name containt the string `customer`

```SQL
DECLARE
  @colNameLike  nvarchar(100),
  @colName      nvarchar(100)

SET @colNameLike = '%customer%'
--SET @colName = ''

SELECT 
  T.name AS table_name, 
  SCHEMA_NAME(schema_id) AS schema_name,
  C.name AS column_name
FROM 
  sys.tables AS T
INNER JOIN 
  sys.columns C ON T.OBJECT_ID = C.OBJECT_ID
WHERE 
  (@colNameLike is not null and C.name LIKE @colNameLike)
  OR (@colName is not null and C.name = @colName)
ORDER BY 
  schema_name, 
  table_name;
```
