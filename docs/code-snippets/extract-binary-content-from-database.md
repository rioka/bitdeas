---
title: Save VARBINARY column to a file
# tags: [sql, blob, varbinary]
---

# Extract the content of a VARBINARY (or IMAGE) column into a file using T-SQL only

Use this code to save  the content of a blob (varbinary or image) 
into a file, using T-SQL only.

## Requirements

```SQL
sp_configure 'show advanced options', 1;  
GO  

RECONFIGURE;  
GO  

sp_configure 'Ole Automation Procedures', 1;  
GO  

RECONFIGURE;  
GO 
``` 

## Code

```SQL
DECLARE 
  @rawData      VARBINARY(MAX),
  @timestamp    VARCHAR(MAX),
  @objectToken  INT

/* sample select */
DECLARE IMGPATH 
  CURSOR FAST_FORWARD FOR 
  SELECT Content
  FROM [dbName].dbo.Reports 
  WHERE id = 7140

OPEN IMGPATH 

FETCH NEXT FROM IMGPATH INTO @rawData

WHILE @@FETCH_STATUS = 0
    BEGIN
        SET @timestamp = 'c:\path\to\folder\' + REPLACE(REPLACE(REPLACE(REPLACE(CONVERT(VARCHAR, GETDATE(), 121), '-', ''), ':', ''), '.', ''), ' ', '') + '.docx'

        PRINT @timestamp

        EXEC sp_OACreate 'ADODB.Stream', @objectToken OUTPUT
        EXEC sp_OASetProperty @objectToken, 'Type', 1
        EXEC sp_OAMethod @objectToken, 'Open'
        EXEC sp_OAMethod @objectToken, 'Write', NULL, @rawData
        EXEC sp_OAMethod @objectToken, 'SaveToFile', NULL, @timetamp, 2
        EXEC sp_OAMethod @objectToken, 'Close'
        EXEC sp_OADestroy @objectToken

        FETCH NEXT FROM IMGPATH INTO @rawData
    END 

CLOSE IMGPATH
DEALLOCATE IMGPATH
```




