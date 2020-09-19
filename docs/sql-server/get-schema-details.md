---
title: Get schema details
---

# How to Get Information About Schemas


Both `INFORMATION_SCHEMA.TABLES` and `sys.*` are views.
Their definitions are available in `OBJECT_DEFINITION`

```sql
SELECT OBJECT_DEFINITION(OBJECT_ID('INFORMATION_SCHEMA.TABLES'))
SELECT OBJECT_DEFINITION(OBJECT_ID('sys.tables'))
SELECT OBJECT_DEFINITION(OBJECT_ID('sys.schemas'))
```

When you run a query against `INFORMATION_SCHEMA.TABLES`, you're actually running a query against a simplified version of `sys.objects` and `sys.schemas`.
So instead of `schema.Tables`, we can use `sys_table`.