## Overview
Due to the limits of SCF, only code packages below 50 MB in size can be uploaded currently. If your project is too large, you can put dependencies in layers instead of the deployment package to reduce the package size. For specific usages of layers, please see [Operations](https://intl.cloud.tencent.com/document/product/583/34878).

## Directions
### Creating layer
You can create a layer and upload dependencies in the following two ways:
- Create in the [SSR console](https://console.cloud.tencent.com/ssr)
- Use the Layer component of Serverless Framework (for more information, please see [Layer Component](https://intl.cloud.tencent.com/document/product/1040/37262)) 

### Using layer
You can use layer deployment in project configuration in the following two ways: console configuration and local configuration.

#### Configuring in console
- For applications in the Node.js framework, Serverless Framework will automatically create a layer named `${appName}-layer` and upload the application dependency `node_modules` to this layer.
- When importing an existing project, you can also choose to create a layer or use an existing layer for deployment. If you create a layer, Serverless Framework will automatically upload the application dependency `node_modules` to this layer.

>?The layer creation operation is supported only for the Node.js framework. When using a layer in other frameworks, please make sure that the layer has already been created and the relevant dependencies have been uploaded to the layer.

#### Configuring through Layer component
1. The Next.js component is used as an example here. Adjust the local project directory, add a `layer` folder, and create a **serverless.yml** file to configure the layer name and version. The `.yml` template is as follows:
   ```yml
   app: appDemo
   stage: dev

   component: layer
   name: layerDemo

   inputs:
    name: test
    region: ap-guangzhou
    src: ../node_modules # Path of the file to be uploaded
    runtimes:
      - Nodejs10.14
   ```
   For detailed configuration items, please see [Layer Component Configuration](https://github.com/serverless-components/tencent-layer/blob/master/docs/configure.md).

   The updated directory structure is as follows:
   ```
   .
   ├── node_modules
   ├── src
   │   ├── serverless.yml # Function configuration file
   │   └── index.js # Entry function
   ├── layer
   │   └── serverless.yml # Layer configuration file
   └── .env # Environment variable file
   ```
2. Open the project configuration file, add the layer configuration item, and import the output of the Layer component as the input of the project configuration file. The template is as follows:
  ```yml
   app: appDemo
   stage: dev

   component: nextjs
   name: nextjsDemo

   inputs:
     src:
       src: ./
       exclude:
         - .env
         
     region: ap-guangzhou
     runtime: Nodejs10.15
     apigatewayConf:
        protocols:
          - http
          - https
        environment: release
     layers:
        - name: ${output:${stage}:${app}:layerDemo.name} # Layer name
        version: ${output:${stage}:${app}:layerDemo.version} # Version
  ```
   For the import format, please see [Variable Import Description](https://github.com/AprilJC/Serverless-Framework-Docs/blob/main/docs/%E5%87%BD%E6%95%B0%E5%BA%94%E7%94%A8%E5%BC%80%E5%8F%91/%E6%9E%84%E5%BB%BA%E5%BA%94%E7%94%A8.md#%E5%8F%98%E9%87%8F%E5%BC%95%E7%94%A8%E8%AF%B4%E6%98%8E).
3. In the project root directory, run `sls deploy` to complete layer creation and use the output of the Layer component as the input of the Next.js component to configure the layer.

