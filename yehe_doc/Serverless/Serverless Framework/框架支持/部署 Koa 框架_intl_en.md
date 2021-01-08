## Overview
The Koa component can help you quickly and conveniently create, configure, and manage a [Koa framework](https://koajs.com/) in Tencent Cloud with the aid of the serverless-tencent basic components (such as API Gateway component and SCF component).

>!We recommend you use Node.js 10.0 or above; otherwise, Component v2 may report errors during deployment.

## Migration Prerequisites

- [Serverless Framework 1.67.2 or above](https://intl.cloud.tencent.com/document/product/1040/36249) has been installed.
- You have [registered a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/10495).

>?If your account is a **Tencent Cloud sub-account**, please get the authorization from the root account first as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

## Directions
>?The following steps are mainly for deployment on the command line. For deployment in the console, please see [Console Deployment Guide](https://intl.cloud.tencent.com/document/product/1040/39132).

### 1. Initialize the Koa template project (optional)
If you don't have a local Koa project, you can quickly create a Koa project template with the following command (if you already have one, you can ignore this step):
```
serverless init koa-starter --name example
cd example
```

### 2. Modify the project code
Open the entry file `sls.js` (or `app.js`) of the Koa project, comment out the local listening port, and export the default Koa application:

```javascript
// sls.js

const koa = require('koa');
const app = koa();

// *****

// Comment out the local listening port
// app.listen(3000);

// Export the Koa application
module.exports = app;
```

### 3. Generate a .yml file and deploy
After modifying the code, you can run the `sls deploy` command, and Serverless Framework will automatically generate a basic `serverless.yml` file and complete the deployment to quickly migrate the Koa framework application.

The generated default configuration file is as follows:
```yml
component: koa
name: koaDemo
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

### 4. Modify the .yml file

You can add more configuration items in `serverless.yml` based on your actual deployment needs and run `sls deploy` for redeployment.

For more information on the configuration of the .yml file, please see [Koa Component Configuration](https://github.com/serverless-components/tencent-koa/blob/master/docs/configure.md).

### 5. Monitor the OPS
After the deployment is completed, you can log in to the [SSR console](https://console.cloud.tencent.com/ssr) to view the basic information of the application and monitor logs.

### Account configuration (optional)

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:
```console
touch .env # Tencent Cloud configuration information
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

## More Components
You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).
