## Overview
**Tencent Cloud Express component** uses [Tencent Serverless Framework](https://github.com/serverless/components/tree/cloud). Based on serverless services (gateways, functions, etc.) in the cloud, it can implement "zero" configuration, convenient development, and rapid deployment of your Express application. The Express component supports a rich set of configuration extensions and provides the easiest-to-use, low-cost, and elastically scalable cloud-based Express project development and hosting capabilities.

Express.js features:
- **Pay-as-you-go billing**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **"Zero" configuration**: you only need to write project code and then deploy it, and the Serverless Framework will take care of all the configuration work.
- **Fast deployment**: you can deploy your entire Express application in just a few seconds.
- **Real-time log**: you can view the business status through the output of the real-time log, which makes it easy for you to develop applications directly in the cloud.
- **Cloud debugging**: it supports quick cloud debugging for the Node.js framework, which shields differences in the local environment.
- **Convenient collaboration**: the status information and deployment logs in the cloud make multi-person collaborative development easier.
- **Custom domain name**: it supports configuration of custom domain names and HTTPS access.

Through the [Serverless Framework Express component](https://github.com/serverless-components/tencent-express), you can quickly migrate traditional local Express applications to the serverless function platform.

## Migration Prerequisites

- [Serverless Framework 1.67.2 or above](https://intl.cloud.tencent.com/document/product/1040/37034) has been installed.
- You have [registered a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/10495).

>?If your account is a **Tencent Cloud sub-account**, please get the authorization from the root account first as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

## Architecture

The Express component will use the following Serverless services in your Tencent Cloud account:

- **API Gateway**: it will receive external requests and forward them to the SCF function.
- **SCF**: it will carry the Express application.
- **CAM**: this component will create a default CAM role for authorizing access to associated resources.
- **COS**: to ensure the upload speed and quality, when the function is compressed and the code is uploaded, the code package will be stored in a specifically named COS bucket by default.
  
## Directions

>?The following steps are mainly for deployment on the command line. For deployment in the console, please see [Console Deployment Guide](https://intl.cloud.tencent.com/document/product/1040/39132).
### 1. Initialize the Express template project (optional)
If you don't have a local Express project, you can quickly create an Express project template with the following command (if you already have one, you can ignore this step):
```
serverless init express-starter --name example
cd example
```

### 2. Modify the project code
Open the entry file `sls.js` (or `app.js`) of the Express project, comment out the local listening port, and export the default Express application:

```javascript
// sls.js

const express = require('express');
const app = express();

// *****

// Comment out the local listening port
// app.listen(3000);

// Export the Express application
module.exports = app;
```

### 3. Generate a .yml file and deploy
After modifying the code, you can run the `sls deploy` command, and Serverless Framework will automatically generate a basic `serverless.yml` file and complete the deployment to quickly migrate the Express framework application.

The generated default configuration file is as follows:
```yml
component: express
name: expressDemo
app: appDemo

inputs:
  entryFile: sls.js # Use the actual entry file name
  src: ./
  region: ap-guangzhou
  runtime: Nodejs10.15
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```

After the deployment is completed, access the application by accessing the output API Gateway link.

### 4. Modify the .yml configuration file

You can add more configuration items in `serverless.yml` based on your actual deployment needs and run `sls deploy` for redeployment.

For more information on the configuration of the .yml file, please see [Express Component Configuration](https://github.com/serverless-components/tencent-express/blob/master/docs/configure.md).

### 5. Monitor the OPS
After the deployment is completed, you can log in to the [Serverless Framework console](https://console.cloud.tencent.com/ssr) to view the basic information of the application and monitor logs.


## Account Configuration

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:

```console
$ touch .env # Tencent Cloud configuration information
```

Configure Tencent Cloud's `SecretId` and `SecretKey` information in the `.env` file and save it:

```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
>?
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

