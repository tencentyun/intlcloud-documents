## Operation Scenarios
This document describes how to use the API Gateway component provided by Serverless Framework to quickly create and deploy an API Gateway service/API.

## Prerequisites
You have installed Serverless Framework.

## Directions
### Configuring API Gateway service

Create the `serverless.yml` file locally:

```console
touch serverless.yml
```

 Configure `serverless.yml` as follows: 

```yml
# serverless.yml

component: apigateway # Component name, which is required. `apigateway` is used in this example
name: apigwDemo # Instance name, which is required
org: orgDemo # Organization information, which is optional. The default value is the `appid` of your Tencent Cloud account
app: appDemo # Next.js application name, which is optional
stage: dev # Information for identifying environment, which is optional. The default value is `dev`

inputs:
  region: ap-guangzhou
  protocols:
    - http
    - https
  serviceName: serverless
  environment: release
  endpoints:
    - path: /
      protocol: HTTP
      method: GET
      apiName: index
      function:
        functionName: myFunction
```

[Detailed Configuration >>](https://github.com/serverless-components/tencent-apigateway/blob/master/docs/configure.md)

### Deploying API Gateway service

Run the following command to deploy by scanning code:

```console
sls deploy
```

>?To grant persistent permission, please see [Account Configuration](#account).

### Removing deployed service

You can run the following command to remove the deployed service:

```console
sls remove
```

<span id="account"></span>
### Account configuration (optional)

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:

```shell
touch .env # Tencent Cloud configuration information
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