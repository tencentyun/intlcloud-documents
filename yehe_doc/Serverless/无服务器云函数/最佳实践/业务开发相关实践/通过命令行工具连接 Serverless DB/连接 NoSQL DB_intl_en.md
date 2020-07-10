## Operation Scenarios
You can use the [Serverless Framework component](https://intl.cloud.tencent.com/document/product/1040/33163) to create, deploy, and manage a Serverless DB instance easily and connect to and access the database through the SCF SDK. Based on the serverless services in the cloud, you can conveniently develop and rapidly deploy your business with "zero" configuration so as to implement it more easily.

Currently, Serverless Framework supports connecting to and deploying two types of databases: **PostgreSQL** and **NoSQL**. This document describes how to use an SCF function to connect to a NoSQL database.


## Prerequisites
You have installed Serverless Framework on at least the following versions; otherwise, please install it as instructed in [Installing Serverless Framework](https://intl.cloud.tencent.com/document/product/583/36263).
```
Framework Core: 1.67.3
Plugin: 3.6.6
SDK: 2.3.0
Components: 2.30.1
```




## Notes
- Please make sure that the executing role of `SLS_QcsRole` under your account has been granted the `QcloudTCBFullAccess` permission; otherwise, please go to the [CAM Console](https://console.cloud.tencent.com/cam/role) to configure it.
- Currently, TCB allows you to create/terminate an environment for up to **4** times per month. Please create an environment with caution, as an error will be reported if the limit is exceeded.


## Directions
This document uses a function in the Node.js programming language as an example to describes how to use the Serverless Framework component to write and create a function and use it to create and access a NoSQL database. The configuration process is as follows:
1. **Configure identity information**: configure the Tencent Cloud account information locally.
1. **Create a TCB environment configuration file**: use the [Serverless Framework component](https://intl.cloud.tencent.com/document/product/1040/33164) to create a TCB environment and create and use a NoSQL database in the environment.
2. **Write business code**: use the Serverless DB SDK to call the database. SCF allows you to directly call the Serverless DB SDK to create and manage a NoSQL database.
4. **Deploy and debug**: use Serverless Framework to deploy the project in the cloud and test it in the SCF Console.
5. **Remove project**: you can use Serverless Framework to remove the project.



### Configuring identity information
1. Create a local directory to store code and dependent modules. This document uses the `test-NoSQL` folder as an example.
2. Serverless Framework allows you to configure identity information in the following two ways. Please choose one as needed:
	- Run the following command for authentication:
```
serverless login
```
	- Create a `.env` file in `test-NoSQL` and configure the corresponding Tencent Cloud `SecretId` and `SecretKey` as follows:
```text
# .env
TENCENT_SECRET_ID=xxx  // `SecretId` of your account
TENCENT_SECRET_KEY=xxx // `SecretKey` of your account
```
>?
> - If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
> - If you already have a Tencent Cloud account, please make sure that your account has been granted the `AdministratorAccess` permission. In addition, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
>


### Creating TCB environment configuration file
1. Create a `DB` folder in `test-NoSQL`.
2. Create a `serverless.yml` file in the `DB` folder and enter the following content to use the Serverless Framework component to configure the TCB environment:
```
# serverless.yml 
component: mongodb
name: mongoDBDemoMongo
org: anycodes
app: mongoDBAPP
stage: dev
inputs:
     name: Mydemo
```

### Writing business code
1. Create a `function` folder in `test-NoSQL` to store the business logic code and relevant dependencies.
2. Create an `src` folder in the `function` folder, enter it on the command line, and run the following command to install the [TCB dependency package](https://www.npmjs.com/package/tcb-admin-node):
```
npm install --save tcb-admin-node@latest
```
3. Create an `index.js` file in the `src` folder and enter the following sample code, so that you can use the Serverless TCB SDK to call the TCB environment through the function and call the NoSQL database in the environment:
```
const tcb = require('tcb-admin-node')
const app = tcb.init({
	secretId: process.env.SecretId,
	secretKey: process.env.SecretKey,
	env: process.env.MongoId,
	serviceUrl: 'https://tcb-admin.tencentcloudapi.com/admin'
})
const db = app.database()
const _ = db.command
exports.main = async (event, context) => {
	await db.createCollection('serverless')
	const username = 'serverless'
	const collection = db.collection('serverless')
	if (username) {
			await collection.add({username: username})
				}
		const userList = await collection.get()
		return userList
}
```
5. After writing the business code, create a `serverless.yml` file and enter your **SecretId** and **SecretKey** in the environment variables.
>!If you use the following configuration, a TCB environment will be created free of charge. If you already have a free TCB environment, please enter its ID in `MongoId`; otherwise, an error will be reported. 
>
```
component: scf
name: mongoDBDemoSCF
org: anycodes
app: mongoDBAPP
stage: dev
inputs:
     name: MongoDBDemo
     src: ./src
     runtime: Nodejs8.9
     region: ap-guangzhou
     handler: index.main
     environment:
       variables:
         SecretId: enter your `SecretId`
         SecretKey: enter your `SecretKey`
         MongoId: ${output:${stage}:${app}:mongoDBDemoMongo.EnvId}
```



### Deploying and debugging
1. Run the following command for deployment in `test-NoSQL` on the command line:
```bash
sls deploy --all
```
If the following result is returned, the deployment is successful:
```
serverless ⚡ framework
mongoDBDemoMongo:
     Region:    ap-guangzhou
     Name:      Mydemo
     EnvID:     Mydemo-dyxfxv
     FreeQuota: basic
mongoDBDemoSCF: 
     FunctionName: MongoDBDemo
     Description:  
       Namespace:    default
       Runtime:      Nodejs8.9
       Handler:      index.main
       MemorySize:   128
25s › tcbdemo › Success
```
2. After the deployment succeeds, you can view and debug the function in the [SCF Console](https://console.cloud.tencent.com/scf/index?rid=1). For more information on the test steps, please see [Cloud Test](https://intl.cloud.tencent.com/document/product/583/32742). The test success result is as shown below:
![](https://main.qcloudimg.com/raw/c3dba8555c20e92559cb9541ce6da8d5.png)
>?You can also use [Serverless Dashboard](https://serverless.cloud.tencent.com/) to monitor the deployed project in real time with ease.
>

### Removing project
Run the following command in the `test-NoSQL` directory to remove the project:
```
sls remove --all
```
If the following result is returned, the removal is successful:
```
serverless ⚡ framework
4s › test-NoSQL › Success
```

