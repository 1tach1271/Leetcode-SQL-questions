# SQL (Structured Query Language)
- It is a standard language for storing, manipulation and retrieving data in databases.
- SQL became a standard of the American National Standards Institute (ANSI) in 1986, and of the International Organization for Standardization (ISO) in 1987

- SQL keywords are not case sensitive.
**Operator**
- **LIKE** 
    - find specified pattern **like '%a%'**
    - can use _ represents wildcard **like '_sh_s'**
    - can return if any string is inside **like '[b,s,p]%', like '[a-f]%'
- **(INNER) JOIN:** Returns only rows that have matching values in both tables
- **LEFT (OUTER) JOIN:** Returns all rows from the left table, and only the matched rows from the right table
- **RIGHT (OUTER) JOIN:** Returns all rows from the right table, and only the matched rows from the left table
- **FULL (OUTER) JOIN:** Returns all rows when there is a match in either the left or right table
- **UNION** - operator is used to combine the result-set of two or more SELECT statements.
    - The UNION operator automatically removes duplicate rows from the result set.
    
- **Exist:** is used in where clause to check whether a subquery returns any rows.
- The **ANY** operator is used to compare a value to every value returned by a subquery.
- The **ALL** operator is used to compare a value to every value returned by a subquery.
- The **SELECT INTO** statement is used to create a new table and fill it with data from an existing table.
    - The new table will be created with the same column names and data types as defined in the source table. However, primary keys, indexes, or NOT NULL constraints are not automatically transferred.
- The **INSERT INTO SELECT** statement is used to copy data from an existing table and insert it into another existing table.
    ```sql
    INSERT INTO Customers
    SELECT * FROM Suppliers;
    ```
- The CASE expression is used to define different results based on specified conditions in an SQL statement.
    ```sql
    CASE
      WHEN condition1 THEN result1
      WHEN condition2 THEN result2
      WHEN conditionN THEN resultN
      ELSE default_result
    END;
    ```
- SQL has some built-in functions to handle NULL values, and the most common functions are:

    - **COALESCE(column name, value)** - The preferred standard. (Works in MySQL, SQL Server and Oracle)
    - **IFNULL(column name, value)** - (MySQL)
    - **ISNULL(column name, value)** - (SQL Server) used with IIf(IsNull(column name), value, column name)
- A **stored procedure** is a precompiled SQL code that can be saved and reused.
    - syntax = 
    ```sql
    CREATE PROCEDURE procedure_name
    @param1 datatype,
    @param2 datatype
    AS
    BEGIN
        -- SQL_statements to be executed
        SELECT column1, column2
        FROM table_name
        WHERE columnN = @paramN;
    END;
    ```
    - to execute-
    ``` sql
    exec procedurename @param1 = "value", @param2="value";
    ```
    - for example-
    ```sql
    CREATE PROCEDURE GetCustomersByCity
    @City nvarchar(50)
    AS
    BEGIN
        SELECT * FROM Customers
        WHERE City = @City;
    END;
    ```
    now execute 
    ```sql
    exec GetCustomersByCity @City = 'London';
- **Comments:** 
    - for single line --
    - Multi-line comments start with /* and end with */
- **SQL Bitwise Operators**
    - &	Bitwise AND
    - |	Bitwise OR
    - ^	Bitwise exclusive OR
    - ~	Bitwise NOT
- **SQL Logical Operators**
    - ALL	TRUE if all of the subquery values meet the condition	
    - AND	TRUE if all the conditions separated by AND is TRUE	
    - ANY	TRUE if any of the subquery values meet the condition	
    - BETWEEN	TRUE if the operand is within the range of comparisons	
    - EXISTS	TRUE if the subquery returns one or more records	
    - IN	TRUE if the operand is equal to one of a list of expressions	
    - LIKE	TRUE if the operand matches a pattern	
    - NOT	Displays a record if the condition(s) is NOT TRUE	
    - OR	TRUE if any of the conditions separated by OR is TRUE	
    - SOME	TRUE if any of the subquery values meet the condition

- sql backup database:
    ```sql
    BACKUP DATABASE databasename
    TO DISK = 'filepath'
    with differential ;
    ```
    - A differential backup reduces the backup time (since only the changes are backed up) **OPTIONAL**
-The **CHECK** constraint is used to ensure that the values in a column satisfies a specific condition.
- An **auto_increment** field is a numeric column that automatically generates a unique number, when a new record is inserted into a table.
- **VIEW**
    - An SQL view is a virtual table based on the result-set of an SQL statement. 
    - An SQL view contains rows and columns, just like a real table. 
    - The fields in the view are fields from one or more real tables in the database.
    - syntax
    ```sql
    CREATE VIEW [Brazil Customers] AS
    SELECT CustomerName, ContactName
    FROM Customers
    WHERE Country = 'Brazil';
    ```
    - to run it
    ```sql
    SELECT * FROM [Brazil Customers];
    ```

- MySQL has the following date data types:
    - DATE - format YYYY-MM-DD
    - DATETIME - format: YYYY-MM-DD HH:MI:SS
    - TIMESTAMP - format: YYYY-MM-DD HH:MI:SS
    - TIME - format: HH:MI:SS
    - YEAR - format YYYY or YY

### MySQL String Data Types

| Data Type | Description |
|-----------|-------------|
| `CHAR(size)` | A fixed-length string (letters, numbers, and special characters). `size` specifies the column length in characters (0–255). Default size is `1`. |
| `VARCHAR(size)` | A variable-length string (letters, numbers, and special characters). `size` specifies the maximum column length in characters (0–65,535). |
| `BINARY(size)` | Similar to `CHAR()`, but stores binary byte strings. `size` specifies the column length in bytes. Default size is `1`. |
| `VARBINARY(size)` | Similar to `VARCHAR()`, but stores binary byte strings. `size` specifies the maximum column length in bytes. |
| `BLOB(size)` | A BLOB column with a maximum length of **65,535 bytes**. |
| `TINYBLOB` | A BLOB column with a maximum length of **255 bytes**. |
| `MEDIUMBLOB` | A BLOB column with a maximum length of **16,777,215 bytes**. |
| `LONGBLOB` | A BLOB column with a maximum length of **4,294,967,295 bytes (4 GB)**. |
| `TEXT(size)` | Holds a string with a maximum length of **65,535 bytes**. |
| `TINYTEXT` | A TEXT column with a maximum length of **255 characters**. |
| `MEDIUMTEXT` | A TEXT column with a maximum length of **16,777,215 characters**. |
| `LONGTEXT` | A TEXT column with a maximum length of **4,294,967,295 bytes (4 GB)**. |
| `ENUM(val1, val2, ...)` | A string object that can have **only one value**, chosen from a predefined list (up to **65,535 values**). Invalid values are stored as an empty string. |
| `SET(val1, val2, ...)` | A string object that can have **zero or more values**, chosen from a predefined list (up to **64 values**). |


### MySQL Numeric Data Types

| Data Type | Description |
|-----------|-------------|
| `BIT(size)` | A bit-value type. `size` specifies the number of bits (1–64). Default is `1`. |
| `TINYINT(size)` | A very small integer. Signed: **-128 to 127**. Unsigned: **0 to 255**. |
| `BOOL` | Boolean value. `0` = `FALSE`, non-zero = `TRUE`. |
| `BOOLEAN` | Synonym for `BOOL`. |
| `SMALLINT(size)` | A small integer. Signed: **-32,768 to 32,767**. Unsigned: **0 to 65,535**. |
| `MEDIUMINT(size)` | A medium-sized integer. Signed: **-8,388,608 to 8,388,607**. Unsigned: **0 to 16,777,215**. |
| `INT(size)` | A standard integer. Signed: **-2,147,483,648 to 2,147,483,647**. Unsigned: **0 to 4,294,967,295**. |
| `INTEGER(size)` | Synonym for `INT(size)`. |
| `BIGINT(size)` | A large integer. Signed: **-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807**. Unsigned: **0 to 18,446,744,073,709,551,615**. |
| `DECIMAL(size, d)` | An exact fixed-point number. `size` = total digits (max **65**), `d` = decimal digits (max **30**). Defaults: `size = 10`, `d = 0`. |
| `DEC(size, d)` | Synonym for `DECIMAL(size, d)`. |
| `FLOAT(size, d)` | A small floating-point number. **Deprecated in MySQL 8.0.17** and will be removed in future versions. |
| `FLOAT(p)` | A floating-point number. If `p` is **0–24**, uses `FLOAT`; if `25–53`, uses `DOUBLE`. |
| `DOUBLE(size, d)` | A double-precision floating-point number. Range: approximately **±1.7976931348623157E+308**. |
| `DOUBLE PRECISION(size, d)` | Synonym for `DOUBLE(size, d)`. |

### MySQL String Functions

| Function | Description |
|----------|-------------|
| `ASCII()` | Returns the ASCII value for the specific character. |
| `CHAR_LENGTH()` | Returns the length of a string (in characters). |
| `CHARACTER_LENGTH()` | Returns the length of a string (in characters). |
| `CONCAT()` | Adds two or more expressions together. |
| `CONCAT_WS()` | Adds two or more expressions together with a separator. |
| `FIELD()` | Returns the index position of a value in a list of values. |
| `FIND_IN_SET()` | Returns the position of a string within a list of strings. |
| `FORMAT()` | Formats a number like `#,###,###.##`, rounded to the specified number of decimal places. |
| `INSERT()` | Inserts a string within another string at the specified position and for a certain number of characters. |
| `INSTR()` | Returns the position of the first occurrence of a string in another string. |
| `LCASE()` | Converts a string to lowercase. |
| `LEFT()` | Extracts a specified number of characters from the left side of a string. |
| `LENGTH()` | Returns the length of a string (in bytes). |
| `LOCATE()` | Returns the position of the first occurrence of a substring in a string. |
| `LOWER()` | Converts a string to lowercase. |
| `LPAD()` | Left-pads a string with another string to a specified length. |
| `LTRIM()` | Removes leading spaces from a string. |
| `MID()` | Extracts a substring from a string starting at any position. |
| `POSITION()` | Returns the position of the first occurrence of a substring in a string. |
| `REPEAT()` | Repeats a string the specified number of times. |
| `REPLACE()` | Replaces all occurrences of a substring within a string with a new substring. |
| `REVERSE()` | Reverses a string and returns the result. |
| `RIGHT()` | Extracts a specified number of characters from the right side of a string. |
| `RPAD()` | Right-pads a string with another string to a specified length. |
| `RTRIM()` | Removes trailing spaces from a string. |
| `SPACE()` | Returns a string containing the specified number of space characters. |
| `STRCMP()` | Compares two strings. |
| `SUBSTR()` | Extracts a substring from a string starting at any position. |
| `SUBSTRING()` | Extracts a substring from a string starting at any position. |
| `SUBSTRING_INDEX()` | Returns a substring before a specified number of delimiter occurrences. |
| `TRIM()` | Removes leading and trailing spaces from a string. |
| `UCASE()` | Converts a string to uppercase. |
| `UPPER()` | Converts a string to uppercase. |

### MySQL Numeric Functions

| Function | Description |
|----------|-------------|
| `ABS()` | Returns the absolute value of a number. |
| `ACOS()` | Returns the arc cosine of a number. |
| `ASIN()` | Returns the arc sine of a number. |
| `ATAN()` | Returns the arc tangent of one or two numbers. |
| `ATAN2()` | Returns the arc tangent of two numbers. |
| `AVG()` | Returns the average value of an expression. |
| `CEIL()` | Returns the smallest integer greater than or equal to a number. |
| `CEILING()` | Returns the smallest integer greater than or equal to a number. |
| `COS()` | Returns the cosine of a number. |
| `COT()` | Returns the cotangent of a number. |
| `COUNT()` | Returns the number of records returned by a `SELECT` query. |
| `DEGREES()` | Converts a value in radians to degrees. |
| `DIV` | Performs integer division. |
| `EXP()` | Returns *e* raised to the power of a specified number. |
| `FLOOR()` | Returns the largest integer less than or equal to a number. |
| `GREATEST()` | Returns the greatest value from a list of arguments. |
| `LEAST()` | Returns the smallest value from a list of arguments. |
| `LN()` | Returns the natural logarithm of a number. |
| `LOG()` | Returns the natural logarithm of a number, or the logarithm to a specified base. |
| `LOG10()` | Returns the base-10 logarithm of a number. |
| `LOG2()` | Returns the base-2 logarithm of a number. |
| `MAX()` | Returns the maximum value in a set of values. |
| `MIN()` | Returns the minimum value in a set of values. |
| `MOD()` | Returns the remainder of a division operation. |
| `PI()` | Returns the value of π (Pi). |
| `POW()` | Returns a number raised to the power of another number. |
| `POWER()` | Returns a number raised to the power of another number. |
| `RADIANS()` | Converts degrees into radians. |
| `RAND()` | Returns a random number. |
| `ROUND()` | Rounds a number to a specified number of decimal places. |
| `SIGN()` | Returns the sign of a number. |
| `SIN()` | Returns the sine of a number. |
| `SQRT()` | Returns the square root of a number. |
| `SUM()` | Calculates the sum of a set of values. |
| `TAN()` | Returns the tangent of a number. |
| `TRUNCATE()` | Truncates a number to the specified number of decimal places. |



### MySQL Date Functions

| Function | Description |
|----------|-------------|
| `ADDDATE()` | Adds a time/date interval to a date and returns the result. |
| `ADDTIME()` | Adds a time interval to a time or datetime and returns the result. |
| `CURDATE()` | Returns the current date. |
| `CURRENT_DATE()` | Returns the current date. |
| `CURRENT_TIME()` | Returns the current time. |
| `CURRENT_TIMESTAMP()` | Returns the current date and time. |
| `CURTIME()` | Returns the current time. |
| `DATE()` | Extracts the date part from a datetime expression. |
| `DATEDIFF()` | Returns the number of days between two dates. |
| `DATE_ADD()` | Adds a time/date interval to a date. |
| `DATE_FORMAT()` | Formats a date according to a specified format. |
| `DATE_SUB()` | Subtracts a time/date interval from a date. |
| `DAY()` | Returns the day of the month. |
| `DAYNAME()` | Returns the weekday name. |
| `DAYOFMONTH()` | Returns the day of the month. |
| `DAYOFWEEK()` | Returns the weekday index. |
| `DAYOFYEAR()` | Returns the day of the year. |
| `EXTRACT()` | Extracts a specified part from a date. |
| `FROM_DAYS()` | Returns a date from a numeric day value. |
| `HOUR()` | Returns the hour part of a date/time. |
| `LAST_DAY()` | Returns the last day of the month. |
| `LOCALTIME()` | Returns the current date and time. |
| `LOCALTIMESTAMP()` | Returns the current date and time. |
| `MAKEDATE()` | Creates a date from a year and day-of-year value. |
| `MAKETIME()` | Creates a time from hour, minute, and second values. |
| `MICROSECOND()` | Returns the microsecond part of a time/datetime. |
| `MINUTE()` | Returns the minute part of a time/datetime. |
| `MONTH()` | Returns the month part of a date. |
| `MONTHNAME()` | Returns the month name. |
| `NOW()` | Returns the current date and time. |
| `PERIOD_ADD()` | Adds months to a period. |
| `PERIOD_DIFF()` | Returns the difference between two periods. |
| `QUARTER()` | Returns the quarter of the year. |
| `SECOND()` | Returns the seconds part of a time/datetime. |
| `SEC_TO_TIME()` | Converts seconds into a time value. |
| `STR_TO_DATE()` | Converts a string into a date using a format. |
| `SUBDATE()` | Subtracts a time/date interval from a date. |
| `SUBTIME()` | Subtracts a time interval from a datetime. |
| `SYSDATE()` | Returns the current date and time. |
| `TIME()` | Extracts the time part from a datetime. |
| `TIME_FORMAT()` | Formats a time according to a specified format. |
| `TIME_TO_SEC()` | Converts a time value into seconds. |
| `TIMEDIFF()` | Returns the difference between two time/datetime values. |
| `TIMESTAMP()` | Returns a datetime value based on a date or datetime. |
| `TO_DAYS()` | Returns the number of days since `0000-00-00`. |
| `WEEK()` | Returns the week number of a date. |
| `WEEKDAY()` | Returns the weekday number. |
| `WEEKOFYEAR()` | Returns the week number of the year. |
| `YEAR()` | Returns the year part of a date. |
| `YEARWEEK()` | Returns the year and week number of a date. |



### MySQL Advanced Functions

| Function | Description |
|----------|-------------|
| `BIN()` | Returns the binary representation of a number. |
| `BINARY()` | Converts a value to a binary string. |
| `CASE` | Evaluates conditions and returns the first matching result. |
| `CAST()` | Converts a value to a specified data type. |
| `COALESCE()` | Returns the first non-`NULL` value in a list. |
| `CONNECTION_ID()` | Returns the unique connection ID for the current session. |
| `CONV()` | Converts a number from one numeric base to another. |
| `CONVERT()` | Converts a value to a specified data type or character set. |
| `CURRENT_USER()` | Returns the authenticated MySQL username and host. |
| `DATABASE()` | Returns the name of the current database. |
| `IF()` | Returns one value if a condition is `TRUE`, otherwise another value. |
| `IFNULL()` | Returns a specified value if an expression is `NULL`; otherwise returns the expression. |
| `ISNULL()` | Returns `1` if an expression is `NULL`; otherwise returns `0`. |
| `LAST_INSERT_ID()` | Returns the `AUTO_INCREMENT` ID of the last inserted row. |
| `NULLIF()` | Returns `NULL` if two expressions are equal; otherwise returns the first expression. |
| `SESSION_USER()` | Returns the current MySQL username and host. |
| `SYSTEM_USER()` | Returns the current MySQL username and host. |
| `USER()` | Returns the current MySQL username and host. |
| `VERSION()` | Returns the current MySQL server version. |

