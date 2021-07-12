`CREATE FUNCTION` defines a new function. `CREATE OR REPLACE FUNCTION` will either create a new function or replace an existing definition. To be able to define a function, you must have the `USAGE` permission on the language. The name of the new function must not match any existing function or procedure with the same input argument types in the same schema. However, functions and procedures of different argument types can share a name (this is called overloading).

## Functions for PL/pgSQL
PL/pgSQL is a loadable procedural language similar to PL/SQL for Oracle.
Functions created with PL/pgSQL can be used anywhere that built-in functions can be used. SQL is the language most databases use as query language. It's portable and easy to learn. However, every SQL statement must be executed individually by the database server. This means that your client application must send each query to the database server, wait for it to be processed, receive and process the results, do some computation, and then send further queries to the server. All this incurs interprocess communication and will also incur network overhead if your client is on a different machine than the database server.

With PL/pgSQL, you can group a block of computation and a series of queries inside the database server, thus having the power of a procedural language and the ease of use of SQL, but with considerable savings of client/server communication overhead.
- Extra round trips between client and server are eliminated.
- Intermediate results that the client does not need do not have to be marshaled or transferred between server and client.
- Multiple rounds of query parsing can be avoided.

Also, with PL/pgSQL, you can use all the data types, operators, and functions of SQL. Their application methods are similar to those of stored procedures, and the only difference lies in that stored procedures do not have returned values, but functions have.
Sample code:
```
CREATE FUNCTION one() RETURNS integer AS $$
SELECT 1 AS result;
$$ LANGUAGE SQL;
Directly use `SELECT` to call the function:
SELECT one();
```

## Functions for C/C++
User-Defined functions can be written in C/C++. Such functions are compiled into shared libraries (i.e., .so library files) and uploaded to the server before creation. The dynamic loading feature is what distinguishes "C language" functions from "internal" functions - the actual coding conventions are essentially the same for both.

### Writing code
The basic rules for writing and compiling C functions are as follows:
When allocating memory, use functions `palloc` and `pfree` instead of the corresponding C library functions `malloc` and `free`. The memory allocated by `palloc` will be released automatically at the end of each transaction, preventing memory leaks.
Most of the internal TDSQL-A for PostgreSQL types are declared in `postgres.h`, while the function manager interfaces are in `fmgr.h`, so you will need to include at least these two files. For portability reasons, it's best to include `postgres.h` and `fmgr.h` first before any other system or user header files.

Symbol names defined within object files must not conflict with those defined in the original database and operating system executable.
For example:
```
extern "C"{
#include "postgres.h"
#include "fmgr.h"
 
PG_MODULE_MAGIC;
}
// Addition
extern "C"{
PG_FUNCTION_INFO_V1(my_add_func);
Datum my_add_func(PG_FUNCTION_ARGS)
 {
 int32 a = PG_GETARG_INT32(0);
 int32 b = PG_GETARG_INT32(1);
 int64 result = a + b;
 PG_RETURN_INT64(result);
 }
}
```

### Compiling and loading user-defined function
1. Compile:
```
gcc -Wall -Werror -g3 -o my_func.o -fPIC -c my_func.cpp -I/data/tbase/user_1/tdata_02/tbase_v3_1/3.0.16/install/tbase_pgxz/include/postgresql/server/
```
2. Generate the .so library file:
```
gcc -shared -o my_func.so my_func.o
```
3. Send the library file to each DN and CN and grant permissions of the corresponding role to the database user for function creation:
```
create function my_add_func(a integer,b integer) RETURNS integer
as '/data/tbase/my_func.so' ,'my_add_func' language c strict;
CREATE FUNCTION
Use the function for query:
v3=# select my_add_func(1,2);
 my_add_func
\-------------
 3
(1 row)
```

## Functions for PL/Python
Before using PL/Python functions in TDSQL-A for PostgreSQL, you need to create the `plpythonu` extension in advance:
```
create extension plpythonu;
```

### Syntax declaration
Functions in PL/Python are declared via the standard [CREATE FUNCTION](http://postgres.cn/docs/10/sql-createfunction.html) syntax:
```
CREATE FUNCTION funcname (argument-list)
 RETURNS return-type
AS $$
 \# PL/Python function body
$$ LANGUAGE plpythonu;
```
The body of a function is simply a Python script. When the function is called, its arguments are passed as elements of the list `args`; named arguments are also passed as ordinary variables to the Python script. Use of named arguments is usually more readable. The result is returned from the Python code in the usual way, with `return` or `yield` (in case of a result-set statement). If you do not provide a returned value, Python returns the default `None`. PL/Python translates Python's `None` into the SQL null value.
For example, a function to return the greater of two integers can be defined as:
```
CREATE FUNCTION pymax (a integer, b integer)
 RETURNS integer
AS $$
 if a > b:
  return a
 return b
$$ LANGUAGE plpythonu;
```

The Python code that is given as the body of the function definition is transformed into a Python function. For example, the above results in:
```
def __plpython_procedure_pymax_23456():
 if a > b:
  return a
 return b
```

### Variable range
The arguments are set as global variables. Because of the scoping rules of Python, this has the subtle consequence that an argument variable cannot be reassigned inside the function to the value of an expression that involves the variable name itself, unless the variable is redeclared as global in the block. For example, the following won't work:
```
CREATE FUNCTION pystrip(x text)
 RETURNS text
AS $$
 x = x.strip() # error
 return x
$$ LANGUAGE plpythonu;
```

This is because assigning to `x` makes `x` a local variable for the entire block, and so the `x` on the right-hand side of the assignment refers to a not-yet-assigned local variable `x`, not the PL/Python function parameter. Using the `global` statement, this can be made to work:
```
CREATE FUNCTION pystrip(x text)
 RETURNS text
AS $$
 global x
 x = x.strip() # OK now
 return x
$$ LANGUAGE plpythonu;
```
However, it is advisable not to rely on this implementation detail of PL/Python. It is better to treat the function parameters as read-only.
