Tencent Cloud SCF allows you to create and update a function as needed in multiple ways.

## Creating a Function
### Creating function in the console
1. Log in to the [Serverless console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select **Custom** or **Template** to create a function.
 - If you select **Custom**, you need to enter the required function name and runtime environment to create the function.
 - If you select **Template**, you need to enter the required function name, runtime environment, and configuration items in the function template to create the function.


### Creating function in other ways
You can create a function as needed in more ways as detailed below:
- Use Serverless Cloud Framework to create a function. For more information, see [Creating Function on CLI](https://intl.cloud.tencent.com/document/product/583/32743) and relevant function invocation and deployment documents.



## Function Configuration Update

### Updating function configuration in the console
1. Log in to the [Serverless console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
2. Select the region of the function to be updated at the top of the page and click the target function in the list to enter the function details page.
3. Switch to the function configuration page and click **Edit** in the top-right corner to enter the editing mode.
4. Modify the description, memory, timeout, environment variable, and network configuration of the function as needed.
5. After completing the modification, click **Save**.
To cancel the modification, click **Cancel**.


### Updating function configuration on Serverless Cloud Framework
1. To modify the function configuration, directly modify the `serverless.yml` configuration file under the function root directory as shown below:

```yml
# serverless.yml
component: scf # Name of the imported component, which is required. The `tencent-scf` component is used in this example
name: scfdemo # Name of the instance created by this component, which is required


inputs:
  name: scfFunctionName
  src: ./src
  runtime: Nodejs10.15 # Runtime environment of function. Valid values: Python2.7, Python3.6, Nodejs6.10, Nodejs8.9, Nodejs10.15, Nodejs12.16, PHP5, PHP7, Golang1, Java8
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
          description: The service of Serverless Cloud Framework
          environment: release
          endpoints:
            - path: /index
              method: GET
```
2. After completing the modification, run `scf deploy` on Serverless Cloud Framework to deploy the function.


## Function Code Update

### Updating function code in the console

1. Log in to the [Serverless console](https://console.cloud.tencent.com/scf) and click **Functions** on the left sidebar.
2. Select the region of the function to be updated at the top of the page and click the target function in the list to enter the function details page.
3. Switch to the function code page and edit the function code in the following way:
 - For scripting languages: You can directly use the function code editor.
 - For non-scripting languages: You can submit the function code by uploading a zip package or through COS and then edit it.
4. After completing the modification, click **Save**.
To cancel the modification, click **Cancel**.

### Updating function code on Serverless Cloud Framework
After the function code is modified locally, run `scf deploy` on Serverless Cloud Framework to deploy the function and update the code.
>?The development mode of Serverless Cloud Framework supports updating functions synchronously. For more information, see [Development Debugging](https://intl.cloud.tencent.com/document/product/583/36268).



