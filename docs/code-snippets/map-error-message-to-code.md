---
title: Get SQL Server error code from message
#tags: [sql, error]
---

# Get SQL Server error code from an error message 

Sometimes you want to get the error code for a gioven  error message, e.g. to add custom 
error handling code; the following statement can be used to retrieve the error code(s) matching an error message.

```SQL
DECLARE
  @errorMsg NVARCHAR(100),
  @langId   INT

SET @errorMsg = '%duplicate%';

/* set a specific language, if known */
SET langId = 1033

SELECT 
  * 
FROM 
  [sys.messages]
WHERE 
  [text] LIKE @errorMsg 
  -- and [text] like '%key%' 
  AND ([language_id] = @langId 
       OR @langId IS NULL)
```       