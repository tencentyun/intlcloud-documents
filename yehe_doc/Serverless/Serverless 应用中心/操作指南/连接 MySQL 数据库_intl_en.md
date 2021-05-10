## Overview
This document uses a function written in Node.js as an example to describe how to quickly create a TDSQL-C Serverless MySQL instance and call it in SCF.

## Directions

| Step | Description |
|---------|---------|
| [Step 1. Configure environment variables](#step1) | - |
| [Step 2. Configure a VPC](#step2) | Use the Serverless Framework VPC component to create a VPC and subnet for communications between the function and the database. |
| <nobr>[Step 3. Configure Serverless DB](#step3)</nobr> | Use the Serverless Framework CynosDB component to create a MySQL instance to provide database services for the function project. |
| [Step 4. Write business code](#step4) | Use the Serverless DB SDK to call the database. SCF allows you to directly call the Serverless DB SDK to connect to and manage a PostgreSQL database. |
| [Step 5. Deploy an application](#step5) | Use Serverless Framework to deploy the project in the cloud and test it in the SCF console. |
| [Step 6. Remove the project (optional)](#remove) | You can use Serverless Framework to remove the project. |

<span id="step1"></span>

### Step 1. Configure environment variables

1. Create a local directory to store code and dependent modules. This document uses the `test-MySQL` folder as an example.
```
mkdir test-MySQL && cd test-MySQL
```

2. Currently, TDSQL-C Serverless only supports four regions: `ap-beijing-3`, `ap-guangzhou-4`, `ap-shanghai-2`, and `ap-nanjing-1`, so you need to create the `.env` file in the project root directory and then configure the two environment variables `REGION` and `ZONE`:
```text
# .env
REGION=xxx  
ZONE=xxx 
```

<span id="step2"></span>

### Step 2. Configure a VPC

1. Create a `VPC` folder in the `test-MySQL` directory.
```
mkdir VPC && cd VPC
```

2. Create a `serverless.yml` file in `VPC` and use the [VPC component](https://github.com/serverless-components/tencent-vpc) to create the VPC and subnet.
The sample content of `serverless.yml` is as follows (for all configuration items, please see the [product documentation](https://github.com/serverless-components/tencent-vpc/blob/master/docs/configure.md)):
``` yml
#serverless.yml
app: mysql-app
stage: dev
component: vpc # (required) name of the component. In that case, it's vpc.
name: mysql-app-vpc # (required) name of your vpc component instance.
inputs:
    region: ${env:REGION}
    zone: ${env:ZONE}
    vpcName: serverless-mysql
    subnetName: serverless-mysql
```

<span id="step3"></span>
### Step 3. Configure Serverless DB
1. Create a `DB` folder in `test-MySQL`.

2. Create a `serverless.yml` file in the `DB` folder and enter the following content to use the Serverless Framework component to configure the TCB environment:
The sample content of `serverless.yml` is as follows (for all configuration items, please see the [product documentation](https://github.com/serverless-components/tencent-cynosdb/blob/master/docs/configure.md)):
``` yml
# serverless.yml 
app: mysql-app
stage: dev
component: cynosdb
name: mysql-app-db
inputs:
  region: ${env:REGION}
  zone: ${env:ZONE}
  vpcConfig:
    vpcId: ${output:${stage}:${app}:mysql-app-vpc.vpcId}
    subnetId: ${output:${stage}:${app}:mysql-app-vpc.subnetId}
```

<span id="step4"></span>
### Step 4. Write the business code and configuration file
1. Create an `src` folder in `test-MySQL` to store the business logic code and relevant dependencies.

2. Create an `index.js` file in the `src` folder and enter the following sample code, so that you can use the SDK to connect to the MySQL database through the function and call the database in the environment:
``` js
exports.main_handler = async (event, context, callback) => {
    var mysql      = require('mysql2');
    var connection = mysql.createConnection({
    host     : process.env.HOST,
    user     : 'root',
    password : process.env.PASSWORD
    });
    connection.connect();
    connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
    if (error) throw error;
    console.log('The solution is: ', results[0].solution);
    });
    connection.end();
 }
```

3. Install the required dependent modules.
```
npm install mysql2
```

4. After writing the business code and installing the dependencies, create a `serverless.yml` file as shown below:

``` yml
app: mysql-app
stage: dev
component: scf
name: mysql-app-scf

inputs:
  src: ./
  functionName: ${name}
  region: ${env:REGION}
  runtime: Nodejs10.15
  timeout: 30
  vpcConfig:
    vpcId: ${output:${stage}:${app}:mysql-app-vpc.vpcId}
    subnetId: ${output:${stage}:${app}:mysql-app-vpc.subnetId}
  environment:
    variables:
      HOST: ${output:${stage}:${app}:mysql-app-db.connection.ip}
      PASSWORD: ${output:${stage}:${app}:mysql-app-db.adminPassword}
```

<span id="step5"></span>
### Step 5. Deploy
After the creation, the project directory structure is as follows:

```
   ./test-MySQL
   ├── vpc
   │   └── serverless.yml # VPC configuration file
   ├── db
   │   └── serverless.yml # Database configuration file
   ├── src
   │   ├── serverless.yml # SCF component configuration file
   │   ├── node_modules # Project dependency file
   │   └── index.js # Entry function
   └── .env # Environment variable file
```
1. Run the following command for deployment in `test-MySQL` on the command line:
```bash
sls deploy
```
>?
>- During deployment, you need to scan the QR code to authorize. If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If your account is a sub-account, please get the authorization first as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

 If the following result is returned, the deployment is successful:

``` mysql
mysql-app-vpc: 
  region:        xxx
  zone:          xxx
  vpcId:         xxxx-xxx
  ...

mysql-app-db: 
  dbMode:        xxxx
  region:        xxxx
  zone:          xxxx
  ...

mysql-app-scf: 
  functionName:  xxxx
  description:   xxx
  ...

59s › test-MySQL › "deploy" ran for 3 apps successfully.
```

2. After the deployment succeeds, you can view and debug the function in the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1). 

<span id="step6"></span>
### Step 6. Remove the project (optional)
Run the following command in the `test-MySQL` directory to remove the project:
```
sls remove
```
If the following result is returned, the removal is successful:
```
serverless ⚡ framework
4s › test-MySQL › Success
```

## Sample Code
### Python
In Python, you can use the built-in **pymysql** dependency package in the SCF environment to connect to the database. The sample code is as follows:

```  python
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


### Node.js
Node.js allows you to use a connection pool for connection, which supports automatic reconnection to effectively avoid connection unavailability due to connection release by the SCF underlying layer or database. The sample code is as follows:
>?Before using a connection pool, you need to install the **mysql2** dependency package first. For more information, please see [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879).

```  nodejs
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


### PHP
In PHP, you can use the **pdo_mysql** or **mysqli** dependency package for data connection. The sample code is as follows:
- **pdo_mysql**

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

- **mysqli** 
``` php
<?php
function main_handler($event, $context) {
     $host = "";
    $username = "";
    $password = "";
 
    // Create a connection
    $conn = mysqli_connect($servername, $username, $password);

    // Test the connection
    if (!$conn) {
        die("Connection failed: " . mysqli_connect_error());
        }
    echo "Connected successfully"; 

    mysqli_close($conn);
    echo "Disconnected"; 
}
?>
```

### Java
1. Please install the following dependencies as instructed in [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879#java-.E8.BF.90.E8.A1.8C.E6.97.B6).
```  xml
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

``` java
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


### SCF DB SDK for MySQL

For ease of use, the SCF team encapsulated the code related to connection pools in Node.js and Python as SCF DB SDK for MySQL. Please refer to [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879) for installation and use. With this SDK, you can connect to [MySQL](https://intl.cloud.tencent.com/document/product/236/5147) or [TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/1042/33311) databases and performs operations such as insertion and query.

SCF DB SDK for MySQL has the following features:
- It can automatically initialize the database client from environment variables.
- It can maintain a persistent database connection globally and handle reconnection after disconnection.
- The SCF team will continuously check issues to ensure that the database connection is available, so you don't need to pay attention to connection issues.

**1. SDK for Node.js**

```  JavaScript
'use strict';
const database = require('scf-nodejs-serverlessdb-sdk').database;

exports.main_handler = async (event, context, callback) => {
  let pool = await database('TESTDB2').pool()
  pool.query('select * from coffee',(err,results)=>{
    console.log('db2 callback query result:',results)
  })
  // no need to release pool

  console.log('db2 query result:',result)
}
```

>?For specific usage of the SDK for Node.js, please see [SCF DB SDK for MySQL](https://www.npmjs.com/package/scf-nodejs-serverlessdb-sdk).


**2. SDK for Python**

``` Python
from serverless_db_sdk import database

def main_handler(event, context):
    print('Start Serverlsess DB SDK function')

    connection = database().connection(autocommit=False)
    cursor = connection.cursor()
    
    cursor.execute('SELECT * FROM name')
    myresult = cursor.fetchall()
    
    for x in myresult:
        print(x)
```
