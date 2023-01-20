## Best Practice


Query select stored procedure execute in SQL Job Agent
```SQL
SELECT
    [sJOB].[job_id] AS [JobID]
    , [sJOB].[name] AS [JobName]
    , [sJSTP].[step_uid] AS [StepID]
    , [sJSTP].[step_id] AS [StepNo]
    , [sJSTP].[step_name] AS [StepName]
    , CASE [sJSTP].[subsystem]
        WHEN 'ActiveScripting' THEN 'ActiveX Script'
        WHEN 'CmdExec' THEN 'Operating system (CmdExec)'
        WHEN 'PowerShell' THEN 'PowerShell'
        WHEN 'Distribution' THEN 'Replication Distributor'
        WHEN 'Merge' THEN 'Replication Merge'
        WHEN 'QueueReader' THEN 'Replication Queue Reader'
        WHEN 'Snapshot' THEN 'Replication Snapshot'
        WHEN 'LogReader' THEN 'Replication Transaction-Log Reader'
        WHEN 'ANALYSISCOMMAND' THEN 'SQL Server Analysis Services Command'
        WHEN 'ANALYSISQUERY' THEN 'SQL Server Analysis Services Query'
        WHEN 'SSIS' THEN 'SQL Server Integration Services Package'
        WHEN 'TSQL' THEN 'Transact-SQL script (T-SQL)'
        ELSE sJSTP.subsystem
      END AS [StepType]
    , [sPROX].[name] AS [RunAs]
    , [sJSTP].[database_name] AS [Database]
    , [sJSTP].[command] AS [ExecutableCommand]
    , CASE [sJSTP].[on_success_action]
        WHEN 1 THEN 'Quit the job reporting success'
        WHEN 2 THEN 'Quit the job reporting failure'
        WHEN 3 THEN 'Go to the next step'
        WHEN 4 THEN 'Go to Step: ' 
                    + QUOTENAME(CAST([sJSTP].[on_success_step_id] AS VARCHAR(3))) 
                    + ' ' 
                    + [sOSSTP].[step_name]
      END AS [OnSuccessAction]
    , [sJSTP].[retry_attempts] AS [RetryAttempts]
    , [sJSTP].[retry_interval] AS [RetryInterval (Minutes)]
    , CASE [sJSTP].[on_fail_action]
        WHEN 1 THEN 'Quit the job reporting success'
        WHEN 2 THEN 'Quit the job reporting failure'
        WHEN 3 THEN 'Go to the next step'
        WHEN 4 THEN 'Go to Step: ' 
                    + QUOTENAME(CAST([sJSTP].[on_fail_step_id] AS VARCHAR(3))) 
                    + ' ' 
                    + [sOFSTP].[step_name]
      END AS [OnFailureAction]
FROM
    [msdb].[dbo].[sysjobsteps] AS [sJSTP]
    INNER JOIN [msdb].[dbo].[sysjobs] AS [sJOB]
        ON [sJSTP].[job_id] = [sJOB].[job_id]
    LEFT JOIN [msdb].[dbo].[sysjobsteps] AS [sOSSTP]
        ON [sJSTP].[job_id] = [sOSSTP].[job_id]
        AND [sJSTP].[on_success_step_id] = [sOSSTP].[step_id]
    LEFT JOIN [msdb].[dbo].[sysjobsteps] AS [sOFSTP]
        ON [sJSTP].[job_id] = [sOFSTP].[job_id]
        AND [sJSTP].[on_fail_step_id] = [sOFSTP].[step_id]
    LEFT JOIN [msdb].[dbo].[sysproxies] AS [sPROX]
        ON [sJSTP].[proxy_id] = [sPROX].[proxy_id]
WHERE 1 =1 
--AND [sJOB].[name] LIKE '%EDI%' -- Tên job
--AND [sJSTP].[step_name] LIKE '%EDI%' -- Tên step 
AND [sJSTP].[command] LIKE N'%usp_data_extract_dual_invoice%' -- Stored procedure run job
ORDER BY [JobName], [StepNo]
```

Script get user login
```SQL
select p.Email, u.Password, u.*
from retail.blu.tbl_user u
join retail.blu.tbl_person_user p
on u.PersonUserID = p.PersonUserID
and p.Active = 1
where u.Password != ''
and u.PersonUser = 1
and u.Active = 1
and clientIntid in (70,26, 84, 134, 26)
```

Remember when create a new stored procedure
![[Note1_SQL.png]]

Script check column name in scheme
```SQL
USE master  
SELECT *  
FROM EDFDB01.BlueEDF_Sbx.INFORMATION_SCHEMA.COLUMNS  
WHERE COLUMN_NAME LIKE N'%Address1%';
```

Pivot Column sample 
```SQL
use AdvWrk17
select * from dbo.Products

declare @colsPivot nvarchar(256) 
declare @colPivot nvarchar(128)
declare @query nvarchar(max)

select @colsPivot = 
  STUFF((SELECT ', IsNull(' + QUOTENAME(rtrim(p.CategoryID)) +', 0) as ['+ rtrim(p.CategoryID)+']' 
                    from dbo.Products p
                   GROUP BY p.CategoryID
				   ORDER BY p.CategoryID
            FOR XML PATH(''), TYPE
            ).value('.', 'NVARCHAR(MAX)') 
        ,1,1,'')

print @colsPivot

select @colPivot = 
  STUFF((SELECT ','  + QUOTENAME(p.CategoryID) 
                   from dbo.Products p
                   GROUP BY p.CategoryID
				   ORDER BY p.CategoryID
            FOR XML PATH(''), TYPE
            ).value('.', 'NVARCHAR(MAX)') 
        ,1,1,'')

print @colsPivot

SET @query = '
SELECT   SupplierID,' + @colsPivot + ' 
		 from 
         (
            select *, CONVERT(int, isnull(p.UnitsInStock, 0)) as UnitStock
            from Products p
         ) x
         pivot 
         (
            sum(UnitStock)
            for CategoryID in (' + @colPivot + ')
         ) p 
'

select *, convert(int, ISNULL(p.UnitsInStock, 0))  from Products p

EXEC(@query)
```


