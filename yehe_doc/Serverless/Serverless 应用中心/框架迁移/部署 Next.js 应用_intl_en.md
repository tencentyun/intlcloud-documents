## Overview
Tencent Cloud [Next.js](https://github.com/zeit/next.js) component uses [Tencent Serverless Framework](https://github.com/serverless/components/tree/cloud) to implement "zero" configuration, convenient development, and rapid deployment of your webpage application in the Next.js framework based on Tencent Cloud Serverless services (API Gateway, SCF, etc.). The Next.js component supports a rich set of configuration extensions and provides easy-to-use, practical, and cost-effective development/hosting capabilities for webpage application projects.

Next.js features:
- **Pay-as-you-go billing**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **"Zero" configuration**: you only need to write project code and then directly deploy it, and Serverless Framework will take care of all the configuration work.
- **Fast deployment**: you can deploy your entire application in just a few seconds.
- **Real-time log**: you can view the business status through the output of the real-time log, which makes it easy for you to develop applications directly in the cloud.
- **Cloud debugging**: you can directly debug your project in the cloud to avoid problems caused by differences from the local environment.
- **Convenient collaboration**: the status information and deployment logs in the cloud-based console make multi-person collaborative development easier.


## Migration Prerequisites

- [Serverless Framework 1.67.2 or above](https://intl.cloud.tencent.com/document/product/1040/37034) has been installed.
- You have [registered a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/10495).

>?If your account is a **Tencent Cloud sub-account**, please get the authorization from the root account first as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

## Architecture

The Next.js component will use the following Serverless services in your Tencent Cloud account:

- **API Gateway**: it will receive external requests and forward them to the SCF function.
- **SCF**: it will carry the Next.js application.
- **CAM**: this component will create a default CAM role for authorizing access to associated resources.
- **COS**: to ensure the upload speed and quality, when the function is compressed and the code is uploaded, the code package will be stored in a specifically named COS bucket by default.

## Directions

>?The following steps are mainly for deployment on the command line. For deployment in the console, please see [Console Deployment Guide](https://intl.cloud.tencent.com/document/product/1040/39132).

### 1. Initialize the Next.js template project (optional)
If you don't have a local Next.js project, you can quickly create a Next.js project template with the following command (if you already have one, you can ignore this step):
```
serverless init nextjs-starter --name example
cd example
```

### 2. Modify the entry function code (optional)
If the project uses a custom Node.js service, such as the Express or Koa framework, you need to modify the entry file `sls.js` (or `app.js`) and export the corresponding framework application (otherwise, you can skip this step). Click [here](#1) to view the modification template.


### 3. Build the project
```
npm run build
```

### 4. Generate a .yml file and deploy

After modifying the code, you can run the `sls deploy` command, and Serverless Framework will automatically generate a basic `serverless.yml` file and complete the deployment to quickly migrate the Next.js framework application.

The generated default configuration file is as follows:
```yml
component: nextjs
name: nextjsDemo
app: appDemo

inputs:
  src: ./
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
After the deployment is completed, access the application by accessing the output API Gateway link.

### 5. View deployment status

In the directory where the `serverless.yml` file is located, run the following command to check the deployment status:

```
$ serverless info
```


<span id="1"></span>
## Modification Template for Project Migration
- Express template

```js
const express = require('express')
const next = require('next')

// not report route for custom monitor
const noReportRoutes = ['/_next', '/static', '/favicon.ico']

async function createServer() {
  const app = next({ dev: false })
  const handle = app.getRequestHandler()

  await app.prepare()

  const server = express()
  server.all('*', (req, res) => {
    noReportRoutes.forEach((route) => {
      if (req.path.indexOf(route) !== -1) {
        req.__SLS_NO_REPORT__ = true
      }
    })
    return handle(req, res)
  })

  // define binary type for response
  // if includes, will return base64 encoded, very useful for images
  server.binaryTypes = ['*/*']

  return server
}

module.exports = createServer
```

- Koa template
```js
const Koa = require('koa')
const next = require('next')

async function createServer() {
  const app = next({ dev: false })
  const handle = app.getRequestHandler()

  const server = new Koa()
  server.use((ctx) => {
    ctx.status = 200
    ctx.respond = false
    ctx.req.ctx = ctx

    return handle(ctx.req, ctx.res)
  })

  // define binary type for response
  // if includes, will return base64 encoded, very useful for images
  server.binaryTypes = ['*/*']

  return server
}

module.exports = createServer
```

### Custom monitoring

When you deploy the Next.js application, if you don't specify the `role` in `serverless.yml`, the system will try to bind `QCS_SCFExcuteRole` by default and enable custom monitoring to help you collect the statistics of application metrics. For projects with custom entry files, routes except those with `/_next` and `/static` will be reported by default.

If you want to report the performance of custom routes, you can customize the `sls.js` entry file.
For routes that do not need to be reported, set the `__SLS_NO_REPORT__` attribute value to `true` in the `req` object of the Express service; for example:
```js
server.get('/no-report', (req, res) => {
  req.__SLS_NO_REPORT__ = true
  return handle(req, res)
})
```
After configuration, custom monitoring metrics will not be reported when users access the `GET /no-report` route.



## More Resources
### Account configuration
Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:
```bash
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


### More components
You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).

### FAQs
**Why is an entry file no longer needed?**
In the previous version, to use this component, you need to add an `sls.js` file in the project root directory. In the current version, this is taken care of by the component, so you do not need to deal with it separately. For more information, please see the [GitHub documentation](https://github.com/serverless-components/tencent-nextjs/issues/1).

