## Overview

This task shows you how to use Serverless Framework to quickly create, configure, and deploy a Serverless application on Tencent Cloud.

> ?
> - Serverless Framework provides a [Visualized Page](https://serverless.cloud.tencent.com/) for you to view and manage the resources of a Serverless application.
> - Serverless Framework Component V2 has been released. We advise you to use the latest version.

## Prerequisites

- Ensure that [Serverless Framework 1.67.2 or later](https://intl.cloud.tencent.com/document/product/1040/37034) has been installed in advance.
- If your Tencent Cloud account is the root account, you can continue implementing deployment. If your account is a sub-account, please go to [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793) to get permission before implementing deployment.

## Directions 
### Creating an Application
You can run the `sls init` command to quickly create an SCF, Express.js, or static website hosting application. For example, to create an Express.js application:

```
sls init express-demo
```

>? You can run the `sls registry` command to view the supported demo. 

Go to the `express-demo` directory and perform deployment:

```
cd express-demo && sls deploy
```



After the deployment is completed, visit the URL returned from the CLI to access the deployed application.

> ?To view the detailed information during deployment, you can add the `--debug` parameter.

### Viewing the Deployment Information

To view the application deployment statuses and resources again, go to the directory that is successfully deployed and run the following command:

```
$ cd express-app #Go to the project directory.
$ sls info
```

> ?`sls` is short for the `serverless` command.

### Developing and Debugging

Run the `sls dev` command to enable the real-time deployment log. This capability automatically detects the updates of the local code and deploys the updates on cloud. In addition, the invoked log can be output in real time. For a Node.js 10 application, cloud debugging is available. For more information, please see “In-cloud Debugging: Node.js 10+” in [Development Mode and In-cloud Debugging](https://intl.cloud.tencent.com/document/product/1040/36860)

```
$ cd express-app
$ sls dev
```

### Removing the Project

Run the `sls remove` command to remove all on-cloud resources, as shown below:

```
$ cd express-app #Go to the project directory.
$ sls remove

serverless ⚡ framework
Action: "remove" - Stage: "dev" - App: "scfApp" - Instance: "scfdemo"

6s › scfdemo › Success
```

> ?To view the detailed information during removal, you can add the `--debug` parameter.

### Configuring Account Information (Optional)

To configure persistent environment variables or key information, please refer to [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

## FAQs

- Question 1: What do I do if instructions are not displayed when I enter `serverless`?
  Solution: Add the `SERVERLESS_PLATFORM_VENDOR=tencent` configuration to the `.env` file.
	
- Question 2: What do I do if the deployment with an overseas network is very slow after I enter `sls deploy`?
  Solution: Add the `GLOBAL_ACCELERATOR_NA=true` configuration to the `.env` file to accelerate the overseas network.
	
- Question 3: What do I do if network error occurs during deployment after I enter `sls deploy`?
  Solution: Add the following proxy configurations to the `.env` file.
```
HTTP_PROXY=http://127.0.0.1:12345 #Your proxy
HTTPS_PROXY=http://127.0.0.1:12345 #Your proxy
```

  

