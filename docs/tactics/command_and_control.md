Networking
=========================================

## Listening Processes
**Description:** Get the process name, port, and PID, for processes listening on all interfaces

**Author:** 

**Query:** 

```sql tab="All Platforms"
SELECT DISTINCT processes.name, listening_ports.port, processes.pid
  FROM listening_ports JOIN processes USING (pid)
  WHERE listening_ports.address = '0.0.0.0';
```

## ARP anomalies
**Description:** ARP anomalies

**Author:** 

**Query:** 

```sql tab="All Platforms"
SELECT address, mac, COUNT(mac) AS mac_count
  FROM arp_cache GROUP BY mac
  HAVING count(mac) > 1;
```