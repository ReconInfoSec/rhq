Defense Evasion
=========================================
## Disabled security products 
**Description:** List all the disabled security products.

**Author:** [Janantha Marasinghe](https://medium.com/@blueteamops)

**Query:** 

```SELECT * FROM windows_security_products WHERE state = 'Off';
```
