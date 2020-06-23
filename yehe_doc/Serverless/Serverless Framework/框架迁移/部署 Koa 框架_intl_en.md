## Operation Scenarios
The Koa component can help you quickly and conveniently create, configure, and manage a [Koa framework](https://koajs.com/) in Tencent Cloud with the aid of the serverless-tencent basic components (such as API Gateway component and SCF component).

>You are recommended to use Node.js 10.0 or above; otherwise, Component v2 may report errors during deployment.

## Directions
Through the SCF component, you can perform a complete set of operations on a Koa application, such as creation, configuration, deployment, and deletion. The supported commands are as follows:

### 1. Install

Install Serverless through npm:
```console
$ npm install -g serverless
```

### 2. Create

1. Create `serverless.yml` and `app.js` files locally.
```console
$ touch serverless.yml
```
2. Initialize a new npm package and install Koa:
```
npm init              # Keep pressing Enter after the creation
npm i --save koa  # Install Koa
```
3. Create an `sls.js` file:
```console
$ touch app.js
```
4. Create your Koa application in the `app.js` file:
```js
const koa = require('koa')
const app = new koa()

app.use(async (ctx, next) => {
  if (ctx.path !== '/') return next()
  ctx.body = 'Hello from Koa'
})

// set binary types
// app.binaryTypes = [*/*];

// don't forget to export!
module.exports = app
```

### 3. Configure

Configure `serverless.yml` as follows:
```yml
# serverless.yml

org: orgDemo # (optional) serverless dashboard org. default is the first org you created during signup.
app: appDemo # (optional) serverless dashboard app. default is the same as the name property.
stage: dev # (optional) serverless dashboard stage. default is dev.
component: koa # (required) name of the component. In that case, it's koa.
name: koaDemo # (required) name of your koa component instance.

inputs:
  src:
    src: ./src # (optional) path to the source folder. default is a hello world app.
    exclude:
      - .env
  region: ap-guangzhou
  runtime: Nodejs10.15
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```
[Detailed Configuration >>](https://github.com/serverless-components/tencent-koa/blob/v2/docs/configure.md)

### 4. Deploy

If you have not [logged in to](https://intl.cloud.tencent.com/login) or [signed up for](https://intl.cloud.tencent.com/register) a Tencent Cloud account:

Deploy by running the `sls deploy` command, and you can add the `--debug` parameter to view the information during the deployment process:
>`sls` is short for the `serverless` command.

```
$ sls deploy

  koa:
    region:              ap-shanghai
    functionName:        KoaComponent_7xRrrd
    apiGatewayServiceId: service-n0vs2ohb
    url:                 http://service-n0vs2ohb-1300415943.ap-shanghai.apigateway.myqcloud.com/release/

  36s › koa › done

```

After completing the deployment, you can access the returned link in a browser to view the corresponding value returned by Koa.

### 5. Remove

Run the following command to remove the deployed application:
```
$ sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Removed function KoaComponent_MHrAzr successful
  DEBUG ─ Removing any previously deployed API. api-kf2hxrhc
  DEBUG ─ Removing any previously deployed service.  service-n0vs2ohb

  13s › koa › done
```

### Account configuration (optional)

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
>
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

## More Components
You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).
