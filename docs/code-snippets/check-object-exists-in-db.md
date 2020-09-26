---
title: Check if an object exists in a database
# tags: [sql]
---

## Check if a table exists

There are many ways to check for a table

### Use INFORMATION_SCHEMA.TABLES

```SQL
IF EXISTS (SELECT 1 
           FROM   INFORMATION_SCHEMA.TABLES 
           WHERE  SCHEMA_NAME = N'orders'
           AND    TABLE_NAME = N'Customers')
BEGIN
  -- do something
END
```

### Use OBJECT_ID

```SQL
IF OBJECT_ID(N'orders.Customers', N'U') IS NOT NULL
BEGIN
  -- do something
END
```

### Use sys.objects Catalog View

```SQL
IF EXISTS(SELECT 1 
          FROM   sys.objects 
          WHERE  object_id = OBJECT_ID(N'orders.Customers') 
          AND    [type] = N'U')
BEGIN
  -- do something
END
```

### Use sys.tables Catalog View

```SQL
IF EXISTS(SELECT 1 
          FROM   sys.tables T
          INNER JOIN sys.schemas S
          ON     T.schema_id = S.schema_id
          WHERE  T.[name] = N'Customers') 
          AND    T.[type] = N'U'
          AND    S.[name] = N'orders')
BEGIN
  -- do something
END

*We can skip JOIN if there if database has just one schema, or tables have unique names.*
```

### Use sys.sysobjects 

Should be avoided, as `sys.sysobjects` is being deprecated.