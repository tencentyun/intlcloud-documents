You can use the pgx API of Go to connect to a TDSQL-A for PostgreSQL database for data exchange. The resource package required by development is available [here](https://github.com/jackc/pgx).

## Sample 1. Connecting to Database
```
package main
import (
"fmt"
"time"
"github.com/jackc/pgx"
)
func main() {
var error_msg string
// Connect to the database
conn, err := db_connect()
if err != nil {
error_msg = "Database connection failed. Details:" + err.Error()
write_log("Error", error_msg)
return
}/
/ Close the connection when the program finishes running
defer conn.Close()
write_log("Log", "Database connection succeeded")
}
/*
Feature description: processing write log
Parameter description:
log_level: log level, which can be `Error` or `Log` only
error_msg: log content
Returned value description: none
*/
func write_log(log_level string, error_msg string) {
// Print the error message
fmt.Println("Access time:", time.Now().Format("2006-01-02 15:04:05"))
fmt.Println("Log level:", log_level)
fmt.Println("Details:", error_msg)
}
/*
Feature description: connecting to database
Parameter description: none
Returned value description:
conn *pgx.Conn: connection information
err error: error message
*/
func db_connect() (conn *pgx.Conn, err error) {
var config pgx.ConnConfig
config.Host = "127.0.0.1" // Database host or IP
config.User = "dbadmin" // Connected user
config.Password = "pgsql" // User password
config.Database = "postgres" // Name of the connected database
config.Port = 15432 // Port number
conn, err = pgx.Connect(config)
return conn, err
}
```

## Sample 2. Creating Table
```
package main
import (
"fmt"
"time"
"github.com/jackc/pgx"
)
func main() {
var error_msg string
var sql string
// Connect to the database
conn, err := db_connect()
if err != nil {
error_msg = "Database connection failed. Details:" + err.Error()
write_log("Error", error_msg)
return
}/
/ Close the connection when the program finishes running
defer conn.Close()
write_log("Log", "Database connection succeeded")
// Create a table
sql = "create table public.tdapg(id varchar(20),nickname varchar(100))
distribute by shard(id) to group default_group;"
_, err = conn.Exec(sql)
if err != nil {
error_msg = "Table creation failed. Details:" + err.Error()
write_log("Error", error_msg)
return
} else {
write_log("Log", "Table creation succeeded")
}
}
/*
Feature description: processing write log
*/
func write_log(log_level string, error_msg string) {
// Print the error message
fmt.Println("Access time:", time.Now().Format("2006-01-02 15:04:05"))
fmt.Println("Log level:", log_level)
fmt.Println("Details:", error_msg)
}
/*
Feature description: connecting to database
*/
func db_connect() (conn *pgx.Conn, err error) {
var config pgx.ConnConfig
config.Host = "127.0.0.1" // Database host or IP
config.User = "dbadmin" // Connected user
config.Password = "pgsql" // User password
config.Database = "postgres" // Name of the connected database
config.Port = 15432 // Port number
conn, err = pgx.Connect(config)
return conn, err
}
```

## Sample 3. Inserting Data
```
package main
import (
"fmt"
"strings"
"time"
"github.com/jackc/pgx"
)
func main() {
var error_msg string
var sql string
var nickname string
// Connect to the database
conn, err := db_connect()
if err != nil {
error_msg = "Database connection failed. Details:" + err.Error()
write_log("Error", error_msg)
return
}/
/ Close the connection when the program finishes running
defer conn.Close()
write_log("Log", "Database connection succeeded")
// Insert data
sql = "insert into public.tdapg values('1','tdapg'),('2','pgxz');"
_, err = conn.Exec(sql)
if err != nil {
error_msg = "Data insertion failed. Details:" + err.Error()
write_log("Error", error_msg)
return
} else {
write_log("Log", "Data insertion succeeded")
}
// Insert data in the form of binding variables without injection prevention required
sql = "insert into public.tdapg values($1,$2),($1,$3);"
_, err = conn.Exec(sql, "3", "postgresql", "postgres")
if err != nil {
error_msg = "Data insertion failed. Details:" + err.Error()
write_log("Error", error_msg)
return
} else {
write_log("Log", "Data insertion succeeded")
}
// Insert data in the form of concatenating SQL statements with injection prevention required
nickname = "Tdapg is ' good!"
sql = "insert into public.tdapg values('1','" + sql_data_encode(nickname) + "')"
_, err = conn.Exec(sql)
if err != nil {
error_msg = "Data insertion failed. Details:" + err.Error()
write_log("Error", error_msg)
return
} else {
write_log("Log", "Data insertion succeeded")
}
}
func sql_data_encode(str string) string {
return strings.Replace(str, "'", "''", -1)
}
/*
Feature description: processing write log
Parameter description:
log_level: log level, which can be `Error` or `Log` only
error_msg: log content
Returned value description: none
*/
func write_log(log_level string, error_msg string) {
// Print the error message
fmt.Println("Access time:", time.Now().Format("2006-01-02 15:04:05"))
fmt.Println("Log level:", log_level)
fmt.Println("Details:", error_msg)
}
/*
Feature description: connecting to database
Parameter description: none
Returned value description:
conn *pgx.Conn: connection information
err error: error message
*/
func db_connect() (conn *pgx.Conn, err error) {
var config pgx.ConnConfig
config.Host = "127.0.0.1" // Database host or IP
config.User = "dbadmin" // Connected user
config.Password = "pgsql" // User password
config.Database = "postgres" // Name of the connected database
config.Port = 15432 // Port number
conn, err = pgx.Connect(config)
return conn, err
}
```

## Sample 4. Querying Data
```
package main
import (
"fmt"
"strings"
"time"
"github.com/jackc/pgx"
)
func main() {
var error_msg string
var sql string
// Connect to the database
conn, err := db_connect()
if err != nil {
error_msg = "Database connection failed. Details:" + err.Error()
write_log("Error", error_msg)
return
}/
/ Close the connection when the program finishes running
defer conn.Close()
write_log("Log", "Database connection succeeded")
sql = "SELECT id,nickname FROM public.tdapg LIMIT 2"
rows, err := conn.Query(sql)
if err != nil {
error_msg = "Data query failed. Details:" + err.Error()
write_log("Error", error_msg)
return
} else {
write_log("Log", "Data query succeeded")
}
var nickname string
var id string
for rows.Next() {
err = rows.Scan(&id, &nickname)
if err != nil {
error_msg = "Query execution failed. Details:" + err.Error()
write_log("Error", error_msg)
return
}error_msg = fmt.Sprintf("id:%s nickname:%s", id, nickname)
write_log("Log", error_msg)
}rows.Close()
nickname = "tdapg"
sql = "SELECT id,nickname FROM public.tdapg WHERE nickname ='" +
sql_data_encode(nickname) + "' "
rows, err = conn.Query(sql)
if err != nil {
error_msg = "Data query failed. Details:" + err.Error()
write_log("Error", error_msg)
return
} else {
write_log("Log", "Data query succeeded")
}defer rows.Close()
for rows.Next() {
err = rows.Scan(&id, &nickname)
if err != nil {
error_msg = "Query execution failed. Details:" + err.Error()
write_log("Error", error_msg)
return
}error_msg = fmt.Sprintf("id:%s nickname:%s", id, nickname)
write_log("Log", error_msg)
}
}
/*
Feature description: encoding concatenated string for SQL query
Parameter description:
str: string to be encoded
Returned value description:
Encoded string
*/
func sql_data_encode(str string) string {
return strings.Replace(str, "'", "''", -1)
}
/*
Feature description: processing write log
Parameter description:
log_level: log level, which can be `Error` or `Log` only
error_msg: log content
Returned value description: none
*/
func write_log(log_level string, error_msg string) {
// Print the error message
fmt.Println("Access time:", time.Now().Format("2006-01-02 15:04:05"))
fmt.Println("Log level:", log_level)
fmt.Println("Details:", error_msg)
}
/*
Feature description: connecting to database
Parameter description: none
Returned value description:
conn *pgx.Conn: connection information
err error: error message
*/
func db_connect() (conn *pgx.Conn, err error) {
var config pgx.ConnConfig
config.Host = "127.0.0.1" // Database host or IP
config.User = "dbadmin" // Connected user
config.Password = "pgsql" // User password
config.Database = "postgres" // Name of the connected database
config.Port = 15432 // Port number
conn, err = pgx.Connect(config)
return conn, err
}
```

## Sample 5. Inserting Copied Data
```
package main
import (
"fmt"
"math/rand"
"time"
"github.com/jackc/pgx"
)
func main() {
var error_msg string
// Connect to the database
conn, err := db_connect()
if err != nil {
error_msg = "Database connection failed. Details:" + err.Error()
write_log("Error", error_msg)
return
}/
/ Close the connection when the program finishes running
defer conn.Close()
write_log("Log", "Database connection succeeded")
// Construct 5,000 rows of data
inputRows := [][]interface{}{}
var id string
var nickname string
for i := 0; i < 5000; i++ {
id = fmt.Sprintf("%d", rand.Intn(10000))
nickname = fmt.Sprintf("%d", rand.Intn(10000))
inputRows = append(inputRows, []interface{}{id, nickname})
}copyCount, err := conn.CopyFrom(pgx.Identifier{"dbadmin"}, []string{"id",
"nickname"}, pgx.CopyFromRows(inputRows))
if err != nil {
error_msg = "copyFrom execution failed. Details:" + err.Error()
write_log("Error", error_msg)
return
}if copyCount != len(inputRows) {
error_msg = fmt.Sprintf("copyFrom execution failed. Number of copied rows: %d. Number of returned rows: %d",
len(inputRows), copyCount)
write_log("Error", error_msg)
return
} else {
error_msg = "Record copying succeeded"
write_log("Log", error_msg)
}
}
/*
Feature description: processing write log
Parameter description:
log_level: log level, which can be `Error` or `Log` only
error_msg: log content
Returned value description: none
*/
func write_log(log_level string, error_msg string) {
// Print the error message
fmt.Println("Access time:", time.Now().Format("2006-01-02 15:04:05"))
fmt.Println("Log level:", log_level)
fmt.Println("Details:", error_msg)
}
/*
Feature description: connecting to database
Parameter description: none
Returned value description:
conn *pgx.Conn: connection information
err error: error message
*/
func db_connect() (conn *pgx.Conn, err error) {
var config pgx.ConnConfig
config.Host = "127.0.0.1" // Database host or IP
config.User = "dbadmin" // Connected user
config.Password = "pgsql" // User password
config.Database = "postgres" // Name of the connected database
config.Port = 15432 // Port number
conn, err = pgx.Connect(config)
return conn, err
}
```
