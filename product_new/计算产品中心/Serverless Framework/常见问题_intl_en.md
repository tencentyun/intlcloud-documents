### What is the difference between Serverless Framework and SCF?
[Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583) provides a serverless execution environment, enabling companies and developers to execute code without the need to purchase and manage servers.
Serverless Framework provides a serverless application framework combining SCF, API Gateway, databases, and other resources that enables you to write business logic directly while skipping over configuration and management of underlying resources.

### What application frameworks does Serverless Framework provide?
At present, REST APIs and basic websites have been offered, and more frameworks that fit actual application scenarios are on the way.

### What if Serverless Framework prompts that **"component" input is requires to run custom methods**?
When the Serverless Framework CLI is started, if a component is referenced in the yaml configuration file by default, you need to make sure that the folder is empty before you can run the component installation command properly.
Running the `serverless create` command again in an empty folder will not cause this error.

### What if function execution times out?
When the execution times out, the client will be disconnected and an error will be reported. You are recommended to set a limit for the function execution duration and restrain from putting time-consuming operations in functions directly invoked by the client.

### How to use SCF's built-in module?
SCF's built-in module has been integrated into the operating environment and can be used directly. Currently, the supported built-in module is “request 2.87.1”.
If this version of built-in module fails to meet your needs, you can install your own module in SCF which will be used first by default.

### Why are some logs lost during SCF testing?
- If sync invocation is used in SCF testing (with a timeout period less than 20 seconds), up to 4 KB of logs can be returned, and excessive parts will not be displayed.
- In case of async invocation (with a timeout period of 20 or more seconds), up to 6 MB of logs can be returned, and excessive parts will not be displayed.
