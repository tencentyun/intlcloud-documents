## Operation Scenarios
You can use the [Serverless Framework component](https://intl.cloud.tencent.com/document/product/1040/33163) to create, deploy, and manage a Serverless DB instance easily and connect to and access the database through the SCF SDK. Based on the serverless services in the cloud, you can conveniently develop and rapidly deploy your business with "zero" configuration so as to implement it more easily.

Currently, Serverless Framework supports connecting to and deploying two types of databases: **PostgreSQL** and **NoSQL**. This document describes how to use an SCF function to connect to a PostgreSQL database.


## Prerequisites
You have installed Serverless Framework on at least the following versions; otherwise, please install it as instructed in [Installing Serverless Framework](https://intl.cloud.tencent.com/document/product/583/36263).
```
Framework Core: 1.67.3
Plugin: 3.6.6
SDK: 2.3.0
Components: 2.30.1
```

-  Make sure that the current account has been associated with the **QcloudPostgreSQLFullAccess** policy. To learn more about the association, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

## Directions
This document uses a function in the Node.js programming language as an example to describes how to use the Serverless Framework component to write and create a function and use it to access a PostgreSQL database. The configuration process is as follows:
1. **Configure identity information**: configure the Tencent Cloud account information locally.
1. **Configure a VPC**: use the Serverless Framework VPC component to create a **VPC** and **subnet** for communications between the function and the database.
2. **Configure Serverless DB**: use the Serverless Framework PostgreSQL component to create a PostgreSQL instance to provide database services for the function project.
3. **Write business code**: use the Serverless DB SDK to call the database. SCF allows you to directly call the Serverless DB SDK to connect to and manage a PostgreSQL database.
4. **Deploy and debug**: use Serverless Framework to deploy the project in the cloud and test it in the SCF Console.
5. **Remove project**: you can use Serverless Framework to remove the project.


### Configuring identity information
1. Create a local directory to store code and dependent modules. This document uses the `test-postgreSQL` folder as an example. 
2. Create a `.env` file in `test-postgreSQL` and configure your Tencent Cloud `SecretId`, `SecretKey`, region, and AZ information in the following format in the file:
```text
 # .env
 TENCENT_SECRET_ID=xxx  # `SecretId` of your account
 TENCENT_SECRET_KEY=xxx # `SecretKey` of your account
 # Region and AZ configuration
 REGION=ap-guangzhou # Resource deployment region, which refers to the region where the function and static webpage are deployed
 ZONE=ap-guangzhou-2 # Resource deployment AZ, which refers to the AZ where the database is deployed
```
>?
> - If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
> - If you already have a Tencent Cloud account, please make sure that your account has been granted the `AdministratorAccess` permission. In addition, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
>

### Configuring VPC
1. Create a `VPC` folder in `test-postgreSQL`.
2. Create a `serverless.yml` file in `VPC` and enter the following content to configure the VPC and subnet:
```text
org: fullstack
app: fullstack-serverless-db
stage: dev
component: vpc # (required) name of the component. In that case, it's vpc.
name: serverlessVpc # (required) name of your vpc component instance.
inputs:
     region: ${env:REGION}
     zone: ${env:ZONE}
     vpcName: serverless
     subnetName: serverless
```


### Configuring Serverless DB 
1. Create a `DB` folder in `test-postgreSQL`.
2. Create a `serverless.yml` file in `DB` and enter the following content to create and configure a PostgreSQL database:
```text
org: fullstack
app: fullstack-serverless-db
stage: dev
component: postgresql
name: fullstackDB
inputs:
     region: ${env:REGION}
     zone: ${env:ZONE}
     dBInstanceName: ${name}
     vpcConfig:
       vpcId: ${output:${stage}:${app}:serverlessVpc.vpcId}
       subnetId: ${output:${stage}:${app}:serverlessVpc.subnetId}
     extranetAccess: false
```



### Writing business code
1. Create an `api` folder in `test-postgreSQL` to store the business logic code and relevant dependencies.
2. Create an `src` folder in the `api` folder, enter it on the command line, and run the following command to install the [PostgreSQL dependency package](https://www.npmjs.com/package/pg):
```
npm install npm
```
3. Create an `index.js` file in the `src` folder and enter the following sample code, so that you can use the Serverless DB SDK to create a connection pool and call the database through the function:
```
'use strict';
const { Pool } = require('pg');
exports.main_handler = async (event, context, callback) => {
  let pgPool = new Pool({
        connectionString: process.env.PG_CONNECT_STRING,
      });
  await pgPool.query(`CREATE TABLE IF NOT EXISTS users (
        ID serial NOT NULL,
        NAME           TEXT         NOT NULL,
        EMAIL          CHAR(50)     NOT NULL,
        SITE          CHAR(50)     NOT NULL
      );`);
  const client = await pgPool.connect();
  const { rows } = await client.query({
      text: 'select * from users',
    });
  await client.end();
  console.log('pgsql query result:',rows)
}
```
4. Create a `serverless.yml` file in `api` and enter the following content to configure the `Connection String` of Serverless DB in the environment variables:
```
org: fullstack
app: fullstack-serverless-db
stage: dev
component: scf
name: fullstack-serverless-db
inputs:
     name: ${app}
     src:
       src: ./src
       exclude:
         - .env
     region: ${env:REGION}
     runtime: Nodejs10.15
     handler: index.main_handler
     timeout: 30
     vpcConfig:
       vpcId: ${output:${stage}:${app}:serverlessVpc.vpcId}
       subnetId: ${output:${stage}:${app}:serverlessVpc.subnetId}
     environment:
       variables:
         PG_CONNECT_STRING: ${output:${stage}:${app}:fullstackDB.private.connectionString}
```

### Deploying and debugging
1. Run the following command for deployment in the `test-postgreSQL` directory on the command line:
```
sls deploy --all
```
If the following result is returned, the deployment is successful:
```bash
serverless ⚡ framework
serverlessVpc: 
  region:     ap-guangzhou
  zone:       ap-guangzhou-2
  vpcId:      vpc-0ncak84t
  vpcName:    serverless
  subnetId:   subnet-gi085his
  subnetName: serverless
fullstackDB: 
  region:         ap-guangzhou
  zone:           ap-guangzhou-2
  vpcConfig: 
    subnetId: subnet-gi085his
    vpcId:    vpc-0ncak84t
  dBInstanceName: fullstackDB
  dBInstanceId:   postgres-0y2x3fd3
  private: 
    connectionString: postgresql://tencentdb_0y2x3fd3:GD0U1(q~g7%3D6ySI@10.0.0.10:5432/tencentdb_0y2x3fd3
    host:             10.0.0.10
    port:             5432
    user:             tencentdb_0y2x3fd3
    password:         GD0U1(q~g7=6ySI
    dbname:           tencentdb_0y2x3fd3
fullstack-serverless-db: 
  FunctionName: fullstack-serverless-db
  Description:  
  Namespace:    default
  Runtime:      Nodejs10.15
  Handler:      index.main_handler
  MemorySize:   128
25s › fullstack-serverless-db › Success
```
2. After the deployment succeeds, you can view and debug the function in the [SCF Console](https://console.cloud.tencent.com/scf/index?rid=1). For more information on the test steps, please see [Cloud Test](https://intl.cloud.tencent.com/document/product/583/32742). The test success result is as shown below:
![](https://main.qcloudimg.com/raw/c3dba8555c20e92559cb9541ce6da8d5.png)
>?You can also use [Serverless Dashboard](https://serverless.cloud.tencent.com/) to monitor the deployed project in real time with ease.
>

### Removing project
Run the following command in the `test-postgreSQL` directory to remove the project:
```bash
sls remove --all
```
If the following result is returned, the removal is successful:
```
serverless ⚡ framework
38s › tencent-fullstack › Success
```
