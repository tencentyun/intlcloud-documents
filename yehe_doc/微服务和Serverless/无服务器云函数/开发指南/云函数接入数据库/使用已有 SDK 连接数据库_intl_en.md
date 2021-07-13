## Operation Scenarios
This document describes how to use an existing SDK to connect to a [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/5147) database in the SCF function code and perform operations such as insertion and query in the database. [TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/1042/33311) databases can also be connected. You can perform relevant operations as needed.



## Prerequisites
You have signed up for a Tencent Cloud account and completed identity verification. If you haven't done so, please sign up [here](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F).



## Directions
<span id="createVPC"></span>
### Creating VPC
Create a VPC and subnet as instructed in [Building VPC](https://intl.cloud.tencent.com/document/product/215/31891).

### Creating database instance
1. Create a TencentDB for MySQL database as instructed in [Purchase Method](https://intl.cloud.tencent.com/document/product/236/5160).
>?Select the VPC created in [Creating VPC](#createVPC) as the "Network".
>
2. Initialize the database as instructed in [Initializing TencentDB for MySQL Database](https://intl.cloud.tencent.com/document/product/236/3128) and get the database account name and password.
3. On the [TencentDB for MySQL - Instance List](https://console.cloud.tencent.com/cdb) page, select the instance ID to enter the database details page and get the **private address**, **network**, and **private port** of the database as shown below:
![](https://main.qcloudimg.com/raw/9fc693925406344b169234793205ea48.png)

### Creating security group (optional)
You can add a security group for your database instance as instructed in [TencentDB Security Group](https://intl.cloud.tencent.com/document/product/236/14470).


### Configuring environment variables and VPC
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. Click the name of the function to be connected to the database to enter the "Function Configuration" page of the function and configure the function as shown below:
 - Add an **environment variable** and enter the information by referring to the table below:
![]( https://main.qcloudimg.com/raw/8c75b2184a416c8ee7604402139d1370.png)
<table align=center>
<tr>
<th>key</th>
<th>value</th>
</tr>
<tr>
<td>DB_PASSWORD</td>
<td>Database password</td>
</tr>
<tr>
<td>DB_USER</td>
<td>Database username</td>
</tr>
<tr>
<td>DB_HOST</td>
<td>Database address</td>
</tr>
<tr>
<td>DB_PORT</td>
<td>Database port</td>
</tr>
<tr>
<td>DB_DATABASE</td>
<td>Database name</code></td>
</tr>
</table>
 - Enable VPC and select the same VPC and subnet as those of the database as shown below:
 
![](https://main.qcloudimg.com/raw/757abc018b4767f28902c7ed6465ff47.png)


### Sample function code

#### Python
In Python, you can use the built-in **pymysql** dependency package in the SCF environment to connect to the database. The sample code is as follows:
```python
# -*- coding: utf8 -*-
from os import getenv

import pymysql
from pymysql.err import OperationalError

mysql_conn = None

def __get_cursor():
    try:
        return mysql_conn.cursor()
    except OperationalError:
        mysql_conn.ping(reconnect=True)
        return mysql_conn.cursor()

def main_handler(event, context):
    global mysql_conn
    if not mysql_conn:
        mysql_conn = pymysql.connect(
        host        = getenv('DB_HOST', '<YOUR DB HOST>'),
        user        = getenv('DB_USER','<YOUR DB USER>'),
        password    = getenv('DB_PASSWORD','<YOUR DB PASSWORD>'),
        db          = getenv('DB_DATABASE','<YOUR DB DATABASE>'),
        port        = int(getenv('DB_PORT','<YOUR DB PORT>')),
        charset     = 'utf8mb4',
        autocommit  = True
        )
    
    with __get_cursor() as cursor:
        cursor.execute('select * from employee')
        myresult = cursor.fetchall()
        print(myresult)
        for x in myresult:
            print(x)
```

#### Node.js
Node.js allows you to use a connection pool for connection, which supports automatic reconnection to effectively avoid connection unavailability due to connection release by the SCF underlying layer or database. The sample code is as follows:
>?Before using a connection pool, you need to install the **mysql2** dependency package first. For more information, please see [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879).
>
```nodejs
'use strict';

const DB_HOST       = process.env[`DB_HOST`]
const DB_PORT       = process.env[`DB_PORT`]
const DB_DATABASE   = process.env[`DB_DATABASE`]
const DB_USER       = process.env[`DB_USER`]
const DB_PASSWORD   = process.env[`DB_PASSWORD`]

const promisePool = require('mysql2').createPool({
  host              : DB_HOST,
  user              : DB_USER,
  port              : DB_PORT,
  password          : DB_PASSWORD,
  database          : DB_DATABASE,
  connectionLimit   : 1
}).promise();

exports.main_handler = async (event, context, callback) => {
  let result = await promisePool.query('select * from employee');
  console.log(result);
}
```

#### PHP
In PHP, you can use the **pdo_mysql** dependency package for data connection. The sample code is as follows:
```php
<?php
function handler($event, $context) {
try{
  $pdo = new PDO('mysql:host= getenv("DB_HOST");dbname= getenv("DB_DATABASE"),getenv("DB_USER"),getenv("DB_PASSWORD")');
  $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
}catch(PDOException $e){
  echo 'Databases connection failed: '.$e->getMessage();
  exit;
}
}
```

#### Java
1. Please install the following dependencies as instructed in [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879#java-.E8.BF.90.E8.A1.8C.E6.97.B6).

```xml
<dependencies>
    <dependency>
        <groupId>com.tencentcloudapi</groupId>
        <artifactId>scf-java-events</artifactId>
        <version>0.0.2</version>
    </dependency>
    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>HikariCP</artifactId>
        <version>3.2.0</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.11</version>
    </dependency>
</dependencies>
```
2. Use HikariCP for connection. The sample code is as follows:

```java
package example;

import com.qcloud.scf.runtime.Context;
import com.qcloud.services.scf.runtime.events.APIGatewayProxyRequestEvent;
import com.qcloud.services.scf.runtime.events.APIGatewayProxyResponseEvent;
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;

import javax.sql.DataSource;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.HashMap;
import java.util.Map;

public class Http {
    private DataSource dataSource;

    public Http() {
        HikariConfig config = new HikariConfig();
        config.setJdbcUrl("jdbc:mysql://" + System.getenv("DB_HOST") + ":"+ System.getenv("DB_PORT") + "/" + System.getenv("DB_DATABASE"));
        config.setUsername(System.getenv("DB_USER"));
        config.setPassword(System.getenv("DB_PASSWORD"));
        config.setDriverClassName("com.mysql.jdbc.Driver");
        config.setMaximumPoolSize(1);
        dataSource = new HikariDataSource(config);
    }

    public String mainHandler(APIGatewayProxyRequestEvent requestEvent, Context context) {
        System.out.println("start main handler");
        System.out.println("requestEvent: " + requestEvent);
        System.out.println("context: " + context);

        try (Connection conn = dataSource.getConnection(); PreparedStatement ps = conn.prepareStatement("SELECT * FROM employee")) {
            ResultSet rs = ps.executeQuery();
            while (rs.next()) {
                System.out.println(rs.getInt("id"));
                System.out.println(rs.getString("first_name"));
                System.out.println(rs.getString("last_name"));
                System.out.println(rs.getString("address"));
                System.out.println(rs.getString("city"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }

        APIGatewayProxyResponseEvent apiGatewayProxyResponseEvent = new APIGatewayProxyResponseEvent();
        apiGatewayProxyResponseEvent.setBody("API GW Test Success");
        apiGatewayProxyResponseEvent.setIsBase64Encoded(false);
        apiGatewayProxyResponseEvent.setStatusCode(200);

        Map<String, String> headers = new HashMap<>();
        headers.put("Content-Type", "text");
        headers.put("Access-Control-Allow-Origin", "*");
        apiGatewayProxyResponseEvent.setHeaders(headers);

        return apiGatewayProxyResponseEvent.toString();
    }
}
```











