Tencent Cloud SCF allows you to create and update a function as needed in multiple ways.

## Creating a Function
### Creating Function in Console
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select **Blank Function** or **Function Template** to create a function.
 - When using **Blank Function**, you need to enter the required function name and runtime environment to create the function.
 - When using **Function Template**, you need to enter the required function name, runtime environment, and configuration items in the function template to create the function.


### Creating Function in Other Ways
You can create a function as needed in more ways as detailed below:
- Use Serverless Framework CLI to create a function. For more information, please see [Creating Function on CLI](https://intl.cloud.tencent.com/document/product/583/32743) and relevant function invocation and deployment documents.
- Use VS Code to create a function. For more information, please see [Creating Function with VS Code Plugin](https://intl.cloud.tencent.com/document/product/583/32744) and relevant function invocation and deployment documents.



## Updating Function Configuration

### Updating function configuration in console
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. Select the region of the function to be updated at the top of the page and click the target function in the list to enter the function details page.
3. Switch to the function configuration page and click **Edit** in the top-right corner to enter the editing mode.
4. Modify the description, memory, timeout period, environment variable, and network configuration of the function as needed.
5. After the modification is completed, click **Save** to save the changes.
If you want to cancel, click **Cancel** to discard the changes.


### Updating function configuration on Serverless Framework CLI
1. If you want to modify the function configuration, you can directly modify the `serverless.yml` configuration file under the function root directory as shown below:
```yml
# serverless.yml
component: scf # Name of the imported component, which is required. The `tencent-scf` component is used in this example
name: scfdemo # Name of the instance created by this component, which is required
inputs:
  name: scfFunctionName
  src: ./src
  runtime: Nodejs10.15 # Runtime environment of function. Valid values: Python2.7, Python3.6, Nodejs6.10, Nodejs8.9,Nodejs12.16, PHP5, PHP7, Golang1, Java8.
  region: ap-guangzhou
  handler: index.main_handler
  events:
    - apigw:
        name: serverless_api
        parameters:
          protocols:
            - http
            - https
          serviceName:
          description: The service of Serverless Framework
          environment: release
          endpoints:
            - path: /index
              method: GET
```
2. After the modification is completed, run `sls deploy` on Serverless Framework CLI to deploy the function.


## Updating Function Code

### Updating function code in console

1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. Select the region of the function to be updated at the top of the page and click the target function in the list to enter the function details page.
3. Switch to the function code page and edit the function code in the following way:
 - For scripting languages: you can directly use the function code editor.
 - For non-scripting languages: you can submit the function code by uploading a zip package or through COS and then edit it.
4. After the modification is completed, click **Save** to save the changes.
If you want to cancel, click **Cancel** to discard the changes.

### Updating function code on Serverless Framework CLI
After the function code is modified locally, run `sls deploy` on Serverless Framework CLI to deploy the function and update the code.
>?The development mode of Serverless Framework supports updating functions synchronously. For more information, please see [Development Mode and In-cloud Debugging](https://intl.cloud.tencent.com/document/product/583/36268).



