
This document describes how to create and connect to a PostgreSQL for Serverless instance.

## Use Limits
- During the beta period, a single user can enjoy up to 40,000 QPS and 100 GB disk capacity.
- Currently, PostgreSQL for Serverless instances can be created only with APIs.
- Currently, only Beijing Zone 3, Shanghai Zone 2, and Guangzhou Zone 2 are supported.

## Directions
### Step 1. Create an instance
#### Using Serverless Framework to create an instance
Create an instance quickly with [Serverless Framework](https://intl.cloud.tencent.com/document/product/1040/36821).

#### Using APIs to create an instance
Create an instance with the [CreateServerlessDBInstance](https://intl.cloud.tencent.com/document/product/409/38880) API.

Some important input parameters are listed as follows. For more information, please see [CreateServerlessDBInstance](https://intl.cloud.tencent.com/document/product/409/38880).

| Parameter Name         | Required | Type   | Description                                                        |
| -------------- | ------ | ------ | ----------------------------------------------------------- |
| Zone          | Yes     | string | Availability zone ID. Valid values: ap-shanghai-2, ap-beijing-3, ap-guangzhou-2 |
| DBInstanceName | Yes     | string | TencentDB instance name. This value must be unique for the same account.                    |
| DBVersion      | Yes     | string | Database version. Valid value: 10.4                                |
| DBCharset      | Yes     | string | PostgreSQL database character set. Valid values: UTF8, LATIN1 |
| VpcId          | No     | string | VPC ID. If this parameter is left empty, the instance will be assigned with a classic network IP.     |
| SubnetId       | No     | string | VPC subnet ID. This parameter should be used together with `VpcId`.                  |

After successful execution, the output sample is as follows:
```
{
  "Response": {
    "RequestId": "20304c-6fd7-4427-8e09-2b081e1",
    "DBInstanceId": "postgres-xxxxxxx"  
  }
}
```
Where, `DBInstanceId` refers to the instance ID.

### Step 2. Connect to the instance
1. Use the [DescribeServerlessDBInstances](https://intl.cloud.tencent.com/document/product/409/38878) API to query the information of the PostgreSQL for Serverless instance you just created, including instance IP, port, username, and initial password.
```
{
  "Response": {
    "TotalCount": 1,
    "DBInstanceSet": [
      {
        "DBInstanceId": "postgres-xxxxxxx",
        "DBInstanceName": "test",
        "DBInstanceStatus": "running",#TencentDB instance status
        "Region": "ap-shanghai",
        "Zone": "ap-shanghai-2",
        "ProjectId": 0,
        "VpcId": "vpc-test",
        "SubnetId": "subnet-test",
        "DBCharset": "UTF8",
        "DBVersion": "10.4",
        "CreateTime": "2020-03-23 11:43:56",
        "DBInstanceNetInfo": [
          {
            "Address": "",
            "Ip": "10.1.1.2", #This IP is used as an example. The IP can be accessed over the same subnet and the same private network.
            "Port": 5432, #Connect to the port
            "Status": "opened",
            "NetType": "private"
          },
          {
            "Address": "",
            "Ip": "",
            "Port": 0,
            "Status": "0",
            "NetType": "public"
          }
        ],
        "DBAccountSet": [
          {
            "DBUser": "tencentdb_xxxxxxx",
            "DBPassword": "**************",#Database password. After the password has been reset, the parameter value returned by this API will be invalid.
            "DBConnLimit": 100
          }
        ],
        "DBDatabaseList": [
          "tencentdb_xxxxxxx"
        ]
      }
    ],
    "RequestId": "89583d-cfdd-4db1-bd32-64eb1dbfa"
  }
}
```

2. Taking a CVM instance on CentOS 7.2 (64-bit) as an example, run the following command to install the PostgreSQL client.
```
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
yum install postgresql10 postgresql10.x86_64
```
3. Run the following command to connect to the database.
>?
>- To connect over a private network, you need to use a [CVM](https://intl.cloud.tencent.com/document/product/213/10517) instance to access the private IP of the TencentDB instance, and the two instances must be under the same account and in the same VPC in the same region.
>- To connect over a public network, you need to [enable public access](#kqgbslww) for the instance.
>
```
psql -U database username -h IP address -p port number
```
In this example, the prompt `tencentdb_xx>` indicates successful connection.
![](https://main.qcloudimg.com/raw/bb9562c380e7c42d3e26e7c9d61a172a.png)
4. After successful connection, you can manage database data with SQL statements. For more information, please see [Official Document](https://www.postgresql.org/docs/10/sql-syntax-lexical.html#SQL-SYNTAX-IDENTIFIERS).
>!PostgreSQL for Serverless does not support the following operations:
>- Create a database
>- Access the `postgres` system database
>- View database parameters
>- SET/RESET statements
>- LOAD statements
>- PRESERVE/DELETE ROWS temp tables+
>- LISTEN/NOTIFY
>- WITH HOLD CURSOR
>- PREPARE/DEALLOCATE

<span id="kqgbslww"></span>
## Appendix. Enabling Public Network Access for Instances
To access an instance over a public network, you can use the [OpenServerlessDBExtranetAccess](https://intl.cloud.tencent.com/document/product/409/39712) API to enable the public network access for the instance.
>?After public network access is enabled, the database can be connected and accessed over a public network, which poses security risks. We recommend you access your database instances over a private network.

## References
- You can use the [CloseServerlessDBExtranetAccess](https://intl.cloud.tencent.com/document/product/409/39713) API to disable public network access for an instance.
- You can use the [DeleteServerlessDBInstance](https://intl.cloud.tencent.com/document/product/409/38879) API to terminate an instance.
>!Please note that once an instance is terminated, its data cannot be restored.
- You can use [Serverless Framwork](https://intl.cloud.tencent.com/document/product/1040/36989) to quickly create PostgreSQL for Serverless-based web applications.

