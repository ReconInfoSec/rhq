Persistence
=========================================

## Autoexec (kitchen sink)
**Description:** Aggregate of executables that will automatically execute on the target machine. This is an amalgamation of other tables like services, scheduled_tasks, startup_items and more.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT *
FROM autoexec;
```

## Scheduled Tasks
**Description:** List all scheduled tasks, returning only those that are enabled.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT datetime(last_run_time, 'unixepoch', 'localtime') AS last_run_time,datetime(next_run_time, 'unixepoch', 'localtime') AS next_run_time,action,enabled,hidden,last_run_code,last_run_message,name,path,state 
FROM scheduled_tasks 
WHERE enabled != 0;
```

## Startup Items
**Description:** List all startup items, returning only those that are enabled.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT * 
FROM startup_items 
WHERE status = 'enabled' 
AND path NOT LIKE '%\desktop.ini' 
AND path NOT LIKE 'C:\Windows\System32\mctadmin.exe' 
AND path NOT LIKE '%Sidebar.exe /autoRun';
```

## Services
**Description:** List all services, returning only those that are enabled.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT * 
FROM services 
WHERE start_type != 'DISABLED';
```

## WMI Event Consumers
### WMI Event Filters
**Description:** WMI event filters, filtering out common false positives.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT *
FROM wmi_event_filters 
WHERE (name NOT like 'BVTFilter' AND name NOT like 'SCM Event Log Filter');
```

### WMI CLI Event Consumers
**Description:** WMI command line event consumers, filtering out common false positives.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT *
FROM wmi_cli_event_consumers
WHERE name NOT like 'BVTConsumer';
```

### WMI Script Event Consumers
**Description:** WMI script event consumers.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT *
FROM wmi_script_event_consumers;
```

### WMI Filter+Consumer Bindings
**Description:** WMI event filter/consumer/bindings, filtering out common false positives.

**Author:** [@eric_capuano](https://twitter.com/eric_capuano)

**Query:** 

```sql tab="Windows"
SELECT * 
FROM wmi_filter_consumer_binding 
WHERE (filter NOT LIKE '%BVTFilter%' AND filter NOT LIKE '%SCM Event Log Filter%');
```