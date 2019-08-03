Configuration Audits
=========================================

## Active Directory / GPO
### Checks number of allowed cached credentials 
Default is 10, best practice is lower on key terrain.

```sql tab="Windows"
SELECT data
FROM registry
WHERE path='HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\CachedLogonsCount';
```

### Domain information

```sql tab="Windows"
SELECT *
FROM ntdomains;
```

## Patch level

```sql tab="Windows"
SELECT *
FROM patches
```

## Software

### Installed Chrome extensions

```sql tab="All Platforms"
SELECT *
FROM chrome_extensions
WHERE uid = (SELECT u.uid from users u, logged_in_users liu WHERE liu.user = u.username);
```