Query Tips & Tricks
=========================================

## Join two tables
  - The `p` calls from the `processes` table
  - The `u` calls from the `users` table
  - `u.uid=p.uid` portion of the command gives the part of the schema that both have in common allowing the join
  - Calls from two separate `processes` and `users` using the `uid` to match

```sql
SELECT p.parent, p.path, p.pid, p.cwd, u.uid, u.username
FROM processes p
JOIN users u ON u.uid=p.uid;
```

## Sub-queries

```sql
SELECT address, mac, mac_count
  FROM
    (SELECT address, mac, COUNT(mac) AS mac_count FROM arp_cache GROUP BY mac)
  WHERE mac_count > 1;
```