The following functions are supported for enum types:

| **Function**                     | **Description**                                                     |
| ---------------------------- | ------------------------------------------------------------ |
| enum_first(anyenum)          | Returns the first value of the input enum type                                   |
| enum_last(anyenum)           | Returns the last value of the input enum type                                 |
| enum_range(anyenum)          | Returns all values of the input enum type in an ordered array                 |
| enum_range(anyenum, anyenum) | Returns the range between the two given enum values, as an ordered array. The values must be from the same enum type. If the first parameter is null, the result will start with the first value of the enum type. If the second parameter is null, the result will end with the last value of the enum type |

Sample code:
```
postgres=# CREATE TYPE rainbow AS ENUM ('red', 'orange', 'yellow', 'green', 'blue', 'purple');
CREATE TYPE
postgres=# SELECT enum_first(null::rainbow);
enum_first
------------
 red
(1 row)
 
postgres=# SELECT enum_last(null::rainbow);
 enum_last 
-----------
 purple
(1 row)

postgres=# SELECT enum_range(null::rainbow);
       enum_range        
---------------------------------------
 {red,orange,yellow,green,blue,purple}
(1 row)
 
postgres=# SELECT enum_range('orange'::rainbow, 'green'::rainbow);
   enum_range    
-----------------------
 {orange,yellow,green}
(1 row)

postgres=# SELECT enum_range(NULL, 'green'::rainbow);
    enum_range     
---------------------------
 {red,orange,yellow,green}
(1 row)
 
postgres=# SELECT enum_range('orange'::rainbow, NULL);
      enum_range       
-----------------------------------
 {orange,yellow,green,blue,purple}
(1 row)
```
