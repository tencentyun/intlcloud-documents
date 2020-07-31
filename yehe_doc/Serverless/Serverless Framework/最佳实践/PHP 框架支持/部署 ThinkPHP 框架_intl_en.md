## Operation Scenarios

Tencent Cloud [ThinkPHP](https://github.com/top-think/think) Serverless Component supports deploying RESTful API services.

## Prerequisites

#### Initializing ThinkPHP project

Before using this component, you need to initialize a `ThinkPHP` project first:

```bash
$ composer create-project topthink/think serverless-thinkphp
```

>?ThinkPHP uses Composer to manage dependencies, so you need to install Composer first. For more information, please see [here](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos).

## Directions
### Installation
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:

```bash
$ npm install -g serverless
```

### Configuration
Create a `serverless.yml` file in the project root directory:

```bash
$ touch serverless.yml
```
Configure `serverless.yml` as follows:
```yml
# serverless.yml

MyThinkPHP:
  component: '@serverless/tencent-thinkphp'
  inputs:
    region: ap-guangzhou
    functionName: thinkphp-function
    code: ./
    functionConf:
      timeout: 10
      memorySize: 128
      environment:
        variables:
          TEST: abc
      vpcConfig:
        subnetId: ''
        vpcId: ''
    apigatewayConf:
      protocols:
        - https
      environment: release
```
[Detailed Configuration >>](https://github.com/serverless-components/tencent-thinkphp/tree/master/docs/configure.md)

### Deployment
>!Before deployment, you need to clear the local configuration cache by running `php think clear`.



Deploy by running the `sls` command, and you can add the `--debug` parameter to view the information during the deployment process:
>?`sls` is short for the `serverless` command.

```bash
$ sls --debug

  DEBUG ─ Resolving the template's static variables.
  DEBUG ─ Collecting components from the template.
  DEBUG ─ Downloading any NPM components found in the template.
  DEBUG ─ Analyzing the template's components dependencies.
  DEBUG ─ Creating the template's components graph.
  DEBUG ─ Syncing template state.
  DEBUG ─ Executing the template's components graph.
  DEBUG ─ Compressing function thinkphp-function file to /Users/yugasun/Desktop/Develop/serverless/tencent-thinkphp/example/.serverless/thinkphp-function.zip.
  DEBUG ─ Compressed function thinkphp-function file successful
  DEBUG ─ Uploading service package to cos[sls-cloudfunction-ap-guangzhou-code]. sls-cloudfunction-default-thinkphp-function-1584413066.zip
  DEBUG ─ Uploaded package successful /Users/yugasun/Desktop/Develop/serverless/tencent-thinkphp/example/.serverless/thinkphp-function.zip
  DEBUG ─ Creating function thinkphp-function
  DEBUG ─ Created function thinkphp-function successful
  DEBUG ─ Setting tags for function thinkphp-function
  DEBUG ─ Creating trigger for function thinkphp-function
  DEBUG ─ Deployed function thinkphp-function successful
  DEBUG ─ Starting API-Gateway deployment with name ap-guangzhou-apigateway in the ap-guangzhou region
  DEBUG ─ Service with ID service-qndauhr4 created.
  DEBUG ─ API with id api-6krpwfpo created.
  DEBUG ─ Deploying service with id service-qndauhr4.
  DEBUG ─ Deployment successful for the api named ap-guangzhou-apigateway in the ap-guangzhou region.

  MyThinkPHP:
    functionName:        thinkphp-function
    functionOutputs:
      ap-guangzhou:
        Name:        thinkphp-function
        Runtime:     Php7
        Handler:     serverless-handler.handler
        MemorySize:  128
        Timeout:     10
        Region:      ap-guangzhou
        Namespace:   default
        Description: This is a template function
    region:              ap-guangzhou
    apiGatewayServiceId: service-qndauhr4
    url:                 https://service-qndauhr4-1251556596.gz.apigw.tencentcs.com/release/
    cns:                 (empty array)

  18s › MyThinkPHP › done
```



### Removal
You can run the following commands to remove the deployed API Gateway:

```bash
$ sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Removed function thinkphp-function successful
  DEBUG ─ Removing any previously deployed API. api-6krpwfpo
  DEBUG ─ Removing any previously deployed service. service-qndauhr4

  8s › MyThinkPHP › done
```

### Account configuration (optional)
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
- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

### More components

You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).
