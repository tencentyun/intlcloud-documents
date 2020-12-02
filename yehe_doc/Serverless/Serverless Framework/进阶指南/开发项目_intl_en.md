## Prerequisites
- You have understood how to [quickly deploy a project](https://intl.cloud.tencent.com/document/product/1040/36249).
- You have understood [serverless applications](https://intl.cloud.tencent.com/document/product/1040/38288).
- You have understood [account and permission configuration](https://intl.cloud.tencent.com/document/product/1040/36793).



## Development Process
The development and launch process of a project is as shown below:
![](https://main.qcloudimg.com/raw/d24f99ec6b8e22fa16e230405579c171.svg)
1. Project initialization: initialize the project; for example, select some development frameworks and templates to complete the basic construction.
2. Development: develop product features. This stage may involve collaboration among multiple developers, who will pull different feature branches for separated development and testing and finally merge them into the `dev` branch for joint testing.
3. Testing: test the product features by testing personnel.
4. Release and launch: publish and launch the tested product features. As a newly published version may be unstable, grayscale release will be used generally, and some rules will be configured to monitor the stability of the new version. After the new version becomes stable, all traffic will be switched to it.



## Environment Isolation
During each stage of project development, an environment running independently is required to isolate the development operations.

Define `stage` in the `serverless.yml` file and write `stage` into the component's resource names as a parameter, so that resources named `instance name-{stage}-application name` will be generated during the deployment. In this way, you can generate different resources in different stages by defining different `stage` values so as to isolate the environments.

Take `serverless.yml` of the SCF component as an example:
```
# Application information
app: myApp
stage: dev # The environment is defined as `dev`

# Component information
component: scf 
name: scfdemo 

# Component parameters
inputs:
  name: ${name}-${stage}-${app} # Function name. The `${stage}` variable is used as a part of the resource name
  src: ./  
  handler: index.main_handler 
  runtime: Nodejs10.15 
  region: ap-guangzhou 
  events: 
    - apigw: 
        parameters:
          endpoints:
            - path: /
              method: GET
```

- Define the function `name` as `${name}-${stage}-${app}`.
- Define `stage` as `dev` for the development and testing stages. After the deployment, the function will be named `scfdemo-dev-myApp`.
- Define `stage` as `pro` for the release stage. After the deployment, the function will be named `scfdemo-pro-myApp`.
- Manipulate different function resources in different stages so as to isolate the development from release.

>?You can directly define `stage` in the `serverless.yml` file or pass in the parameter through `sls deploy --stage dev`.



## Permission Management
During project development, you need to assign permissions to different persons and manage their permissions; for example, you want a developer to access only a certain environment in a project. To this end, you can grant sub-accounts permissions to manipulate specified resources in Serverless Framework as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

Taking the `dev` environment of the `myApp` project as an example, the configuration is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "sls:*"
            ],
            "resource": "qcs::sls:ap-guangzhou::appname/myApp/stagename/dev", # `app` is `myApp`, and `stage` is `dev`
            "effect": "allow"
        }
    ]
}
```



## Grayscale Release
Grayscale release (aka canary release) is a release method that can smoothly transition between black and white. To guarantee the stability of your business in the production environment, we recommend you use grayscale release to launch projects in the production environment.

Grayscale release for serverless applications is applicable only to the SCF component and relevant components involving SCF.

You can configure the traffic rule of the SCF function whose alias is `$default` (default traffic) to configure the traffic of two function versions, where one is the `$latest` version of the function, while the other is the last published version. For more information, please see [Grayscale Release](https://intl.cloud.tencent.com/document/product/1040/37698).



## Serverless Framework Commands
From project development to release, you need to use relevant Serverless Framework commands. For more commands, please see [List of Supported Commands](https://intl.cloud.tencent.com/document/product/1040/36861).

```
# Initialize the project
sls

# Download the template project `scf-demo`. You can run `sls registry` to query the available templates
sls init scf-demo

# Download the template project `scf-demo` and initialize it as `myapp`
sls init scf-demo --name my-app 

# Deploy the application
sls deploy

# Deploy the application and specify `stage` as `dev`
sls deploy --stage  dev

# Deploy the application and print the deployment information
sls deploy --debug

# Deploy and publish the function version
sls deploy --inputs publish=trues

# Deploy and switch 20% traffic to the `$latest` version
sls deploy --inputs traffic=0.2
```



## Project Practice
For more information, please see [Developing and Launching Serverless Application](https://intl.cloud.tencent.com/document/product/1040/38253).
