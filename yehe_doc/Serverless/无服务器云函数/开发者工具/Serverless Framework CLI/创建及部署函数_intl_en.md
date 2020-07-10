## Operation Scenarios
This document describes how to use the SCF component provided by Serverless Framework to quickly create and deploy an SCF project.


## Prerequisites
You have installed Serverless Framework as instructed in [Installing Serverless Framework](https://intl.cloud.tencent.com/document/product/583/36263).


## Directions
### Creating function directory
1. Run the following command on the command line to create a directory and enter it (this document uses `tencent-scf` as an example):
```
mkdir tencent-scf && cd tencent-scf
```
2. Run the following commands in sequence to quickly create an SCF application:
```
serverless create --template-url https://github.com/serverless-components/tencent-scf/tree/v2/example
```
```
cd example
```
After the application is created successfully, its directory structure is as follows
```
|- src
|   └── index.py
└──  serverless.yml
```

### Deploying function
1. Enter the directory where `serverless.yml` is and run the following command to deploy the function:
```
serverless deploy
```
2. Log in to your Tencent Cloud account and grant applicable permissions. If you want to configure persistent environment variables or key information, please do so as instructed in [Account Configuration](https://intl.cloud.tencent.com/document/product/583/32743).
After the function is deployed successfully, you can view the URL provided by the gateway trigger of the corresponding function in the command line output and access the URL in a browser to view the function deployment result. 
>If you want to view more information on the deployment process, you can run the `sls deploy --debug` command to view the real-time log information during the deployment process (`sls` is an abbreviation for the `serverless` command).
>


### Configuring deployment
The SCF component supports "zero" configuration deployment, that is, it can be deployed directly with the default values in the configuration file. Nonetheless, you can also modify more optional configuration items as needed to further customize the project to be deployed.
The following is the description of the SCF component configuration file `serverless.yml`. For more information, please see [Full Configuration and Configuration Description](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md).
```
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

## Subsequent Operations
After deploying the function, you can use the development and debugging capabilities provided by the component to re-develop the project into a production-ready application.
