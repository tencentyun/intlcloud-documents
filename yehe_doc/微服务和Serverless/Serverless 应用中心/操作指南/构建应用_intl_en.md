## Overview
After Serverless Framework is installed, you can initialize a project template and build a multiple-component application as instructed in this document.

## Prerequisites
You have [installed Serverless Framework](https://intl.cloud.tencent.com/document/product/1040/37034).

## Directions
### Initializing project template

You can quickly initialize a demo project by running the following command and modify it for further development:
```
sls init scf-demo
```
This command can quickly build a basic function application locally with the following directory structure:

```
.
├── serverless.yml  # Configuration file
└── src
   └── index.js # Entry function
```

You can enter this directory and develop your project based on the demo template.

>?`sls init` can quickly initialize multiple project templates. You can run the `sls registry` command to view all supported project templates.

### Building multiple-component application
Serverless Framework provides multiple basic resource components, which you can mix and use to quickly create and deploy resources in the cloud, thus eliminating the need for manual operations in the console (for more information, please see [Basic Component List and Configuration Method](https://intl.cloud.tencent.com/document/product/1040/39135)).

This document uses deploying a function project triggered by a COS trigger as an example to describe how to import multiple components into your project and quickly complete the deployment. The steps are as follows:

1. Adjust the structure of the project directory, create a COS folder, and write the configuration file `serverless.yml` for the COS component in this directory. The adjusted structure of the directory is as follows:
```
.
├── src
│   ├── serverless.yml # Function configuration file
│   └── index.js # Entry function
├── cos
│   └── serverless.yml # COS bucket configuration file
└── .env # Environment variable file
```

A sample `.yml` file for the COS component is provided below. For more information on all configuration items, please see [COS Component Configuration](https://github.com/serverless-components/tencent-cos/blob/master/docs/configure.md).

```yml
app: appDemo
stage: dev

component: cos
name: cosdemo

inputs:
  bucket: my-bucket
  region: ap-guangzhou
```

2. Modify the `.yml` configuration file for the SCF project and impot the deployment result of the COS component according to the following syntax in the trigger configuration part:

```yml
app: appDemo
stage: dev

component: scf
name: scfdemo
inputs:
  ...
  events:
   - cos: # COS trigger
        parameters:
          bucket: ${output:${stage}:${app}:cosdemo.bucket}
```
>!When deploying multiple component instances in the same project, you need to make sure that the `app` and `stage` parameters of each project are the same; otherwise, they cannot be successfully imported.

3. In the project root directory, run `sls deploy` to complete COS bucket creation and use the output of the COS component as the input of the SCF component to configure the trigger.

### Variable import description
`serverless.yml` supports multiple ways to import variables:

- **Import basic Serverless parameters**
   In the `inputs` field, you can directly import basic Serverless configuration information through the `${org}` and `${app}` syntax.

- **Import environment variables**
   In `serverless.yml`, you can directly import the environment variable configuration (including the environment variable configuration in the `.env` file and variable parameters manually configured in the environment) through the `${env}` syntax.
   For example, you can import the environment variable `REGION` through `${env:REGION}`.

- **Import the output results of other components**
   If you want to import the output information of other component instances into the current component configuration file, you can configure it by using the following syntax: `${output:[app]:[stage]:[instance name].[output]}`

Sample `.yml` file:
```yml
app: demo
component: scf
name: rest-api
stage: dev

inputs:
  name: ${stage}-${app}-${name} # The final name is "acme-prod-ecommerce-rest-api"
  region: ${env:REGION} # `REGION=` information specified in the environment variable
  vpcName: ${output:prod:my-app:vpc.name} # Get the output information of other components
  vpcName: ${output:${stage}:${app}:vpc.name} # The above methods can also be used in combination
```

