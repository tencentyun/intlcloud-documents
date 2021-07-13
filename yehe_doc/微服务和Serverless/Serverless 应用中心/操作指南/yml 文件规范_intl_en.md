Serverless Framework uses the project configuration file `serverless.yml` to identify the application type and configure the resources. After you develop a project locally, you must configure the `.yml` file first before you can deploy the project in the cloud by running the `sls deploy` command to pass the configuration information in `serverless.yml` and the specified parameters or code directory in `inputs` to the Serverless Components deployment engine.

## Basic Information

The first-level field in a basic `serverless.yml` file is configured as follows:

```yml
# Organization information (optional)
app: '' # Application name. If it is left empty, the instance name of the current component will be used by default
stage: '' # Environment name. The default value is `dev`. We recommend you use the `${env.STAGE}` variable to define the environment name

# Component information
component: scf # Component name, which is required. It is `scf` in this example
name: scfdemo # Component instance name, which is required

# Component parameter configuration, which configures specific resource information for each component
inputs:

```

## Detailed Configuration

In the `inputs` field, the corresponding information will be configured for the resources created by each component in the cloud. The [SCF Component](https://github.com/serverless-components/tencent-scf) is taken as an example here. The second-level directory in the `input` field is as follows:

```yml
inputs:
  name: xxx # Function name, which is `${name}-${stage}-${app}` by default
  src: ./src # Project code path in the default format. Create a specifically named COS bucket and upload it
  handler: index.main_handler # Entry
  runtime: Nodejs10.15 # Runtime environment, which is Nodejs10.15 by default
  region: ap-guangzhou # Function region
  description: This is a function in ${app} application.
  environment: # Environment variable
    variables: # Environment variable object
      TEST: value
  layers: # Layer configuration
    - name: scfLayer # Layer name
      version: 1 # Version
  events: # Trigger configuration
    - timer: # Scheduled trigger
        parameters:
          cronExpression: '*/5 * * * * * *' # Trigger once every 5 seconds
          enable: true
```

## Full Configuration List
Below is the list of full configuration information for each component of Serverless Framework:

### Basic components
<style>
table th:nth-of-type(1) {
width: 150px;        
}
</style>
| Component                   |    Full Configuration                           |  
| ----------------------- | ------------------------------------- | 
| SCF     | [SCF - serverless.yml configuration](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md)         |
| Website  |[Website - serverless.yml configuration](https://github.com/serverless-components/tencent-website/blob/master/docs/configure.md)|      
| API Gateway     | [API Gateway - serverless.yml configuration](https://github.com/serverless-components/tencent-apigateway/blob/master/docs/configure.md)                |      
| VPC     | [VPC - serverless.yml configuration](https://github.com/serverless-components/tencent-vpc/blob/master/docs/configure.md)          |      
| COS     | [COS - serverless.yml configuration](https://github.com/serverless-components/tencent-cos/blob/master/docs/configure.md)              |      
| PostgreSQL   | [PostgreSQL - serverless.yml configuration](https://github.com/serverless-components/tencent-postgresql/blob/master/docs/configure.md)         |      
| CynosDB     | [CynosDB - serverless.yml configuration](https://github.com/serverless-components/tencent-cynosdb/blob/master/docs/configure.md)             |      
| CDN | [CDN - serverless.yml configuration](https://github.com/serverless-components/tencent-cdn/blob/master/example/serverless.yml)           |
| Layer    |[Layer - serverless.yml configuration](https://github.com/serverless-components/tencent-layer/blob/master/docs/configure.md)|

### Framework components
<style>
table th:nth-of-type(1) {
width: 150px;        
}
</style>

| Component                   |    Full Configuration                           |  
| ----------------------- | ------------------------------------- | 
| Express     | [Express - serverless.yml configuration](https://github.com/serverless-components/tencent-express/blob/master/docs/configure.md) |
|  Koa       | [Koa - serverless.yml configuration](https://github.com/serverless-components/tencent-koa/blob/master/docs/configure.md)         |      
| Egg  | [Egg - serverless.yml configuration](https://github.com/serverless-components/tencent-egg/blob/master/docs/configure.md)   |      
| Next.js  | [Next.js - serverless.yml configuration](https://github.com/serverless-components/tencent-nextjs/blob/master/docs/configure.md)   |
| Nuxt.js | [Nuxt.js - serverless.yml configuration](https://github.com/serverless-components/tencent-nuxtjs/blob/master/docs/configure.md) |
| Flask | [Flask - serverless.yml configuration](https://github.com/serverless-components/tencent-flask/blob/master/docs/configure.md) |
| Django | [Django - serverless.yml configuration](https://github.com/serverless-components/tencent-django/blob/master/docs/configure.md)|
|Laravel|[Laravel - serverless.yml configuration](https://github.com/serverless-components/tencent-laravel/blob/master/docs/configure.md)|
|ThinkPHP|[ThinkPHP - serverless.yml configuration](https://github.com/serverless-components/tencent-thinkphp/blob/master/docs/configure.md)|
