## Operation Scenarios
**Tencent Cloud [Next.js](https://github.com/zeit/next.js) component** uses [**Tencent Serverless Framework**](https://github.com/serverless/components/tree/cloud) to implement "zero" configuration, convenient development, and rapid deployment of your webpage application in the Next.js framework based on Tencent Cloud Serverless services (API Gateway, SCF, etc.). The Next.js component supports a rich set of configuration extensions and provides easy-to-use, practical, and cost-effective development/hosting capabilities for webpage application projects.

Next.js features:
- **Pay-as-you-go billing**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **"Zero" configuration**: you only need to write project code and then directly deploy it, and Serverless Framework will take care of all the configuration work.
- **Fast deployment**: you can deploy your entire application in just a few seconds.
- **Real-time log**: you can view the business status through the output of the real-time log, which makes it easy for you to develop applications directly in the cloud.
- **Cloud debugging**: you can directly debug your project in the cloud to avoid problems caused by differences from the local environment.
- **Convenient collaboration**: the status information and deployment logs in the cloud-based console make multi-person collaborative development easier.


## Prerequisites
- You have installed Node.js (for detailed directions, please see [Node.js Installation Guide](https://nodejs.org/zh-cn/download/)).
- You have created and initialized a Next.js project locally.
```bash
$ mkdir serverless-next && cd serverless-next
$ npm init next-app src
```

>You are recommended to use Node.js 10.0 or above; otherwise, Component v2 may report errors during deployment.

## Directions
### 1. Install
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:
```bash
$ npm install -g serverless
```

### 2. Configure
Create a `serverless.yml` file in the project root directory (which is `serverless-next` in this example):
```bash
$ touch serverless.yml
```
Configure `serverless.yml` as follows:
```yml
# serverless.yml
component: nextjs # Component name, which is required. `nextjs` is used in this example
name: nextjsDemo # Instance name, which is required
org: orgDemo # Organization information, which is optional. The default value is the `appid` of your Tencent Cloud account
app: appDemo # Next.js application name, which is optional
stage: dev # Information for identifying environment, which is optional. The default value is `dev`

inputs:
  src: 
	src: ./src
    exclude:
      - .env
  functionName: nextjsDemo
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

Enter the Next.js project directory and construct static resources:

```bash
$ cd src && npm run build
```

#### 3.2. Deploy into the cloud
Go back to the project root directory where the `serverless.yml` file is and run the following command for deployment:
```bash
$ sls deploy
```
Authentication is required during deployment. If you have not [logged in to](https://intl.cloud.tencent.com/login) or [signed up for](https://intl.cloud.tencent.com/register) a Tencent Cloud account, please log in or sign up first.

>If you want to view more information on the deployment process, you can run the `sls deploy --debug` command to view the real-time log information during the deployment process (`sls` is an abbreviation for the `serverless` command).

### 4. Debug
After the Next.js application is deployed, the project can be further developed through the debugging feature to create an application for the production environment. After modifying and updating the code locally, you don't need to run the `serverless deploy` command every time for repeated deployment. Instead, you can run the `serverless dev` command to directly detect and automatically upload changes in the local code.
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
```text
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
>
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

### Architecture
The Next.js component will use the following Serverless services in your Tencent Cloud account:

- **API Gateway**: it will receive external requests and forward them to the SCF function.
- **SCF**: it will carry the Next.js application.
- **CAM**: this component will create a default CAM role for authorizing access to associated resources.
- **COS**: to ensure the upload speed and quality, when the function is compressed and the code is uploaded, the code package will be stored in a specifically named COS bucket by default.
- **SSL Certificates Service**: if you configure the `domain` field in the YAML file, you will need to bind a custom domain name and enable HTTPS; therefore, you will also need to use the certificate management service and domain name service. Serverless Framework will automatically apply for and configure an SSL certificate based on the domain name with ICP filing (required for Mainland China service).

### More components
You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).

### FAQs
**Why is an entry file no longer needed?**
In the previous version, to use this component, you need to add an `sls.js` file in the project root directory. In the current version, this is taken care of by the component, so you do not need to deal with it separately. For more information, please see the [GitHub documentation](https://github.com/serverless-components/tencent-nextjs/issues/1).
