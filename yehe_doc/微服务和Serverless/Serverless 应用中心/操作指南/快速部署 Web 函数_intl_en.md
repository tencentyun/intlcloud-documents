## Overview

Web function is a new function capability in SCF. Compared with event function that has limits on the event format, web function focuses on optimization of web service scenarios and can directly send HTTP requests to URLs to trigger function execution. For more information, please see [Function Overview](https://intl.cloud.tencent.com/document/product/583/40688).

The Serverless Framework SCF component now supports deploying web functions; therefore, you can use it to quickly create and deploy web functions.


## Directions

1. Run the following command to initialize the serverless web function template.
```sh
sls init http-demo
```
2. Enter the demo project and view the directory structure as shown below:
```
. http-demo
├── serverless.yml  # Configuration file
├── package.json # Dependency file
├── scf_bootstrap # Project bootstrap file
└── index.js # Service function
```
Here, `scf_bootstrap` is the project bootstrap file. For the specific writing rules, please see [Bootstrap File Description](https://intl.cloud.tencent.com/document/product/583/40690).
3. Open `serverless.yml` to view the configuration information.
You only need to add the `type` parameter in `yml` to specify the function type and deploy the web function.
<dx-alert infotype="notice" title="">
- For web functions, there is no need to specify the entry function.
- If the `type` parameter is not entered, the function will be an event function by default.
- If there is no `scf_bootstrap` bootstrap file in the local code, you can specify the `entryFile` parameter in `yml` to specify the entry function, and the component will generate a default `scf_bootstrap` file for you to complete the deployment based on the runtime language. After the deployment is completed, you need to modify the content of the `scf_bootstrap` file in the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) according to the actual needs of your project.
</dx-alert>
Below is a sample <code>yml</code> file:
<dx-codeblock>
:::  yaml
component: scf
name: http
inputs: 
  src: 
    src: ./
    exclude: 
      - .env
  # Specify web type as the function type
  type: web
  name: web-function
  region: ap-guangzhou
  runtime: Nodejs12.16
  # For Node.js, you can enable automatic dependency installation
  installDependency: true
  events: 
    - apigw: 
        parameters: 
          protocols: 
            - http
            - https
          environment: release
          endpoints: 
            - path: /
              method: ANY
:::
</dx-codeblock>
4. In the root directory, run `sls deploy` to complete the service deployment. Below is a sample:
```shell
$ sls deploy
serverless ⚡components
Action: "deploy" - Stage: "dev" - App: "http" - Name: "http"
type:         web
functionName: web-function
description:  This is a function in http application
namespace:    default
runtime:      Nodejs12.16
handler:      
memorySize:   128
lastVersion:  $LATEST
traffic:      1
triggers: 
  - 
    NeedCreate:  true
    created:     true
    serviceId:   service-xxxxxx
    serviceName: serverless
    subDomain:   service-xxxxxx.cd.apigw.tencentcs.com
    protocols:   http&https
    environment: release
    apiList: 
      - 
        path:            /
        method:          ANY
        apiName:         index
        created:         true
        authType:        NONE
        businessType:    NORMAL
        isBase64Encoded: false
        apiId:           api-xxxxxx
        internalDomain:  
        url:             https://service-xxxx.cd.apigw.tencentcs.com/release/
18s › http › executed successfully
```


## Relevant Commands

### Viewing access log

Similar to event function, you can directly run the `sls log` command to view the latest 10 logs of the deployed function. Below is a sample:
```sh
$ sls log
serverless ⚡components
Action: "log" - Stage: "dev" - App: "http" - Name: "http"
- 
  requestId:   xxxxx
  retryNum:    0
  startTime:   1624262955432
  memoryUsage: 0.00
  duration:    0
  message: 
    """
    """
- 
  requestId: xxxxx
  retryNum:    0
  startTime:   1624262955432
  memoryUsage: 0.00
  duration:    0
  message: 
    """
    """
```

### Testing service

- Scheme 1: directly open the output path URL in a browser, and if it can be accessed normally, the function is successfully created, as shown below:
![](https://main.qcloudimg.com/raw/5268439a29278030d6614d35d7b9933b.png)
- Scheme 2: use other HTTP testing tools such as CURL and Postman to test the web function you have successfully created. Below is a sample test with CURL:
```sh
curl https://service-xxx.cd.apigw.tencentcs.com/release/
```


### Deleting service

Run the following command to remove your deployed cloud resources.
```sh
sls remove
```

### Web framework migration
Serverless Framework CLI provides an HTTP component specifically for web framework deployment, which can quickly implement features such as web framework deployment, layer creation, static/dynamic resource separation, and CDN acceleration. For usage, please see [Deploying Framework on Command Line](https://intl.cloud.tencent.com/document/product/1040/41597).

