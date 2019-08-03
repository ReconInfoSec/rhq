Impact
=========================================

## File Deletion
**Description:** List recycled files for all users on the system.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT datetime(atime, 'unixepoch', 'localtime') AS atime,datetime(btime, 'unixepoch', 'localtime') AS btime,datetime(ctime, 'unixepoch', 'localtime') AS ctime,datetime(mtime, 'unixepoch', 'localtime') AS mtime,path,device,filename,size,type,uid,volume_serial FROM file 
WHERE path LIKE 'C:\$Recycle.bin\%%';
```
