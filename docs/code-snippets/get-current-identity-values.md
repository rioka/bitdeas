---
title: Get current value for IDENTITY
# tags: [sql]
---

# Current value for IDENTITY

The following script get the current value of `IDENTITY` for column in a database

```SQL
SELECT 
  TABLE_NAME,
  TABLE_SCHEMA,
  IDENT_SEED(TABLE_NAME) AS Seed,
  IDENT_INCR(TABLE_NAME) AS Increment,
  IDENT_CURRENT(TABLE_NAME) AS Current_Identity
FROM 
  INFORMATION_SCHEMA.TABLES
WHERE 
  OBJECTPROPERTY(OBJECT_ID(TABLE_NAME), 'TableHasIdentity') = 1
  AND TABLE_TYPE = 'BASE TABLE'
```

To filter by table, simply add proper clause for `TABLE_NAME`, `TABLE_SCHEMA`