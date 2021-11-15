## Connecting with Client
TDSQL for MySQL supports a connection method compatible with MySQL. It can be connected using the IP address, port number, username, and password, as shown below:
```
mysql -hxxx.xxx.xxx.xxx -Pxxxx -uxxx -pxxx -c
```
>!TDSQL for MySQL does not support clients earlier than version 4.0 and compression protocols. We recommend that you add the `-c` option when using the client, so that you can use advanced features.

## Connecting with PHP MySQLi
To connect to TDSQL for MySQL in PHP, you need to enable the MySQLi extension. A demo is as follows:
```
header("Content-Type:text/html;charset=utf-8");
$host="10.10.10.10";  //Instance proxy_host_ip
$user="test";  //Instance user
$pwd="test";  //Instance password
$db="aaa";  //Database name
$port="15002";  //proxy_host port number
$sqltool=new MySQLli($host,$user,$pwd,$db,$port);
//Other necessary code
$sqltool->close();
echo "ok"."\n";
```

## Connecting with JDBC
You can run the following code to connect to TDSQL for MySQL with JDBC:
```
private final String USERNAME = "test";  
private final String PASSWORD = "123456"; 
private final String DRIVER = "com.mysql.jdbc.Driver";   
private final String URL = "jdbc:mysql://10.10.10.10:3306?userunicode=true&characterEncoding=utf8mb4";  
private Connection connection;  
private PreparedStatement pstmt;  
private ResultSet resultSet;  
```

## Other Connection Methods
TDSQL for MySQL supports other connection methods compatible with MySQL, such as Navicat and ODBC.
