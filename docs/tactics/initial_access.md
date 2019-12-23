Initial Access
=========================================

## Email

### Email Attachments
**Description:** List and hash all files in common Outlook temp directories

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT * FROM hash 
WHERE (path LIKE 'C:\Users\%\AppData\Local\Temp\%.tmp\%' 
OR path LIKE 'C:\Users\%\AppData\Local\Microsoft\Outlook%%'
OR path LIKE 'C:\Documents and Settings\%\Local Settings\Temporary Internet Files\Content.Outlook%%');
```

## File Opening
### Jump Lists
**Description:** Enumerate LNK files in user jump lists, evidence of file opening.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT datetime(btime, 'unixepoch', 'localtime') AS firstaccess,
datetime(mtime, 'unixepoch', 'localtime') AS lastaccess,filename,path
FROM file
WHERE path LIKE 'C:\Users\%\AppData\Roaming\Microsoft\Windows\Recent\%.lnk'
ORDER BY lastaccess DESC;
```

## File Download
### Open/Save MRU
**Description:** Tracks files that have been opened or saved within a Windows shell dialog box

- https://digital-forensics.sans.org/blog/2010/04/02/openrunsavemru-lastvisitedmru/

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT datetime(mtime, 'unixepoch', 'localtime') AS mtime,name,path,key FROM registry 
WHERE path LIKE 'HKEY_USERS\%\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidlMRU\%%';
```
