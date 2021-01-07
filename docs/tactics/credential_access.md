Credential Access
=========================================

## ProcDump
**Description:** Identify systems that the ProcDump EULA has been accepted. Read more about the technique [here](https://medium.com/@markmotig/some-ways-to-dump-lsass-exe-c4a75fdc49bf).

- `mtime` = Time that EULA was accepted

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:**

```sql tab="Windows"
SELECT datetime(mtime, 'unixepoch', 'localtime') AS EULA_accepted,path 
FROM registry 
WHERE path LIKE 'HKEY_USERS\%\Software\Sysinternals\ProcDump\EulaAccepted';
```