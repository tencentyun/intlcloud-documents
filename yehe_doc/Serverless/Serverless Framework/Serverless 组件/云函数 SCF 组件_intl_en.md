## Component Overview

**Tencent Cloud SCF** uses [Tencent Serverless Framework](https://github.com/serverless/components/tree/cloud). Based on serverless services (functions, triggers, etc.) in the cloud, it can implement "zero" configuration, convenient development, and rapid deployment of your first function. It supports a rich set of configuration extensions and provides the easiest-to-use, low-cost, and elastically scalable cloud-based function development, configuration, and deployment capabilities.


## Getting Started

### Prerequisites

- You have installed Serverless Framework as instructed in [Installing Serverless Framework](https://intl.cloud.tencent.com/document/product/1040/37034).
- Your account has the Serverless Framework permissions as detailed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).


### Directions

#### Creation
- Method 1. Select an SCF project template for creation as instructed in [Serverless Framework](https://intl.cloud.tencent.com/document/product/1040/36249).
- Method 2. Directly run the `sls init` command for creation. You can quickly create an SCF function in Node.js as follows:
```
sls init scf-nodejs
```
>?The `helloworld` templates currently supported by the SCF component are `scf-golang`, `scf-php`, and `scf-python`. You only need to replace `scf-nodejs` in the command with the template name listed above to quickly initialize a template in the corresponding language.

#### Deployment
Run the following command, and a QR code will pop up. Directly scan the code to authorize for deployment:
```
sls deploy
```
>?If authentication fails, please authorize as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).


#### Viewing
Run the following command to view the information of the deployed project:
```
sls info
```

#### Removal
Run the following command to remove the deployed project:
```
sls remove
```



## Advanced Guide
### serverless.yml
When `sls deploy` is executed, function resources will be created or updated according to the configuration in the `serverless.yml` file. The following is a simple `serverless.yml` file:
>?For more information on the configuration, please see the [configuration documentation](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md).

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

Information in the `serverless.yml` file:

#### Component information

| Component | Required | Description |
|---------|---------|---------|
| component | Yes | Component name. You can run `sls registry` to query components available for import. |
| name | Yes | Name of the created instance. An instance will be created when each component is deployed. |


#### Parameter information
Parameters in `inputs` are component configuration parameters. The parameters of a simplest SCF component are as detailed below:

| Parameter | Description |
|---------|---------|
| name | Function name. As it is also the resource ID, to ensure the uniqueness of the resource, we recommend you use the `${name}-${stage}-${app}` variable as the name. |
| src | Code path. |
| handler | Function handler name. |
| runtime | Function runtime environment. Valid values: Python2.7, Python3.6, Nodejs6.10, Nodejs8.9, Nodejs10.15, Nodejs12.16, PHP5, PHP7, Go1, Java8, CustomRuntime. |
| region | Function region. |
| events | Trigger. Valid values: timer, apigw, cos, cmq, ckafka. |




### Account permission
When deploying an instance, you need to grant the corresponding account permissions to manipulate specific Tencent Cloud resources. Currently, you can authorize **by scanning the code** or **with a key**.

- **Authorization by scanning code**: this method allows you to quickly authorize for deployment, but the generated credential is only temporary, and you need to scan the code again after the credential expires.
- **Authorization with key**: this method grants persistent permissions, but you need to configure the `SecretId` and `SecretKey` of the account in advance.

For more information on the configuration, please see [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).



### Development and debugging

You can run `sls dev` in the directory of the `serverless.yml` file to output cloud logs in real time. After each deployment, you can access the project to output invocation logs in real time on the command line, which makes it easy for you to view business conditions and troubleshoot issues. Node.js allows you to enable the development debugging feature, which can detect and automatically upload changes in the local code. For more information, please see [Development Mode and In-cloud Debugging](https://intl.cloud.tencent.com/document/product/1040/36860).



### Application management
Deployment of a component instance in Serverless Framework is actually deployment of a single-component instance application.

During the development of an application project, there may be multiple component instances under the same application. For detailed directions on how to manage component instances for application project development, please see [Application Management](https://intl.cloud.tencent.com/document/product/1040/38288).



### Component commands

The SCF component provides component-level commands. A function successfully deployed by running the `sls deploy` command can be manipulated with the following commands.

>?The command must be executed in the same directory as `serverless.yml`.

#### Publishing function version
Publish the `$LATEST` version of the `my-function` function as a fixed version:
```
sls publish-ver --inputs  function=my-function
```

#### Creating alias
Create the `routing-alias` alias for the `my-function` function, with the routing rule of 50% traffic for version 1 and 50% traffic for version 2:
```
sls create-alias --inputs name=routing-alias  function=my-function  version=1  
config='{"weights":{"2":0.5}}'
```

#### Updating alias
Update the flow rule of the `routing-alias` alias of the `my-function` function to 10% for version 1 and 90% for version 2:
```
sls update-alias --inputs name=routing-alias  function=my-function  version=1 config='{"weights":{"2":0.9}}'
```

#### Listing alias
List the `routing-alias` alias of the `my-function` function:
```
sls list-alias --inputs function=my-function
```

#### Deleting alias
Delete the `routing-alias` alias of the `my-function` function:
```
sls delete-alias --inputs name=routing-alias  function=my-function
```

#### Triggering function
Invoke the `functionName` function and pass the JSON parameter `{"weights":{"2":0.1}}`:
```
sls invoke  --inputs function=functionName  clientContext='{"weights":{"2":0.1}}'
```

