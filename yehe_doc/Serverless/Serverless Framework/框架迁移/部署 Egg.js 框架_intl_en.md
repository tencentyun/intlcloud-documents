
## Operation Scenarios
Tencent Cloud [Egg.js](https://github.com/eggjs/egg) Serverless Component supports deploying RESTful API services.

## Prerequisites

>You are recommended to use Node.js 10.0 or above; otherwise, Component v2 may report errors during deployment.

#### Initialize Egg.js project
```shell
$ mkdir serverless-egg && cd serverless-egg
$ npm init egg src --type=simple
$ cd src && npm install
```

#### Modify Egg.js configuration

When a function is executed, only `/tmp` is readable/writable; therefore, you need to write the logs of Egg.js framework running attempts into this directory by modify the configuration in `config/config.default.js` to the following:
```js
const config = (exports = {
  rundir: '/tmp',
  logger: {
    dir: '/tmp'
  }
})
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
Configure the `serverless.yml` file as follows:
```yml
# serverless.yml

org: orgDemo
app: appDemo
stage: dev
component: egg@0.0.0-dev
name: eggDemo

inputs:
  src: ./src
  region: ap-guangzhou
  functionName: eggDemo
  runtime: Nodejs10.15
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```

[Detailed Configuration >>](https://github.com/serverless-components/tencent-egg/blob/v2/docs/configure.md)

### 3. Deploy

If you have not [logged in to](https://intl.cloud.tencent.com/login) or [signed up for](https://intl.cloud.tencent.com/register) a Tencent Cloud account:

Deploy by running the `sls deploy` command, and you can add the `--debug` parameter to view the information during the deployment process:
>`sls` is short for the `serverless` command.

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
>
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

#### Notes

Generally, when you initialize an Egg.js project, the `app/public` directory will be created automatically. If this directory is empty during packaging and compressing, it will not exist after the deployment; instead, it will automatically be created when the Egg.js project is started; however, SCF will not have the permission to manipulate it. Therefore, you are recommended to create an empty folder `.gitkeep` in the `app/public` directory to solve this problem.

## More Components
You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).
