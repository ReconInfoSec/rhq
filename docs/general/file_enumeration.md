File Enumeration
=========================================

## List directory contents
**Description:** A non-recursive (single level) directory listing.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT *
FROM file
WHERE path LIKE 'C:\Users\%';
```

```sql tab="MacOS"
SELECT *
FROM file
WHERE path LIKE '/Users/%';
```

```sql tab="Linux"
SELECT *
FROM file
WHERE path LIKE '/home/%';
```

## Recursive directory listing
```sql tab="Windows"
SELECT *
FROM file
WHERE path LIKE 'C:\Users\username\%%';
```

```sql tab="MacOS"
SELECT *
FROM file
WHERE path LIKE '/Users/username/%%';
```

```sql tab="Linux"
SELECT *
FROM file
WHERE path LIKE '/home/username/%%';
```

## List downloads for all users
```sql tab="Windows"
SELECT *
FROM file
WHERE path LIKE 'C:\Users\%\Downloads\%%';
```

```sql tab="MacOS"
SELECT *
FROM file
WHERE path LIKE '/Users/%/Downloads/%%';
```

```sql tab="Linux"
SELECT *
FROM file
WHERE path LIKE '/home/%/Downloads/%%';
```

## List executables in temp directories
```sql tab="Windows"
SELECT btime,ctime,mtime,directory,filename,path,size
FROM file
WHERE (path LIKE 'C:\Users\%\AppData\Local\Temp\%' OR path LIKE 'C:\Windows\temp\%') 
AND (filename LIKE '%.exe' OR filename LIKE '%.dll');
```

```sql tab="MacOS"
Contribute a query!
```

```sql tab="Linux"
Contribute a query!
```

## Obtain hashes of a file
- **NOTE:** This type of query should only be performed against **specific files**, not entire directories and certainly not recursively against many directories as calculating hashes is resource intensive.

```sql tab="Windows"
SELECT *
FROM hash
WHERE path LIKE 'C:\path\to\legit.docx';
```

```sql tab="MacOS"
SELECT *
FROM hash
WHERE path LIKE '/Users/%/Downloads/legit.docx';
```

```sql tab="Linux"
SELECT *
FROM hash
WHERE path LIKE '/home/%/Downloads/legit.docx';
```