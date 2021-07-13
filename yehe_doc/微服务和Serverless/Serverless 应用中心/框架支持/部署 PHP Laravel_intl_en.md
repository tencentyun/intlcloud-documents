## Overview
 Tencent Cloud [Laravel](https://github.com/laravel/laravel) Serverless Component supports Laravel v6.0 and above. 



## Directions
### 1. Install Serverless CLI
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:
```shell
npm install -g serverless
```

>?The following steps are mainly for deployment on the command line. For deployment in the console, please see [Console Deployment Guide](https://intl.cloud.tencent.com/document/product/1040/39132).

### 2. Initialize the Laravel template project (optional)
If you don't have a local Laravel project, you can initialize a Laravel project with the following commands (if you already have one, you can ignore this step):
```
serverless init laravel-starter --name example
cd example
```

### 3. Configure the .yml file
Create a `serverless.yml` file in the project root directory:
```sh
touch serverless.yml
```
Paste the following configuration template into the file to implement basic project configuration.
>?You can add more configuration items in `serverless.yml` based on your actual deployment needs. For more information on the configuration of the .yml file, please see [Laravel Component Configuration](https://github.com/serverless-components/tencent-laravel/blob/master/docs/configure.md).
```yml
# serverless.yml

component: laravel
name: laravelDemo
app: appDemo
stage: dev

inputs:
  src: ./
  region: ap-guangzhou
  runtime: Php7
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```

### 4. Deploy the application
Deploy by running the `sls deploy` command, and you can add the `--debug` parameter to view the information during the deployment process:

```
sls deploy --debug
```
After the deployment is completed, access the application by accessing the output API Gateway link.

### 5. Monitor the OPS
After the deployment is completed, you can log in to the [Serverless Framework console](https://console.cloud.tencent.com/ssr) to view the basic information of the application and monitor logs.



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

