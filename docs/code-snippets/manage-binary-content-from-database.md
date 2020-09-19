---
title: Manage VARBINARY column via T-SQL
# tags: [sql, blob, varbinary]
---

# Insert, update and extract a BLOB using T-SQL only

## Insert a BLOB 

```SQL
/* Create a table with a VARBINARY column */
CREATE TABLE Documents(
  [FileName] NVARCHAR(60),
  [FileType  NVARCHAR(60), 
  [Content]  VARBINARY(max)
)
GO

INSERT INTO Documents(
  [FileName], [FileType], [Content]
)
SELECT 
  N'Text1.txt' AS [FileName],
  N'.txt' AS [FileType],
  * FROM OPENROWSET(BULK N'C:\path\to\Text1.txt', SINGLE_BLOB) AS [Content]
GO
```

## Update content of a VARBINARY column

Assuming the same table as in the sample above

```SQL
UPDATE 
  Documents
SET 
  Content = (SELECT * FROM OPENROWSET(BULK N'c:\path\to\20180520215030133.docx', SINGLE_BLOB) AS T)
WHERE 
  [FileName] = N'Doc1.docx'
```

## Save content to file

Use this code to save the content of a blob (varbinary or image) 
into a file, using T-SQL only.

### Requirements

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

### Code

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





