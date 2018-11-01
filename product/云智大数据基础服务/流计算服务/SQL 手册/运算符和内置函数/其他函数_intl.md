### Mapping Function
The function names and descriptions of Mapping functions are as follows:

| Function Name | Feature Description |
| ----- | ----- |
| CARDINALITY(map)	| Returns the total number of items in a mapping. |
| map '[' key ']'	| Returns the value corresponding to the key of Map. |

### Hash Function
The names and feature descriptions of hash functions are as follows:

| Function Name | Feature Description |
| ----- | ----- |
| MD5(string)	| Returns the MD5 value (a string of 32-bit hexadecimal digits) of a string. Returns NULL if NULL is entered. |
| SHA1(string)	| Returns the SHA1 value (a string of 40-bit hexadecimal digits) of a string. Returns NULL if NULL is entered. |
| SHA256(string)	| Returns the SHA256 value (a string of 64-bit hexadecimal digits) of a string. Returns NULL if NULL is entered. |

### Value Access Functions
The names and feature descriptions of value access functions are as follows:

| Function Name | Feature Description |
| ----- | ----- |
| tableName.compositeType.field	| Accesses fields of compound types (Tuple and POJO). |
| tableName.compositeType.\*	| Accesses all fields of Tuple or POJO. |

### Value Constructor
The names and feature descriptions of value constructors are as follows:

| Function Name | Feature Description |
| ----- | ----- |
| (value, [, value]\*)	| Creates a row containing several values. |
| ROW(value, [, value]\*)	| Creates a row containing several values. |
| ARRAY '[' value [, value ]\* ']'	| Creates an array that contains several values. |
| MAP '[' key, value [, key, value ]\* ']'	| Creates a mapping that contains several key-value pairs. |

### Array Function
The names and feature descriptions of array functions are as follows:

| Function Name | Feature Description |
| ----- | ----- |
| CARDINALITY(array)	| Returns the length of an array. |
| array '[' index ']'	| Returns the item at the specified position of an array (subscript starts with 1). |
| ELEMENT(array)	| Returns the content of a single-element array (returns NULL if the array is empty; throws an exception if the array has more than one element).|

