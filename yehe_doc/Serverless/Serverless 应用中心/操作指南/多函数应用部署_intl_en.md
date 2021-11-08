You can quickly build and deploy a multi-function application based on the Tencent Cloud [multi-scf](https://github.com/serverless-components/tencent-multi-scf) component, which greatly reduces the development costs of complex applications.

### Prerequisites
- Serverless Framework has been installed. For more information, please see [Installing Serverless Framework](https://intl.cloud.tencent.com/document/product/1040/37034).
- Your account has the Serverless Framework permissions. For more information, please see [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

### Development and deployment steps
For details of sample projects, please see [Case List](https://github.com/serverless-components/tencent-multi-scf/tree/master/examples).

1. Develop your application project locally. This document takes a project with two functions as an example. The application directory structure is as follows:
```
   ./multi-scf-demo
   ├── index
   │   ├── index.js # Main function 1
   │   ├── package.json
   │   └── scf_bootstrap # Bootstrap file for HTTP-triggered functions, which can be ignored for event-triggered functions
   ├── user
   │   ├── index.js # Main function 2
   │   ├── package.json
   │   └── scf_bootstrap # Bootstrap file for HTTP-triggered functions, which can be ignored for event-triggered functions
   └── serverless.yml # YML configuration file
```

2. In the **root directory**, create a `serverless.yml` file and configure relevant parameters for your project by referring to the following sample YML. For more configuration content, please see [Full Configuration](https://github.com/serverless-components/tencent-multi-scf/blob/master/docs/configure.md).
```yml
app: multi-scf # Application name
component: multi-scf # Component type, which is `multi-scf` here
name: web_demo # Customizable instance name

inputs:
  src:
    # The code directory must be specified here, and SCF will automatically split the function code according to the function configuration
    src: ./
    exclude:
      - .env
  region: ap-guangzhou # Region
  runtime: Nodejs12.16 # Function language version
  memorySize: 512
  timeout: 3
  type: web  # Function type, which is HTTP-triggered function here
  functions:
    index:
      src: ./index # Entry function of function 1
      handler: scf_bootstrap # Bootstrap file
    user:
      src: ./user # Entry function of function 2
      handler: scf_bootstrap # Bootstrap file
  triggers: # Trigger configuration
    - type: apigw
      parameters:
        name: serverless
        protocols:
          - https
          - http
        apis:
          - path: /
            method: ANY
            # The API function configuration has a higher priority than the outer function
            function: index
          - path: /user
            method: ANY
            # The API function configuration has a higher priority than the outer function
            function: user
```

3. After completing the configuration, run `sls deploy` in the root directory to test whether the project is successfully deployed.


### Application launch in console
Submit the application through a **[ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=1123&source=0&data_title=Serverless%20Framework&step=1)**. Note that your project must include the following:

| Parameter | Description |  
| ----------------------- |----------| 
| Basic configuration parameter list | Basic configuration parameter list |
| Advanced configuration parameter list | Optional |
| Application name, overview, documentation link, and tag | For block display in the console |
