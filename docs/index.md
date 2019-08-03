Recon Hunt Queries
=========================================
Welcome to the Recon Hunt Queries repo! 
## About 
This project is proudly maintained by [Recon InfoSec](http://reconinfosec.com) to support the community of osquery users!

Our goal with this project is to have a consolidated place for **incident response & threat hunting** focused queries for **[osquery](https://github.com/osquery/osquery)**. We've grouped the queries by the [MITRE ATT&CK](https://attack.mitre.org/wiki/Main_Page) tactics they support, but there are a few "General" categories of queries as well. Use the navigation bar to the left to explore.

These are collections of **individual queries** for specific use cases, not query packs which are a [separate thing](https://www.darkbytes.com/osquery-scheduled-queries-packs/) altogether.

These queries are great for on-demand hunting across hundreds or thousands of systems via osquery [distributed queries](https://osquery.readthedocs.io/en/stable/deployment/remote/) using a frontend like [Kolide Fleet](https://github.com/kolide/fleet).

There are several other great projects that track example queries, be sure to check them out!

- [osquery packs](https://github.com/osquery/osquery/tree/master/packs)
- [osquery queryhub](https://github.com/osquery/queryhub)

## Contribute
Please contribute any queries you've found useful for threat hunting & incident response! Be sure to study the [osquery Schema](https://osquery.io/schema/) for inspiration.

Notice the "edit" icon at the top right of every page? Click on it, add your stuff, submit a PR -> raise the collective capabilities of osquery hunters everywhere!

### Query template
The following markdown code produces the example below it.

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

---

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

---

For a query that is universal across all supported osquery platforms, simply specify "All Platforms" as in the `tab`

If your query is only applicable to one platform, feel free to omit the non-applicable tabs.