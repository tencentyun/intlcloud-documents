
## Overview
This document describes how to quickly create, configure, and deploy an SCF application in Tencent Cloud through Serverless Framework.

## Prerequisites
- [Serverless Framework 1.67.2 or above has been installed](https://intl.cloud.tencent.com/document/product/1040/37034).
```
npm install -g serverless
```
- You have [registered a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/10495).

>?If your account is a **Tencent Cloud sub-account**, please get the authorization from the root account first as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

## Directions
### Quick deployment

In an **empty folder** directory, run the following command:

```sh
serverless
```

Next, follow the interactive prompts to initialize the project. Please select the `scf-starter` template for the application and select the runtime you want to use (Node.js is used as an example here):
```sh
Serverless: 当前未检测到 Serverless 项目，是否希望新建一个项目？ Yes
Serverless: 请选择您希望创建的 Serverless 应用 scf-starter - 快速部署一个云函数

  react-starter - 快速部署一个 React.js 应用 
  restful-api - 快速部署一个 REST API 使用 python + API gateway 
❯ scf-starter - 快速部署一个云函数 
  vue-starter - 快速部署一个 Vue.js 基础应用 
  website-starter - 快速部署一个静态网站 
  eggjs-starter - 快速部署一个Egg.js 基础应用 
  express-starter - 快速部署一个 Express.js 基础应用 
  
Serverless: 请选择应用的运行时 scf-nodejs - 快速部署一个 nodejs 云函数

  scf-golang - 快速部署一个 golang 云函数 
❯ scf-nodejs - 快速部署一个 nodejs 云函数 
  scf-php - 快速部署一个 PHP 云函数 
  scf-python - 快速部署一个 python 云函数  
  
Serverless: 请输入项目名称 demo
Serverless: 正在安装 scf-nodejs 应用...

scf-nodejs › Created


demo 项目已成功创建!
```

Select **Deploy Now** to quickly deploy the initialized project to the SCF console:

```sh
Serverless: 是否希望立即将该项目部署到云端？ Yes

xxxxxxxx
x  QR  x
x CODE x
xxxxxxxx

serverless ⚡ framework
Action: "deploy" - Stage: "dev" - App: "scfApp" - Instance: "scfdemo"

functionName: helloworld
description:  helloworld 空白模板函数
namespace:    default
runtime:      Nodejs10.15
handler:      index.main_handler
memorySize:   128
lastVersion:  $LATEST
traffic:      1
triggers: 
  apigw: 
    - http://service-xxxxxxx.gz.apigw.tencentcs.com/release/

27s › scfdemo › Success
```

After deployment, complete the remote invocation of the function by running the following command:
```sh
sls invoke --inputs function=helloworld
```
>>?`sls` is short for the `serverless` command.

### Viewing deployment information

If you want to check the deployment status and resources of the application again, you can go to the folder where the project is successfully deployed and run the following command to view the corresponding information:

```
cd demo #进入项目目录，此处请改为您的项目目录名称
sls info
```

### Viewing directory structure
In the directory of the initialized project, you can see the most basic structure of a serverless function project:

```
.
├── serverless.yml  # 配置文件
├—— index.js    # 入口函数
└── .env # 环境变量文件
```

- The `serverless.yml` configuration file implements the quick configuration of the basic function information. All the configuration items supported by the SCF console can be configured in the `.yml` file (for more information, please see [SCF Configuration Information](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md)).
- `index.js` is the entry function of the project, which is the `helloworld` template here.
- The `.env` file stores user login authentication information. You can also configure other environment variables in it.

### Redeployment
In the local project directory, you can modify the function template and configuration file and then redeploy the project by running the following command:
```
sls deploy
```
>?If you want to view the details during the removal process, you can add the `--debug` parameter.

### Continuous development
After the deployment is completed, Serverless Framework supports running different commands to help you implement continuous development, deployment, and grayscale release for the project. You can also use this component in conjunction with other components to manage the deployment of multi-component applications.

For more information, please see [Application Management](https://intl.cloud.tencent.com/document/product/1040/38288) and [List of Supported Commands](https://intl.cloud.tencent.com/document/product/1040/36861).

## FAQs

- Problem 1: the wizard does not pop up by default when `serverless` is entered. 
  Solution: add the `SERVERLESS_PLATFORM_VENDOR=tencent` configuration item to the `.env` file.	

- Problem 2: after `sls deploy` is entered in a network environment outside the Chinese mainland, the deployment is very slow. 
  Solution: add the `GLOBAL_ACCELERATOR_NA=true` configuration item to the `.env` file to enable acceleration outside the Chinese mainland.	

- Problem 3: after `sls deploy` is entered, the deployment reports a network error. 
  Solution: add the following proxy configuration to the `.env` file.
  ```
  HTTP_PROXY=http://127.0.0.1:12345 #请将'12345'替换为您的代理端口
  HTTPS_PROXY=http://127.0.0.1:12345 #请将'12345'替换为您的代理端口
  ```




