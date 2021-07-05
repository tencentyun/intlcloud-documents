## Array Operators
TDSQL-A for PostgreSQL supports the following operators for array types:

| **Operator** | **Description**       | **Example**                                 | **Result**                  |
| ---------- | -------------- | ---------------------------------------- | ------------------------- |
| =          | Equal to           | ARRAY[1.1,2.1,3.1]::int[] = ARRAY[1,2,3] | t                         |
| <>         | Not equal to         | ARRAY[1,2,3] <> ARRAY[1,2,4]             | t                         |
| <          | Less than           | ARRAY[1,2,3] < ARRAY[1,2,4]              | t                         |
| >          | Greater than           | ARRAY[1,4,3] > ARRAY[1,2,4]              | t                         |
| <=         | Less than or equal to       | ARRAY[1,2,3] <= ARRAY[1,2,3]             | t                         |
| >=         | Greater than or equal to       | ARRAY[1,4,3]>=ARRAY[1,4,3]               | t                         |
| @>         | Contains           | ARRAY[1,4,3] @> ARRAY[3,1]               | t                         |
| <@         | Is contained by         | ARRAY[2,7] <@ ARRAY[1,7,4,2,6]           | t                         |
| &&         | Overlaps           | ARRAY[1,4,3] && ARRAY[2,1]               | t                         |
| \|\|       | Array-to-Array concatenation | ARRAY[1,2,3] \|\| ARRAY[4,5,6]           | {1,2,3,4,5,6}             |
| \|\|       | Array-to-Array concatenation | ARRAY[1,2,3]\|\|ARRAY[[4,5,6],[7,8,9]]   | {{1,2,3},{4,5,6},{7,8,9}} |
| \|\|       | Element-to-Array concatenation | 3 \|\| ARRAY[4,5,6]                      | {3,4,5,6}                 |
| \|\|       | Array-to-Element concatenation | ARRAY[4,5,6] \|\| 7                      | {4,5,6,7}                 |


## Array Functions
| **Function**                        | **Return Type** | **Description**                                                     |
| --------------------------- | ------------ | -------------------------------------- |
| array_append(anyarray,  anyelement)                 | anyarray     | Appends an element to the end of an array                                 |
| array_cat(anyarray,  anyarray)                      | anyarray     | Concatenates two arrays                                                 |
| array_ndims(anyarray)                               | int          | Returns the number of dimensions of the array                                             |
| array_length(anyarray,  int)                        | int          | Returns the length of the requested array dimension                                   |
| array_lower(anyarray,  int)                         | int          | Returns the lower bound of the requested array dimension                                   |
| array_position(anyarray,  anyelement [, int])       | int          | Returns the subscript of the first occurrence of the second argument in the array, starting at the element indicated by the third argument or at the first element (array must be one-dimensional) |
| array_prepend(anyelement,  anyarray)                | anyarray     | Appends an element to the beginning of an array                 |
| array_remove(anyarray,  anyelement)                 | anyarray     | Removes all elements equal to the given value from the array (array must be one-dimensional)     |
| array_replace(anyarray,   anyelement,   anyelement) | anyarray  | Replaces each array element equal to the given value with a new value      |
| array_to_string(  anyarray,   text [, text])        | text         | Concatenates array elements by using supplied delimiter and optional null string                     |
| array_upper(anyarray,  int)                   | int          | Returns the upper bound of the requested array dimension                                   |
| string_to_array(text,   text [, text])         | text[]       | Splits string into array elements by using supplied delimiter and optional null string           |

Sample code:
```
postgres=# SELECT array_append(ARRAY[1,2], 3);
 array_append 
--------------
 {1,2,3}
(1 row) 

postgres=# SELECT array_cat(ARRAY[1,2,3], ARRAY[4,5]);
 array_cat 
-------------
 {1,2,3,4,5}
(1 row) 

postgres=# SELECT array_ndims(ARRAY[[1,2,3], [4,5,6]]);
 array_ndims 
-------------
      2
(1 row) 

postgres=# SELECT array_length(array[1,2,3], 1);
 array_length 
--------------
      3
(1 row) 

postgres=# SELECT array_lower('[0:2]={1,2,3}'::int[], 1);
 array_lower 
-------------
      0
(1 row) 

postgres=# SELECT array_position(ARRAY['sun','mon','tue','wed','thu','fri','sat'], 'mon');
 array_position 
----------------
       2
(1 row) 

postgres=# SELECT array_prepend(1, ARRAY[2,3]);
 array_prepend 
---------------
 {1,2,3}
(1 row)
 
postgres=# SELECT array_remove(ARRAY[1,2,3,2], 2);
 array_remove 
--------------
 {1,3}
(1 row) 

postgres=# SELECT array_replace(ARRAY[1,2,5,4], 5, 3);
 array_replace 
---------------
 {1,2,3,4}
(1 row)

postgres=# SELECT array_to_string(ARRAY[1, 2, 3, NULL, 5], ',', '*');
 array_to_string 
-----------------
 1,2,3,*,5
(1 row) 

postgres=# SELECT array_upper(ARRAY[1,8,3,7], 1);
 array_upper 
-------------
      4
(1 row)

postgres=# SELECT string_to_array('xx~^~yy~^~zz', '~^~', 'yy');
 string_to_array 
-----------------
 {xx,NULL,zz}
(1 row)
```
Above are some common array functions. For more information, please see [Array Functions and Operators](http://www.postgres.cn/docs/10/functions-array.html).
