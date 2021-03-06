# Lateral Movement

## SMB / Named Pipes
**Description:** Named pipes are an inter-process communication mechanism on Windows and are very often leveraged by malware and C2 beacons.

- https://blog.cobaltstrike.com/2013/12/06/stealthy-peer-to-peer-cc-over-smb-pipes/
- https://medium.com/@petergombos/smb-named-pipe-pivoting-in-meterpreter-462580fd41c5

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT proc.parent AS process_parent, proc.path AS process_path, proc.pid AS process_id, proc.cwd AS process_directory, pipe.pid AS pipe_pid, pipe.name AS pipe_name 
FROM processes proc 
JOIN pipes pipe ON proc.pid=pipe.pid;
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

## PsExec
**Description:** Identify systems that the PsExec EULA has been accepted.

- `mtime` = Time that EULA was accepted

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:**

```sql tab="Windows"
SELECT datetime(mtime, 'unixepoch', 'localtime') AS EULA_accepted,path 
FROM registry 
WHERE path LIKE 'HKEY_USERS\%\Software\Sysinternals\PsExec\EulaAccepted';
```