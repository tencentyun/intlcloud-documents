## Operation Scenarios
This document describes how to use the SCF component provided by Serverless Framework to quickly create and deploy an SCF project. To learn more about components and how to use them, please see [Components Overview](https://intl.cloud.tencent.com/document/product/1040/33163).
>?SCF CLI has been disused since February 2020. We recommend you use the more rich-featured and convenient Serverless Framework CLI for project development.
>


## Directions
### Installing Serverless Framework
On the command line, run the following command to install the latest version of Serverless Framework through npm.
```
npm install -g serverless
```

### Creating function directory
1. Run the following command to create a directory and enter it (this document uses `tencent-scf` as an example):
```
mkdir tencent-scf && cd tencent-scf
```
2. Run the following commands in sequence to quickly create an SCF application:
```
serverless create --template-url https://github.com/serverless-components/tencent-scf/tree/master/example
```
```
cd example
```
After the application is created successfully, its directory structure is as follows
```
|- src
|   └── index.js
└──  serverless.yml
```

### Deploying function
1. In the directory where `serverless.yml` is located, run the following command to deploy the function:
```
serverless deploy
```
2. If you want to configure persistent environment variables or key information, please do so as instructed in [Account configuration](#accountConfiguration).
After the function is deployed successfully, you can view the URL provided by the gateway trigger of the corresponding function in the command line output and access the URL in a browser to view the function deployment result.
>?If you want to view more information on the deployment process, you can run the `sls deploy --debug` command to view the real-time log information during the deployment process (`sls` is an abbreviation for the `serverless` command).
>


### Configuring deployment
The SCF component supports "zero" configuration deployment, that is, it can be deployed directly with the default values in the configuration file. Nonetheless, you can also modify more optional configuration items as needed to further customize the project to be deployed.

The following is the description of the SCF component configuration file `serverless.yml`. For more information, please see [Full Configuration and Configuration Description](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md).
```yml
# serverless.yml
component: scf # Name of the imported component, which is required. The `tencent-scf` component is used in this example
name: scfdemo # Name of the instance created by this component, which is required
org: test # Organization information, which is optional. The default value is the `appid` of your Tencent Cloud account
app: scfApp # SCF application name, which is optional
stage: dev # Information for identifying environment, which is optional. The default value is `dev`
inputs:
  name: scfFunctionName
  src: ./src
  runtime: Nodejs10.15 # Runtime environment of function. Valid values: Python2.7, Python3.6, Nodejs6.10, Nodejs8.9, Nodejs10.15, Nodejs12.16, PHP5, PHP7, Golang1, Java8
  region: ap-guangzhou
  handler: index.main_handler
  events:
    - apigw:
        name: serverless_api
        parameters:
          protocols:
            - http
            - https
          serviceName:
          description: The service of Serverless Framework
          environment: release
          endpoints:
            - path: /index
              method: GET
```
After updating the fields in the configuration file, run the `serverless deploy` or `serverless` command again to update the configuration to the cloud.

### Development and debugging
After deploying the function, you can use the development and debugging capabilities provided by the component to re-develop the project into a production-ready application.

#### Development mode
In the directory where the `serverless.yml` file is located, run the following command to enter the development mode:
```
serverless dev
```
After the local code is modified or updated, there is no need to repeatedly run the `serverless deploy` command for deployment again. After entering the development mode, the component can detect and automatically upload changes to the local code.
`serverless dev` also supports real-time outputting of cloud logs. After each deployment, you can access the project to output invocation logs in real time on the command line, which makes it easy for you to view business conditions and troubleshoot issues.

#### In-cloud debugging
For Node.js applications, the component supports in-cloud debugging. Once in the development mode, it will automatically listen on the remote port and set the function timeout period to 900 seconds temporarily. At this point, you can find the remote debugging path by accessing `chrome://inspect/#devices` and directly debug the code with breakpoints. After the debugging ends, you need to deploy the function again to update the code and reset the timeout period. For more information, please see [Development Mode and In-cloud Debugging](https://intl.cloud.tencent.com/document/product/583/36268).



### Viewing deployment status

In the directory where the `serverless.yml` file is located, you can run the following command to check the deployment status:
```
serverless info
```

### Removing application
In the directory where the `serverless.yml` file is located, run the following command to remove the deployed SCF application. After removal, this component will delete all related resources created during deployment in the cloud.
```
serverless remove
```
>?You can run the `sls remove --debug` command to view real-time log information during the removal process (`sls` is short for the `serverless` command).


## Relevant Operations
### Account configuration<span id="accountConfiguration"></span>
Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can do so in the following steps:
1. Run the following command to create a `.env` file locally:
```console
touch .env # Tencent Cloud configuration information
```
2. Configure Tencent Cloud `SecretId` and `SecretKey` information in the `.env` file as follows and save it:
```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
>?
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
