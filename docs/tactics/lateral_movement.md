# Lateral Movement

## SMB / Named Pipes
**Description:** Named pipes are an inter-process communication mechanism on Windows and are very often leveraged by malware and C2 beacons.

- https://blog.cobaltstrike.com/2013/12/06/stealthy-peer-to-peer-cc-over-smb-pipes/
- https://medium.com/@petergombos/smb-named-pipe-pivoting-in-meterpreter-462580fd41c5

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query1:** 

```sql tab="Windows"
SELECT proc.parent AS process_parent, proc.path AS process_path, proc.pid AS process_id, proc.cwd AS process_directory, pipe.pid AS pipe_pid, pipe.name AS pipe_name 
FROM processes proc 
JOIN pipes pipe ON proc.pid=pipe.pid;
```

##Provide default named pipes used by most popular post exploitation frameworks
**Query2:** 
```sql tab="Windows"
SELECT * from pipes WHERE name LIKE 'psexesvc%' OR name LIKE 'remcom%' OR name LIKE 'gruntsvc%' OR name LIKE 'msagent%' OR name LIKE 'status%' OR name LIKE 'csexecsvc%' OR name LIKE 'TestSVC%' OR name LIKE 'jaccdpqnvbrrxlaf' OR name LIKE 'Posh%';
```

## Logged in users
**Description:** Get all logged on users. Helpful if you already suspect a compromised account and want to quickly identify where that account is in use.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="All Platforms"
SELECT * 
FROM logged_in_users 
WHERE user = 'compromised.username';
```
