## Operation Scenarios

**Tencent Cloud [Nuxt.js](https://github.com/nuxt/nuxt.js) component** uses [**Tencent Serverless Framework**](https://github.com/serverless/components/tree/cloud) to implement "zero" configuration, convenient development, and rapid deployment of your webpage application in the Nuxt.js framework based on Tencent Cloud Serverless services (API Gateway, SCF, etc.). The Nuxt.js component supports a rich set of configuration extensions and provides easy-to-use, practical, and cost-effective development/hosting capabilities for webpage application projects.

Features:
- **Pay-as-you-go billing**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **"Zero" configuration**: you only need to write project code and then directly deploy it, and Serverless Framework will take care of all the configuration work.
- **Fast deployment**: you can deploy your application in just a few seconds.
- **Real-time log**: you can view the business status through the output of the real-time log, which makes it easy for you to develop applications directly in the cloud.
- **Cloud debugging**: you can directly debug your project in the cloud to avoid problems caused by differences from the local environment.
- **Convenient collaboration**: the status information and deployment logs in the cloud-based console make multi-person collaborative development easier.


## Prerequisites

#### Initialize Nuxt.js project

Create a root directory and initialize a Nuxt.js project locally:
```bash
$ mkdir serverless-nuxtjs && cd serverless-nuxtjs
$ npx create-nuxt-app src
```
>!The Nuxt project in this tutorial is built with JavaScript and the npm installation package. Please select the appropriate options when initializing the project.

>!You are recommended to use Node.js 10.0 or above; otherwise, Component v2 may report errors during deployment.

## Directions
### 1. Install
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:
```bash
$ npm install -g serverless
```

### 2. Configure
Create a `serverless.yml` file in the project root directory:
```bash
$ touch serverless.yml
```
Configure `serverless.yml` as follows:
```yml
# serverless.yml
component: nuxtjs # Component name, which is required. `nuxtjs` is used in this example
name: nuxtjsDemo # Instance name, which is required
org: orgDemo # Organization information, which is optional. The default value is the `APPID` of your Tencent Cloud account.
app: appDemo # Nuxt.js application name, which is optional
stage: dev # Information for identifying environment, which is optional. The default value is `dev`

inputs:
  src:
    src: ./src
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

View [more configurations and descriptions >>](https://github.com/serverless-components/tencent-nextjs/tree/master/docs/configure.md)

### 3. Deploy
#### 3.1. Construct static resources

Enter the Nuxt.js project directory and construct static resources:
```bash
$ cd src && npm run build
```

#### 3.2. Deploy into the cloud

Go back to the project root directory where the `serverless.yml` file is and run the following command for deployment:
```bash
# Enter the project directory `serverless-nuxtjs`
$ sls deploy

serverless ⚡ framework
Action: "deploy" - Stage: "dev" - App: "appDemo" - Instance: "nuxtjsDemo"

region: ap-guangzhou
apigw:
  serviceId:   service-4v2jx72g
  subDomain:   service-4v2jx72g-1258834142.gz.apigw.tencentcs.com
  environment: release
  url:         https://xxxxxx.gz.apigw.tencentcs.com/release/
scf:
  functionName: nuxtjs_component_mm518kl
  runtime:      Nodejs10.15
  namespace:    default

139s › nuxtjsDemo › Success
```


>?If you want to view more information on the deployment process, you can run the `sls deploy --debug` command to view the real-time log information during the deployment process (`sls` is an abbreviation for the `serverless` command).


### 4. Debug

After the Nuxt.js application is deployed, the project can be further developed through the debugging feature to create an application for the production environment. After modifying and updating the code locally, you don't need to run the `serverless deploy` command every time for repeated deployment. Instead, you can run the `serverless dev` command to directly detect and automatically upload changes in the local code.
You can enable debugging by running the `serverless dev` command in the directory where the `serverless.yml` file is located.
`serverless dev` also supports real-time outputting of cloud logs. After each deployment, you can access the project to output invocation logs in real time on the command line, which makes it easy for you to view business conditions and troubleshoot issues.

### 5. View deployment status

In the directory where the `serverless.yml` file is located, run the following command to check the deployment status:

```
$ serverless info
```

### 6. Remove

In the directory where the `serverless.yml` file is located, run the following command to remove the deployed API gateway. After removal, this component will delete all related resources created during deployment in the cloud.

```bash
$ sls remove
```
Similar to the deployment process, you can run the `sls remove --debug` command to view real-time log information during the removal process (`sls` is an abbreviation for the `serverless` command).

## More Resources
### Account configuration

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:
```bash
$ touch .env # Tencent Cloud configuration information
```

Configure Tencent Cloud's `SecretId` and `SecretKey` information in the `.env` file and save it:
>?
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

```text
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
>!When logging in with an IP outside Mainland China, you need to add `SERVERLESS_PLATFORM_VENDOR=tencent` in the `.env` file to make `sls` use the `tencent` component by default.

### More components

You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).

### FAQs
**Why is an entry file no longer needed?**
In the previous version, to use this component, you need to add an `sls.js` file in the project root directory. In the current version, this is taken care of by the component, so you do not need to deal with it separately. For more information, please see the [GitHub documentation](https://github.com/serverless-components/tencent-nuxtjs/issues/1).

