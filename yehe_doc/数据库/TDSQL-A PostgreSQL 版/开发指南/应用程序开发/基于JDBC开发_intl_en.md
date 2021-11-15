## JDBC Driver Package
You can get the driver package from the [JDBC official website](https://jdbc.postgresql.org/) or the software provider.

## Driver Class
Before creating a database connection in the code, you need to load the database driver class `org.postgresql.Driver`.

## Connection Parameters
When using JDBC to connect to a database, you can use a URL to specify the database to be connected in one of the following formats:
```
jdbc:postgresql:database
jdbc:postgresql://host/database
jdbc:postgresql://host:port/database
```
Parameter description:
- host: server host name, which is `localhost` by default. To specify an IPv6 address, you must enclose `host` in square brackets "[]", for example, `Jdbc:postgresql:// 127.0.0.1:5740/accounting`.
- port: port number that the server is listening on.
- database: database name.
In addition to the standard connection parameters, the driver also supports many other properties, which can be used to specify behavior specific to other drivers. These properties can be specified in the `Properties` object parameter of `DriverManager.getConnection` or in the URL.
- user: database user creating the connection, which is in string type.
- password: database user password, which is in string type.
- ssl: specifies whether SSL connection is used, which is in Boolean type.
- loggerLevel: sets the log level and information volume for `LogStream` or `LogWriter`, which is in string type. Currently, `OFF`, `DEBUG`, and `TRACE` are supported. 
   - `DEBUG` indicates that only logs at the `DEBUG` or higher level are printed, generating a little log information.
   - `TRACE` indicates that logs at the `DEBUG` and `TRACE` levels are printed, generating detailed log information. The default value is `OFF`, indicating not to print logs.
- prepareThreshold: number of `PreparedStatement` execution times required before SQL statements converted to prepared statements on the server, which is in integer type. The default value is 5.
- batchMode: specifies whether to connect to the database in `batch` mode, which is in Boolean type.
- Fetchsize: default `fetchsize` for statements created by the database connection, which is in integer type.
- ApplicationName: application name, which is in string type. The default value is `PostgreSQL JDBC Driver` if this parameter is left empty.
- allowReadOnly: specifies whether to enable the `readonly` mode for the connection, which is in Boolean type. The default value is `false`. If this value is not changed to `true`, the execution of `connection.setReadOnly` will not work.
- blobMode: sets the data type to which the `setBinaryStream` method assigns values, which is in string type. The value `on` indicates that values are assigned to the `BLOB` data type, and `off` the `bytea` data type. The default value is `on`.
- connectionExtraInfo: specifies whether the JDBC driver reports the current driver deployment path and process owner to the database, which is in Boolean type.

Sample code:
```
public static Connection GetConnection(String username, String passwd)
  {
    // Driver class
    String driver = "org.postgresql.Driver";
    // Database connection descriptor
    String sourceURL = "jdbc:postgresql://10.10.0.13:11345/tdapg";
    Connection conn = null;
      try
    {
      // Load the driver
      Class.forName(driver);
    }
    catch( Exception e )
    {
      e.printStackTrace();
      return null;
    }
    try
    {
       // Create a connection
      conn = DriverManager.getConnection(sourceURL, username, passwd);
      System.out.println("Connection succeed!");
    }
    catch(Exception e)
    {
      e.printStackTrace();
      return null;
    }
    return conn;
};
```

## Sample Code
Java connection demos for database connection, table creation, batch insertion, update, etc.:
```
package Demo;
import java.sql.*;
public class tdapg_Conn {
 public static Connection GetConnection(String username, String passwd) {
  String driver = "org.postgresql.Driver";
  String sourceURL = "jdbc:postgresql://100.1.1.1:11345/v3";
  Connection conn = null;
  try {
   Class.forName(driver).newInstance();
  } catch (Exception e) {
   e.printStackTrace();
   return null;
  }
  try {
   conn = DriverManager.getConnection(sourceURL, username, passwd);
   System.out.println("Connection succeed!");
  } catch (Exception e) {
   e.printStackTrace();
   return null;
  }
  return conn;
 };
 public static void CreateTable(Connection conn) {
  Statement stmt = null;
  try {
   stmt = conn.createStatement();
   int rc = stmt.executeUpdate("CREATE TABLE user_table(user_id INTEGER, user_name VARCHAR(32));");
   stmt.close();
   System.out.println("TABLE customer_t1 create Successful!");
  } catch (SQLException e) {
   if (stmt != null) {
    try {
     stmt.close();
    } catch (SQLException e1) {
     e1.printStackTrace();
    }
   }
   e.printStackTrace();
  }
 }
 

public static void BatchInsertData(Connection conn) {
 PreparedStatement pst = null;
 try {
   pst = conn.prepareStatement("INSERT INTO user_table VALUES (?,?)");
   for (int i = 0; i < 3; i++) {
    pst.setInt(1, i);
    pst.setString(2, "data " + i);
    pst.addBatch();
   }
   pst.executeBatch();

   pst.close();
   System.out.println("Insert succeed!");
 

  } catch (SQLException e) {
   if (pst != null) {
    try {
     pst.close();
    } catch (SQLException e1) {
    e1.printStackTrace();
    }
   }
   e.printStackTrace();
  }
 }
 public static void ExecPreparedSQL(Connection conn) {
  PreparedStatement pstmt = null;
  try {
   pstmt = conn.prepareStatement("UPDATE user_table SET user_name = ? WHERE user_id = 1");
   pstmt.setString(1, "new Data");
   int rowcount = pstmt.executeUpdate();
   pstmt.close();
   System.out.println("Update succeed!");
  } catch (SQLException e) {
   if (pstmt != null) {
    try {
     pstmt.close();
 

    } catch (SQLException e1) {
     e1.printStackTrace();
    }
   }
   e.printStackTrace();
  }
 }


public static void main(String[] args) {
  Connection conn = GetConnection("dbadmin", "tdapg@2021");
  CreateTable(conn);
  BatchInsertData(conn);
  ExecPreparedSQL(conn);
  try {
   conn.close();
   } catch (SQLException e) {
   e.printStackTrace();
   }
  }
}
```
Execution result:
![](https://main.qcloudimg.com/raw/64d648b009a743c91f5e2999c6351886.png)
