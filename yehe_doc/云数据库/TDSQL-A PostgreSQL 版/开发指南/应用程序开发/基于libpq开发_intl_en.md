libpq is the C application programmer's API to TDSQL-A for PostgreSQL. libpq is a set of library functions that allow client programs to pass queries to the TDSQL-A for PostgreSQL backend server and to receive the results of these queries.

libpq is also the underlying engine for several other TDSQL-A for PostgreSQL APIs, including those written for C++, Perl, Python, Tcl, and ECPG.

Client programs that use libpq must include the header file `libpq-fe.h` and must link with the libpq library.

## Sample Code
### Sample 1: connecting to database
1. Create the `conn_test.cpp` file.
```
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"  
int
main(int argc, char **argv){
  const char *conninfo;
  PGconn   *conn;   
  if (argc > 1){
    conninfo = argv[1];
  }else{
    conninfo = "dbname = postgres"; 
  }      
  conn = PQconnectdb(conninfo);
  if (PQstatus(conn) != CONNECTION_OK){
    fprintf(stderr, "Database connection failed: %s",PQerrorMessage(conn));       
  }else{
    printf("Database connection succeeded\n");
  }
  PQfinish(conn);
  return 0;
}
```
2. Compile the code.
```
gcc -c -I ~/user_1/tdata_02/tbase_v3_1/3.0.16/install/tbase_pgxz/include conn_test.cpp
```
3. Link the complied file to form an executable file.
```
gcc -o conn conn_test.o -L ~/user_1/tdata_02/tbase_v3_1/3.0.16/install/tbase_pgxz/lib/ -lpq
```
4. Test the database connection.
```
./conn "host=localhost dbname=postgres port=11345"
```
Database connection succeeded!

### Sample 2: creating table
1. Create the `createtable.c` file.
```
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"  
int
main(int argc, char **argv){
  const char *conninfo;
  PGconn   *conn;   
  PGresult  *res;
  const char *sql = "create table tdapg(id int,nickname text) ";
  if (argc > 1){
    conninfo = argv[1];
  }else{
    conninfo = "dbname = postgres";      
  }    
  conn = PQconnectdb(conninfo);
  if (PQstatus(conn) != CONNECTION_OK){
    fprintf(stderr, "Database connection failed: %s",PQerrorMessage(conn));       
  }else{
    printf("Database connection succeeded\n");
  }
  res = PQexec(conn,sql);
  if(PQresultStatus(res) != PGRES_COMMAND_OK){
    fprintf(stderr, "Table creation failed: %s",PQresultErrorMessage(res)); 
  }else{
    printf("Table creation succeeded\n");
  }
  PQclear(res);
  PQfinish(conn);
  return 0;
}
```
2. Compile the code.
```
gcc -c -I ~/user_1/tdata_02/tbase_v3_1/3.0.16/install/tbase_pgxz/include createtable .cpp
```
3. Link the complied file to form an executable file.
```
gcc -o createtable createtable.o -L ~/user_1/tdata_02/tbase_v3_1/3.0.16/install/tbase_pgxz/lib/ -lpq
```
4. Test the database connection.
```
./createtable "host=localhost dbname=postgres port=11345"
```
![](https://main.qcloudimg.com/raw/bb0cb159049e78d02dded8f3b8803007.png)
 
### Sample 3: inserting data
1. Create the `insert.c` file.
```
#include <stdio.h>
#include <stdlib.h>
#include "libpq-fe.h"  
int
main(int argc, char **argv){
  const char *conninfo;
  PGconn   *conn;   
  PGresult  *res;
  const char *sql = "INSERT INTO tdapg (id,nickname) values(1,'tdapg'),(2,'pgxz')";
  if (argc > 1){
    conninfo = argv[1];
  }else{
    conninfo = "dbname = postgres";      
  }    
  conn = PQconnectdb(conninfo);
  if (PQstatus(conn) != CONNECTION_OK){
    fprintf(stderr, "Database connection failed: %s",PQerrorMessage(conn));       
  }else{
    printf("Database connection succeeded\n");
  }
  res = PQexec(conn,sql);
  if(PQresultStatus(res) != PGRES_COMMAND_OK){
    fprintf(stderr, "Data insertion failed: %s",PQresultErrorMessage(res)); 
  }else{
    printf("Data insertion succeeded\n");
  }
  PQclear(res);
  PQfinish(conn);
  return 0;
}
```
2. Compile the code.
```
gcc -c -I ~/user_1/tdata_02/tbase_v3_1/3.0.16/install/tbase_pgxz/include insert.cpp
```
3. Link the complied file to form an executable file.
```
gcc -o insert insert.o -L ~/user_1/tdata_02/tbase_v3_1/3.0.16/install/tbase_pgxz/lib/ -lpq
```
4. Test the database connection.
```
./insert "host=localhost dbname=postgres port=11345"
```
![](https://main.qcloudimg.com/raw/4e80c5f4712cb438933d6ac6b587927c.png)
 
### Sample 4: querying data
1. Create the `select.c` file.
```
#include <stdlib.h>
#include "libpq-fe.h"
int
main(int argc, char **argv){
  const char *conninfo;
  PGconn   *conn;
  PGresult  *res;
  const char *sql = "select * from tdapg";
  if (argc > 1){
    conninfo = argv[1];
  }else{
    conninfo = "dbname = postgres";
  }
  conn = PQconnectdb(conninfo);
  if (PQstatus(conn) != CONNECTION_OK){
    fprintf(stderr, "Database connection failed: %s",PQerrorMessage(conn));
   }else{
    printf("Database connection succeeded\n");
  }
  res = PQexec(conn,sql);
  if(PQresultStatus(res) != PGRES_TUPLES_OK){
    fprintf(stderr, "Data insertion failed: %s",PQresultErrorMessage(res));
  }else{
    printf("Data query succeeded\n");
    int rownum = PQntuples(res) ;
    int colnum = PQnfields(res);
    for(int j = 0;j< colnum; ++j){
      printf("%s\t",PQfname(res,j));
    }
    printf("\n");
    for(int i = 0;i< rownum; ++i){
      for(int j = 0;j< colnum; ++j){
        printf("%s\t",PQgetvalue(res,i,j));
      }
      printf("\n");
    }
  }
  PQclear(res);
  PQfinish(conn);
  return 0;
}
```
2. Compile the code.
```
gcc -std=c99 -c -I ~/user_1/tdata_02/tbase_v3_1/3.0.16/install/tbase_pgxz/include select.c
```
3. Link the complied file to form an executable file.
```
gcc -o select select.o -L ~/user_1/tdata_02/tbase_v3_1/3.0.16/install/tbase_pgxz/lib/ -lpq
```
4. Test the database connection.
```
./select"host=localhost dbname=postgres port=11345"
```
![](https://main.qcloudimg.com/raw/73ffdf332b1e6ac6a2521c0eb224f82a.png)
