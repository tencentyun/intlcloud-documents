## Overview
This document describes how to quickly create, configure, and deploy a web framework application in Tencent Cloud through Serverless Framework.


## Prerequisites
- [Serverless Framework 1.67.2 or above](https://github.com/AprilJC/Serverless-Framework-Docs/blob/main/docs/%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/%E4%B8%8B%E8%BD%BD%E5%AE%89%E8%A3%85.md) has been installed.
```
npm install -g serverless
```
- You have [registered a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/10495).

>?If your account is a **Tencent Cloud sub-account**, please get the authorization from the root account first as instructed in [Account and Permission Configuration](https://github.com/AprilJC/Serverless-Framework-Docs/blob/main/docs/%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/%E6%9D%83%E9%99%90%E9%85%8D%E7%BD%AE%E8%AF%B4%E6%98%8E.md#%E5%AD%90%E8%B4%A6%E5%8F%B7%E6%9D%83%E9%99%90%E9%85%8D%E7%BD%AE).

## Directions
### Quick deployment
In an **empty folder** directory, run the following command:

```sh
serverless
```

Next, follow the interactive prompts to initialize the project. Please select the application framework template you want to deploy (Express is used as an example here):
```sh
Serverless: No serverless project is detected. Do you want to create one? Yes
Serverless: Please select the serverless application you want to create: express-starter

  eggjs-starter - quickly deploys a basic Egg.js application 
❯ express-starter - quickly deploys a basic Express.js application 
  flask-starter - quickly deploys a basic Flask application 
  fullstack - quickly deploys a full stack application (Vue.js + Express + Postgres) 
  koa-starter - quickly deploys a basic Koa.js application 
  laravel-starter - quickly deploys a basic Laravel application 
  nextjs-starter - quickly deploys a basic Next.js application 
  
Serverless: Please enter the project name: demo
Serverless: Installing the express-starter application...


express-starter › Created


The demo project has been successfully created!
```

Select **Deploy Now** to quickly deploy the initialized project to the Tencent Cloud platform:

```sh
Serverless: Do you want to deploy the project in the cloud now? Yes

xxxxxxxx
x  QR  x
x CODE x
xxxxxxxx
Please scan the QR code above with WeChat or click the link below to log in
https://slslogin.qcloud.com/XKYUcbaK
Logged in successfully!

serverless ⚡framework
Action: "deploy" - Stage: "dev" - App: "demo1" - Instance: "expressDemo"

region: ap-guangzhou
apigw: 
  serviceId:   service-xxxxx
  subDomain:   service-xxxxx.gz.apigw.tencentcs.com
  environment: release
  url:         https://service-xxxxx.gz.apigw.tencentcs.com/release/
scf: 
  functionName: express_component
  runtime:      Nodejs10.15
  namespace:    default
  lastVersion:  $LATEST
  traffic:      1

26s › expressDemo › Success
```

After the deployment is completed, click the API Gateway link output by the command line to quickly access the successfully deployed web framework application.

### Viewing deployment information

If you want to check the deployment status and resources of the application again, you can go to the folder where the project is successfully deployed and run the following command to view the corresponding information:

```
cd demo # Enter the project directory. Please change to your actual project's directory name here
sls info
```
>?`sls` is short for the `serverless` command.

### Viewing directory structure
In the directory of the initialized project, you can see the most basic structure of an Express project:

```
.
├── serverless.yml  # Configuration file
├—— index.js    # Entry function
├—— package.json # Project dependencies
└── .env # Environment variable file
```

- The `serverless.yml` configuration file implements the quick configuration of the basic function information. All the configuration items supported by the SCF console can be configured in the `.yml` file (for more information, please see [SCF Configuration Information](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md)).
- `index.js` is the entry function of the project, which is the `helloworld` template here.
- `package` is the dependent file of the project, which records the dependency package that should be installed for the Express project.
- The `.env` file stores user login authentication information. You can also configure other environment variables in it.

### Redeployment
In the local project directory, you can modify the function template and configuration file, reinstall the dependencies, and then redeploy the project by running the following command:
```
npm install && sls deploy
```
>?If you want to view the details during the removal process, you can add the `--debug` parameter after `sls deploy`.

### Continuous development
After the deployment is completed, you can log in to the [SSR console](https://console.cloud.tencent.com/ssr) to view the monitoring metric data output after project deployment, such as the basic information, the number of project requests, and project error statistics.
View the monitoring metric data output after project deployment, such as the basic information, the number of project requests, and project error statistics, and implement the continuous development and deployment of the project.

For more information, please see [Console Deployment Guide](https://github.com/AprilJC/Serverless-Framework-Docs/blob/main/docs/%E6%A1%86%E6%9E%B6%E8%BF%81%E7%A7%BB/%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%83%A8%E7%BD%B2%E6%8C%87%E5%8D%97.md).
Serverless Framework supports running different commands to help you implement continuous development, deployment, and grayscale release for the project. You can also use this component in conjunction with other advanced capabilities such as **layer** and **custom domain name** to configure advanced features for the application.


## FAQs

- Problem 1: the wizard does not pop up by default when `serverless` is entered.
  Solution: add the `SERVERLESS_PLATFORM_VENDOR=tencent` configuration item to the `.env` file.
	
- Problem 2: after `sls deploy` is entered in a network environment outside the Chinese mainland, the deployment is very slow.
  Solution: add the `GLOBAL_ACCELERATOR_NA=true` configuration item to the `.env` file to enable acceleration outside the Chinese mainland. 
	
- Problem 3: after `sls deploy` is entered, the deployment reports a network error.
  Solution: add the following proxy configuration to the `.env` file.
  ```
  HTTP_PROXY=http://127.0.0.1:12345 # Replace "12345" with your proxy port
  HTTPS_PROXY=http://127.0.0.1:12345 # Replace "12345" with your proxy port
  ```
