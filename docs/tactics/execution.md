Execution
=========================================

## Prefetch files
**Description:** Prefetch is one of several "evidence of execution" artifacts. 

- `btime` = First execution
- `mtime` = Last execution
- Timestamps are in epoch, use converter: [https://www.epochconverter.com/](https://www.epochconverter.com/)
- Will convert time  from epoch to local `datetime(btime, 'unixepoch', 'localtime') as ctime ` when defined after select

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:**

```sql tab="Windows"
SELECT datetime(btime, 'unixepoch', 'localtime') AS firstrun,datetime(mtime, 'unixepoch', 'localtime') AS lastrun,filename
FROM file
WHERE path LIKE 'C:\Windows\Prefetch\%.pf'
ORDER BY lastrun DESC;
```

## UserAssist
**Description:** 

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT * FROM registry 
WHERE path like 'HKEY_USERS\%\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\%%';
```

## AppCompat Shims
**Description:** Application Compatibility shims are a way to persist malware. This table presents the AppCompat Shim information from the registry in a nice format. See http://files.brucon.org/2015/Tomczak_and_Ballenthin_Shims_for_the_Win.pdf for more details.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT * FROM appcompat_shims;
```

## Last-Visited MRU
Values stored in REG_BINARY format – decode with CyberChef recipe: https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')Decode_text('UTF16LE%20(1200)')

```sql tab="Windows"
SELECT * FROM registry 
WHERE path LIKE 'HKEY_USERS\%\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU\%%';
```

## RecentApps
**Description:** 
GUI Program execution launched on the Win10 system is tracked in the RecentApps key

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT * FROM registry 
WHERE path LIKE 'HKEY_USERS\%\Software\Microsoft\Windows\CurrentVersion\Search\RecentApps';
```

## Unsigned binaries in system directories
**Description:** 
File (executable, bundle, installer, disk) code signing status **NOTE:** Potential for high false positives, validate with sigcheck/SignTool

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT * 
FROM authenticode 
WHERE path LIKE 'C:\Windows\System32\%' 
AND (path like '%.exe' OR path like '%.dll' OR path like '%.sys') 
AND result = 'missing';
```

## Unsigned/unverified drivers
**Description:** List all loaded drivers without a digital signature.

- https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/Driver-Signing-changes-in-Windows-10-version-1607/ba-p/364894

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT * 
FROM drivers 
WHERE signed != '1';
```

## Process without binary on disk
**Description:** Check running processes without a binary on disk, filtering out common false positives

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT * 
FROM processes 
WHERE on_disk != '1' 
AND gid >= 1 
AND cmdline != '\SystemRoot\System32\smss.exe';
```

## Suspicious PowerShell
**Description:** Needs additional testing/benchmarking

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT script_name,script_path,script_text,datetime(time, 'unixepoch', 'localtime') AS time
FROM powershell_events 
WHERE (script_text LIKE '%-en%' OR script_text LIKE '%DownloadString%' OR script_text LIKE '%-nop%' OR script_text LIKE '%hidden%' OR script_text LIKE '%IEX%' OR script_text LIKE '%http%');
```