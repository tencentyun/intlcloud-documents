## Operation Scenarios
This document describes how to quickly create, configure, and deploy a serverless application in Tencent Cloud through Serverless Framework.
>?
>- Serverless Framework provides a [visual UI](https://serverless.cloud.tencent.com/) where you can view and manage resources at the serverless application level.
>- Serverless Framework v2 Component has been released, which is recommended as the latest version.

## Prerequisites
- Before use, please make sure that [Serverless Framework 1.67.2 or above has been installed](https://intl.cloud.tencent.com/document/product/1040/37034).
- If your Tencent Cloud account is a root account, you can directly proceed with the deployment. If your account is a sub-account, please get the authorization first before deployment as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

## Directions

Enter the `serverless` command in an empty folder and follow the instructions to deploy an SCF, Express.js, or static website hosting application. The interaction process is as follows:

```
$ serverless
Serverless: No serverless project is detected. Do you want to create one? (Y/n) y
Serverless: Please select the serverless application you want to create (Use arrow keys)
❯ Express.js app 
  SCF Function 
  Website app 
Serverless: Please enter the project name "express-app"

The "express-app" project has been created successfully!
Serverless: Do you want to deploy the project in the cloud now? (Y/n) y
Please scan QR code login from wechat. 
Wait login...
Login successful for TencentCloud. 

serverless ⚡ framework
Action: "deploy" - Stage: "dev" - App: "scfApp" - Instance: "scfdemo"

FunctionName: scfFunctionName
Description:  
Namespace:    default
Runtime:      Nodejs10.15
Handler:      index.main_handler
MemorySize:   128
Triggers: 
  apigw: 
    - https://service-9k0ggfbe-1250000000.gz.apigw.tencentcs.com/release/index

23s › scfdemo › Success
```

After the deployment is completed, visit the webpage link output on the command line to access the successfully deployed application.
>?If you want to view details during the deployment process, you can add the `--debug` parameter.


### Viewing deployment information

If you want to check the deployment status and resources of the application again, you can go to the folder where the project is successfully deployed and run the following command to view the corresponding information:

```
$ cd express-app # Enter the project directory
$ sls info
```
>?`sls` is short for the `serverless` command.

### Development and debugging

By running the `sls dev` command, you can enable real-time logging of the deployment. This feature will automatically monitor local code updates, sync them to the cloud for deployment, and output invocation logs in real time. For applications on Node.js 10, you can also enable in-cloud debugging. For more information, please see [In-cloud Debugging for Node.js(https://intl.cloud.tencent.com/document/product/1040/36860).

```
$ cd express-app
$ sls dev
```

### Removing project

You can remove all resources deployed in the cloud by running the `sls remove` command as follows:

```
$ cd express-app # Enter the project directory
$ sls remove

serverless ⚡ framework
Action: "remove" - Stage: "dev" - App: "scfApp" - Instance: "scfdemo"

6s › scfdemo › Success
```

>?If you want to view the details during the removal process, you can add the `--debug` parameter.

### Configuring account information (optional)

If you want to configure persistent environment variables/key information, please see [Configuring Account](https://intl.cloud.tencent.com/document/product/1040/36793).

## FAQs
If a proxy is configured in your environment, the following problems may occur:

- Problem 1: the guide does not pop up by default when `serverless` is entered.
Solution: add the `SERVERLESS_PLATFORM_VENDOR=tencent` configuration item to the `.env` file.

- Problem 2: after `sls deploy` is entered, the deployment reports a network error.
Solution: add the following proxy configuration to the `.env` file.
```
HTTP_PROXY=http://127.0.0.1:12345 # Your proxy
HTTPS_PROXY=http://127.0.0.1:12345 # Your proxy
```

  

