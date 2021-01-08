
## Overview
Tencent Cloud [Egg.js](https://github.com/eggjs/egg) Serverless Component supports deploying RESTful API services.

## Prerequisites

#### Initialize Egg.js project
```shell
$ mkdir serverless-egg && cd serverless-egg
$ npm init egg src --type=simple
$ cd src && npm install
```


## Directions
### 1. Install
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:
```shell
$ npm install -g serverless
```

### 2. Configure
Create a `serverless.yml` file in the project root directory:
```shell
$ touch serverless.yml
```
Configure the `serverless.yml` file as follows (for more information on the configuration of the .yml file, please see [Configuration Information](https://github.com/serverless-components/tencent-egg/blob/master/docs/configure.md)):
```yml
component: egg
name: eggDemo
app: appDemo

inputs:
  src: ./
  region: ap-guangzhou
  runtime: Nodejs10.15
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```

### 3. Deploy

If you have not [logged in to](https://intl.cloud.tencent.com/login) or [signed up for](https://intl.cloud.tencent.com/register) a Tencent Cloud account, you can directly log in or sign up by scanning the QR code on the command line with **WeChat**.

Deploy by running the `sls deploy` command, and you can add the `--debug` parameter to view the information during the deployment process:
>?`sls` is short for the `serverless` command.

```shell
$ sls deploy

  MyComponent: 
    region:              ap-beijing
    functionName:        egg-function
    apiGatewayServiceId: service-n5m5e8x3
    url:                 https://service-n5m5e8x3-1251971143.bj.apigw.tencentcs.com/release/

  32s › MyComponent › done
```

### 4. Remove

You can run the following commands to remove the deployed API Gateway and SCF services:
```shell
$ sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Removing function
  DEBUG ─ Request id
  DEBUG ─ Removed function egg-function successful
  DEBUG ─ Removing any previously deployed API. api-cmkhknda
  DEBUG ─ Removing any previously deployed service. service-n5m5e8x3

  8s › MyComponent › done

```

### Account configuration (optional)

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:

```shell
$ touch .env # Tencent Cloud configuration information
```

Configure Tencent Cloud's `SecretId` and `SecretKey` information in the `.env` file and save it:
```text
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
>?
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

## More Resources
### FAQs

1. **What should I do if the `app/public` deployment directory does not exist?**

   Generally, when you initialize an Egg.js project, the `app/public` directory will be created automatically. If this directory is empty during packaging and compressing, it will not exist after the deployment; instead, it will automatically be created when the Egg.js project is started; however, SCF will not have the permission to manipulate it. Therefore, we recommend you create an empty folder `.gitkeep` in the `app/public` directory to solve this problem.

2. **What should I do if a failure to find the dependent module is reported after deployment with Layer?**

   For more information, please see [here](https://github.com/serverless-components/tencent-egg/issues/11#issue-618169731).

### More components
You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).
