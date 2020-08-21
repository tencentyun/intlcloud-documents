## Operation Scenarios
**Tencent Cloud Express component** uses [Tencent Serverless Framework](https://github.com/serverless/components/tree/cloud). Based on serverless services (gateways, functions, etc.) in the cloud, it can implement "zero" configuration, convenient development, and rapid deployment of your Express application. The Express component supports a rich set of configuration extensions and provides the easiest-to-use, low-cost, and elastically scalable cloud-based Express project development and hosting capabilities.

Express.js features:
- **Pay-as-you-go billing**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **"Zero" configuration**: you only need to write project code and then deploy it, and the Serverless Framework will take care of all the configuration work.
- **Fast deployment**: you can deploy your entire Express application in just a few seconds.
- **Real-time log**: you can view the business status through the output of the real-time log, which makes it easy for you to develop applications directly in the cloud.
- **Cloud debugging**: it supports quick cloud debugging for the Node.js framework, which shields differences in the local environment.
- **Convenient collaboration**: the status information and deployment logs in the cloud make multi-person collaborative development easier.
- **Custom domain name**: it supports configuration of custom domain names and HTTPS access.

## Prerequisites
You have installed Node.js (for detailed directions, please see [Node.js Installation Guide](https://nodejs.org/zh-cn/download/)).

>!You are recommended to use Node.js 10.0 or above; otherwise, Component v2 may report errors during deployment.

## Directions
#### 1. Install

Install the latest version of Serverless Framework through npm:
```
$ npm install -g serverless
```

#### 2. Create

Create a directory and enter it:
```
$ mkdir tencent-express && cd tencent-express
```

Use the following command and template link to quickly create an Express application:
```
$ serverless create --template-url https://github.com/serverless-components/tencent-express/tree/master/example
$ cd example
```

Run the following command to install the corresponding dependencies of the Express application:
```
$ npm install
```

#### 3. Deploy

Run `sls deploy` in the directory under the `serverless.yml` file to deploy the Express project. The first deployment may take a relatively long time, but subsequent deployments can be completed within a few seconds. After the deployment, you can view the URL address of your Express application in the output on the command line. Then, you can click the address to access your Express project.
```
$ sls deploy

Please scan QR code login from wechat. 
Wait login...
Login successful for TencentCloud. 

serverless ⚡ framework
Action: "deploy" - Stage: "dev" - App: "appDemo" - Instance: "expressDemo"

region: ap-guangzhou
apigw: 
  serviceId:   service-xxxxxxxx
  subDomain:   service-xxxxxxxx-1250000000.gz.apigw.tencentcs.com
  environment: release
  url:         https://service-xxxxxxxx-1250000000.gz.apigw.tencentcs.com/release/
scf: 
  functionName: expressDemo
  runtime:      Nodejs10.15
  namespace:    default

23s › expressDemo › Success
```
>!
>- If an "internal server error" occurs, please check whether `npm install` was run after the template was created.
>- If you want to view more information on the deployment process, you can run the `sls deploy --debug` command to view the real-time log information during the deployment process (`sls` is an abbreviation for the `serverless` command).


#### 4. Configure

The Express component supports "zero" configuration deployment, that is, it can be deployed directly through the default values in the configuration file. Nonetheless, you can also modify more optional configuration items to further customize your project.

The following is the complete configuration description for `serverless.yml` of the Express component:
```yml
# serverless.yml

component: express # Name of the imported component, which is required. The `express-tencent` component is used in this example
name: express-api # Name of the instance created by this Express component, which is required
org: test # Organization information, which is optional. The default value is the `appid` of your Tencent Cloud account
app: expressApp # Express application name, which is optional
stage: dev # Information for identifying environment, which is optional. The default value is `dev`

inputs:
  region: ap-guangzhou
  functionName: express-api
  serviceName: mytest
  runtime: Nodejs8.9
  serviceId: service-np1uloxw
  src: ./src
  functionConf:
    timeout: 10
    memorySize: 128
    environment:
      variables:
        TEST: vale
  apigatewayConf:
    customDomains:
      - domain: abc.com
        certificateId: abcdefg
        isDefaultMapping: 'FALSE'
        pathMappingSet:
          - path: /
            environment: release
        protocols:
          - http
          - https
```

View the [complete configuration and configuration description >>](https://github.com/serverless-components/tencent-express/blob/master/docs/configure.md)

After you update the configuration fields according to the configuration file, run `serverless deploy` or `serverless` again to update the configuration to the cloud.

#### 5. Debug

After the Express.js application is deployed, the project can be further developed through the debugging feature to create an application for the production environment. After modifying and updating the code locally, you don't need to run the `serverless deploy` command every time for repeated deployment. Instead, you can run the `serverless dev` command to directly detect and automatically upload changes in the local code.

You can enable debugging by running the `serverless dev` command in the directory where the `serverless.yml` file is located.

`serverless dev` also supports real-time outputting of cloud logs. After each deployment, you can access the project to output invocation logs in real time on the command line, which makes it easy for you to view business conditions and troubleshoot issues.

Currently, in addition to real-time log output, for Node.js applications, cloud debugging is also supported. After the `serverless dev` command is started, it will automatically listen on the remote port and set the function timeout period to 900 seconds temporarily. At this point, you can find the remote debugging path by accessing `chrome://inspect/#devices` and directly debug the code with breakpoints. After the debugging mode ends, you need to deploy the function again to update the code and set the timeout period back to the original value. 

#### 6. Check status

In the directory where the `serverless.yml` file is located, run the following command to check the deployment status:

```
$ serverless info
```

#### 7. Remove

In the directory where the `serverless.yml` file is located, run the following command to remove the deployed Express service. After removal, this component will delete all related resources created during deployment in the cloud.
```
$ serverless remove
```

Similar to the deployment process, you can run the `sls remove --debug` command to view real-time log information during the removal process (`sls` is an abbreviation for the `serverless` command).

## Architecture

The Express component will use the following Serverless services in your Tencent Cloud account:

- **API Gateway**: it will receive external requests and forward them to the SCF function.
- **SCF**: it will carry the Express.js application.
- **CAM**: this component will create a default CAM role for authorizing access to associated resources.
- **COS**: to ensure the upload speed and quality, when the function is compressed and the code is uploaded, the code package will be stored in a specifically named COS bucket by default.
- **SSL Certificates Service**: if you configure the `domain` field in the YAML file, you will need to bind a custom domain name and enable HTTPS; therefore, you will also need to use the certificate management service and domain name service. Serverless Framework will automatically apply for and configure an SSL certificate based on the domain name. If the domain name is used for Mainland China service, ICP filing is required.

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
