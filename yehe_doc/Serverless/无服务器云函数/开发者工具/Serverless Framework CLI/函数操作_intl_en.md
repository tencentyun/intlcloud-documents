## Overview
This document describes how to quickly create and deploy an SCF project.

## Prerequisites
- Serverless Framework has been installed. For more information, please see [Installing Serverless Framework](https://intl.cloud.tencent.com/document/product/583/36263).
- Your account has the Serverless Framework permissions. For more information, please see [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/583/36270).

## Directions

### Creating function
Run the following command to quickly create a function in the Node.js language:
```
sls init scf-demo
```
>?`scf-demo` in the command is the Node.js template by default, and you can replace it with function templates in other languages, such as `scf-golang`, `scf-php`, and `scf-python`.
>
After the function is successfully created, there will be a `serverless.yml` configuration file in the `scf-demo` project directory, which defines the SCF resource information for each deployment. For more information on the configuration file, please see [Configuration file](#configuration).

### Deploying function
Run the following command in the `scf-demo` directory to deploy the function:
```
sls deploy
```
A QR code will pop up. Please scan it to authorize and start deployment. After successful deployment, SCF resources will be automatically created.
>?If authentication fails, please authorize as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).
>

### View function information
Run the following command to view the information of the deployed SCF resources:
```
sls info
```

### Removing function
Run the following command to remove the deployed SCF resources:
```
sls remove
```

[](id:configuration)

### Configuration file

Serverless Framework CLI relies on the configuration in the `serverless.yml` file when creating or updating a function. When the `sls deploy` command is executed to deploy a function, SCF resources will be created or updated according to the configuration in the `serverless.yml` file. Below is a simple example of this file. For more information on the configuration, please see [Full Configuration](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md).
```
# SCF component configuration sample
# For all configuration items, please visit https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md.

# Component information
component: scf # Name of the imported component, which is required. The `tencent-scf` component is used in this example
name: scfdemo # Name of the created instance, which is required. Replace it with the name of your instance

# Component parameters
inputs:
  name: ${name}-${stage}-${app} # Function name
  src: ./  # Code path
  handler: index.main_handler # Entry
  runtime: Nodejs10.15 # Function runtime environment
  region: ap-guangzhou # Function region
  events: # Trigger
    - apigw: # Gateway trigger
        parameters:
          endpoints:
            - path: /
              method: GET
```

The `serverless.yml` file contains the following information:

#### Component information

| Component | Required | Description |
| --------- | -------- | ---------------------------------------------------------- |
| component | Yes | Component name. You can run the `sls registry` command to query components available for import. |
| name | Yes | Name of the created instance. An instance will be created when each component is deployed. |


#### Parameter information

Parameters in `inputs` are component configuration parameters. The parameters of a simplest SCF component are as detailed below:

| Parameter | Description |
| ------- | ------------------------------------------------------------ |
| name | Function name, which also serves as a resource ID. |
| src | Code path. |
| handler | Function handler name. |
| runtime | Function runtime environment. Valid values: Python2.7, Python3.6, Nodejs6.10, Nodejs8.9, Nodejs10.15, Nodejs12.16, PHP5, PHP7, Go1, Java8, CustomRuntime. |
| region | Function region. |
| events | Trigger. Valid values: timer, apigw, cos, cmq, ckafka. |



## Common Operation Commands
Serverless Framework provides a set of operation commands for deployment orchestration, which can be used to quickly deploy function resources. For more information, please see [List of Supported Commands](https://intl.cloud.tencent.com/document/product/583/36269).

For a function successfully deployed by running the `sls deploy` command, the following common operation commands provided by the SCF component can also be used.
>!Such commands must be executed in the same directory as `serverless.yml`.
>
- **Publish function version**
Run the following command to publish the `$LATEST` version of the `my-function` function as a fixed version:
```plaintext
sls publish-ver --inputs  function=my-function
```
- **Create alias**
Run the following command to create the `routing-alias` alias for the `my-function` function, with the routing rule of 50% traffic for version 1 and 50% traffic for version 2:
```plaintext
sls create-alias --inputs name=routing-alias  function=my-function  version=1  
config='{"weights":{"2":0.5}}'
```
- **Update alias**
Run the following command to update the flow rule of the `routing-alias` alias of the `my-function` function to 10% for version 1 and 90% for version 2:
```plaintext
sls update-alias --inputs name=routing-alias  function=my-function  version=1 config='{"weights":{"2":0.9}}'
```
- **List alias**
Run the following command to list the `routing-alias` alias of the `my-function` function:
```plaintext
sls list-alias --inputs function=my-function
```
- **Delete alias**
Run the following command to delete the `routing-alias` alias of the `my-function` function:
```plaintext
sls delete-alias --inputs name=routing-alias  function=my-function
```
- **Trigger function**
Run the following command to invoke the `functionName` function and pass the JSON parameter {"weights":{"2":0.1}}:
```plaintext
sls invoke  --inputs function=functionName  clientContext='{"weights":{"2":0.1}}'
```
