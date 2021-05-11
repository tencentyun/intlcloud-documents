## Overview
Serverless Framework provides multiple basic resource components, which you can mix and use to quickly create and deploy resources in the cloud. This document describes how to use existing components to build your own multi-component serverless application template.

## Prerequisites
You have [installed Serverless Framework](https://intl.cloud.tencent.com/document/product/1040/37034) on at least the following versions:

```shell
$ serverless –v
Framework Core: 2.16.1
Plugin: 4.3.0
SDK: 2.3.2
Components: 3.4.3
```

<span id ="doc"></span>

## Component Configuration Documentation

- [Basic Component List](https://intl.cloud.tencent.com/document/product/1040/39135)
- [Framework Component List](https://intl.cloud.tencent.com/document/product/1040/39375)


## Directions
This document uses deploying a **framework project based on Layer and Egg** as an example to describe how to import multiple components into your project and quickly complete the deployment. The steps are as follows:

### Step 1. Create a project
Create a project `app-demo` and enter this directory:

   ```bash
   $ mkdir app-demo && cd app-demo
   ```

### Step 2. Build an Egg project

1. In the `app-demo` directory, create a `src` folder and create an Egg project in it:
```bash
$ mkdir src && cd src
$ npm init egg --type=simple
$ npm i
```

2. In the `src` directory, write the configuration file `serverless.yml`:
```bash
$ touch serverless.yml
```
 A sample `.yml` file for the Egg component is provided below. For more information on all configuration items, please see [Egg.js Component Configuration](https://github.com/serverless-components/tencent-egg/blob/master/docs/configure.md).

``` yml
# serverless.yml
app: app-demo # Application name. The `app`, `stage`, and `org` parameters must be the same for each component under the same application
stage: dev
component: egg 
name:  app-demo-egg # Name of the created instance, which is required

inputs:
  src:   
    src: ./    # Project path for upload
    exclude:   # Exclude the `node_modules` and `.env` file
      - .env
      - node_modules
  region: ap-guangzhou
  functionName: eggDemo  # Function configuration
  runtime: Nodejs10.15
  apigatewayConf:
    protocols:           # API Gateway trigger configuration. A gateway will be created by default
      - http
      - https
    environment: release
```

>!
>- The **`app`, `stage`, and `org`** parameters must be the same for the resources created by each component under the same project.
>- The Egg component essentially creates an API Gateway trigger + SCF resource. Here, you can select different components according to your actual development needs, and the configuration methods are similar. For more information, please see [Component Configuration Documentation](#doc).


### Step 3. Create a layer
Go back to the root directory of `app-demo`, create a `layer` folder, and create a layer configuration file `serverless.yml` in it:
```
$ cd ..
$ mkdir layer && cd layer
$ touch serverless.yml
```
`serverless.yml` can be configured according to the following template (for more information on the configuration, please see [Layer Component Configuration](https://github.com/serverless-components/tencent-layer/blob/master/docs/configure.md)):
```  yml
# serverless.yml
app: app-demo # Application name. The `app`, `stage`, and `org` parameters must be the same for each component under the same application
stage: dev
component: layer 
name:  app-demo-layer # Name of the created instance, which is required

inputs:
  region: ap-guangzhou
  src: 
    src: ../src/node_modules # Path of the project you want to upload to the layer. `node_modules` is used as an example here
    targetDir: /node_modules # File compression directory after upload
  runtimes:
    - Nodejs10.15
```

>!
>- The **`app`, `stage`, and `org`** parameters must be the same for the resources created by each component under the same project.
>- The Layer component also supports importing projects from COS buckets. For more information, please see [Layer Component Configuration](https://github.com/serverless-components/tencent-layer/blob/master/docs/configure.md). When entering the `bucket` parameter, be sure not to include `-${appid}`, as the component will add it automatically.

### Step 4. Organize the resource relationship

In the same application, you can organize the creation order of resources according to their dependency relationship. Taking this project as an example, you need to create a layer first and then use the layer in the Egg.js project; therefore, you should ensure that the resource creation order is * *layer > Egg.js application**. The specific steps are as follows:

Modify the `.yml` configuration file of the Egg.js project, configure the layer configuration according to the following syntax, and import the deployment output of the Layer component as the deployment input of the Egg.js project to ensure that the Layer component is created before the Egg.js project:

```
$ cd ../src
```
In `serverless.yml`, add layer configuration in the `inputs` section:

``` yml
inputs:
  src:   
    src: ./    
    exclude:  
      - .env
      - node_modules
  region: ap-guangzhou
  functionName: eggDemo  
  runtime: Nodejs10.15
  layers:   # Add the layer configuration
    - name: ${output:${stage}:${app}:app-demo-layer.name} # Layer name
      version: ${output:${stage}:${app}:app-demo-layer.version} # Version
  apigatewayConf:
    protocols:        
      - http
      - https
    environment: release
```

For the variable import format, please see [Variable Import Description](#quote).

At this point, the serverless application has been built, and the project directory structure is as follows:

```
   ./app-demo
   ├── layer
   │   └── serverless.yml # Layer configuration file
   ├── src
   │   ├── serverless.yml # Egg component configuration file
   │   ├── node_modules # Project dependency file
   │   ├── ...
   │   └── app # Project routing file
   └── .env # Environment variable file
```

### Step 5. Deploy the application
In the project root directory, run `sls deploy` to complete layer creation and use the output of the Layer component as the input of the Egg.js component to cloudify the Egg.js framework.
```  bash
 $ sls deploy

serverless ⚡framework

app-demo-layer: 
  region:        ap-guangzhou
  name:          layer_component_xxx
  bucket:        sls-layer-ap-guangzhou-code
  object:        layer_component_xxx.zip
  description:   Layer created by serverless component
  runtimes: 
    - Nodejs10.15
  version:       3
  vendorMessage: null

app-demo-egg: 
  region:        ap-guangzhou
  scf: 
    functionName: eggDemo
    runtime:      Nodejs10.15
    namespace:    default
    lastVersion:  $LATEST
    traffic:      1
  apigw: 
    serviceId:   service-xxxx
    subDomain:   service-xxx.gz.apigw.tencentcs.com
    environment: release
    url:         https://service-xxx.gz.apigw.tencentcs.com/release/
  vendorMessage: null

76s › app-demo › "deploy" ran for 2 apps successfully.
```


You can click the URL output by `apigw` to access the created application, run `sls info` to view the status of the deployed instance, or run `sls remove` to quickly remove the application.

### Step 6. Publish the application template
After the serverless project template is built, Serverless Framework allows you to publish it in the Serverless Registry for use by your team and others.

#### 1. Create a configuration file
In the root directory, create a `serverless.template.yml` file, and the project directory structure is as follows:

   ```
   ./app-demo
   ├── layer
   │   └── serverless.yml # Layer configuration file
   ├── src
   │   ├── serverless.yml # Egg component configuration file
   │   ├── node_modules # Project dependency file
   │   ├── ...
   │   └── app # Project routing file
   ├── .env # Environment variable file
   └── serverless.template.yml # Template project description file
   ```

#### 2. Configure and publish the project template file
```  yml
 # serverless.template.yml
name: app-demo # Project template name, which must be unique
displayName: Egg.js project template created based on layer # Name of the project template displayed in the console
author: Tencent Cloud, Inc. # Author name
org: Tencent Cloud, Inc. # Organization name, which is optional
type: template # Project type, which can be either `template` or `component`. It is `template` here
description: Deploy an egg application with layer. # Describe your project template
description-i18n:
  zh-cn: Egg.js project template created based on layer # Description
keywords: tencent, serverless, eggjs, layer # Keywords
repo:  # Source code repo, which is usually your GitHub repo
readme:  # Detailed description file, which is usually your GitHub repo README file
license: MIT # Copyright notice
src: # Describe the files in the project to be published as a template
  src: ./ # Specify a relative directory, the files under which will be published as a template
  exclude: # Describe the files in the specified directory to be excluded
    # The following files are usually excluded
    # 1. Files containing `secrets`
    # 2. Files managed by `.git` git source code
    # 3. Third-party dependencies such as `node_modules`
    - .env
    - '**/node_modules'
    - '**/package-lock.json'
```

After the `serverless.template.yml` file is configured, you can use the `sls publish` command to publish the project to the Registry as a template.
   ```
$ sls publish

serverless ⚡registry
Publishing "app-demo@0.0.0"...

Serverless › Successfully published app-demo
   ```

#### 3. Reuse the template

After your template is published, others can quickly download it and reuse the project by running the `sls init` command.
```
$ sls init app-demo --name example
$ cd example
$ npm install
```

<span id="quote"></span>

## Variable Import Description

`serverless.yml` supports multiple ways to import variables:

- **Import basic Serverless parameters**
   In the `inputs` field, you can directly import basic Serverless parameter configuration information through the `${org}` and `${app}` syntax.

- **Import environment variables**  
   In `serverless.yml`, you can directly import the environment variable configuration (including the environment variable configuration in the `.env` file and variable parameters manually configured in the environment) through the `${env}` syntax.
   
   For example, you can import the environment variable `REGION` through `${env:REGION}`.

- **Import the output results of other components**
   If you want to import the output information of other component instances into the current component configuration file, you can configure it by using the following syntax:
	 `${output:[app]:[stage]:[instance name].[output]}`

Sample `.yml` file:
```  yml
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



