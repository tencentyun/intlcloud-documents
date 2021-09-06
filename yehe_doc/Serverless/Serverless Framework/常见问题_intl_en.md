### What is Serverless Framework?
Well-received in the industry, Serverless Framework allows you to deploy a complete, available serverless application framework without the need to care about underlying resources. It features resource orchestrating, auto scaling, and event driving and covers the full development lifecycle from coding and debugging to testing and deploying, helping you quickly build serverless applications with the aid of Tencent Cloud resources. For more information, please see [Product Overview](https://intl.cloud.tencent.com/document/product/1040/33150).

### Is Serverless Framework a paid service?
Currently, Serverless Framework is free of charge, but the Tencent Cloud services used by it will be charged by resource usage following their respective billing rules. For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1040/33152).

### What is the difference between Serverless Framework and SCF?
[Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583) provides a serverless execution environment, enabling companies and developers to execute code without the need to purchase and manage servers.
Serverless Framework provides a serverless application framework combining SCF, API Gateway, COS, TencentDB, and other resources that enables you to write business logic directly while skipping over configuration and management of underlying resources.

### What application frameworks does Serverless Framework provide?
Currently, Serverless Framework Component provides various applications such as RESTful API and static website deployment. It supports web frameworks in multiple programming languages such as Koa, Express, React, Vue, and SSR-related Next.js and Nuxt.js for Node.js; WSGI frameworks like Flask and Django for Python; and Laravel and ThinkPHP for PHP. More frameworks that fit actual application scenarios will be supported soon.

### What should I do if Serverless Framework prompts that `"component" input is requires to run custom methods`?
When the Serverless Framework CLI is started, if a component is referenced in the `yaml` configuration file by default, you need to make sure that the folder is empty before you can run the component installation command properly.
Running the `serverless create` command again in an empty folder will not cause this error.

If you have any other questions or feedback, please visit [GitHub Repository Issues](https://github.com/serverless-components?q=tencent).

### What should I do if Serverless Framework prompts that `The appid is unavailable for legal reasons.`?

This error is caused by overdue account, as it is impossible to create pay-as-you-go resources. Please check whether your account is overdue. This error can be resolved by topping up your account to a positive balance.

### What should I do if I have no operate permission in the Window Powershell?
nder the strict permission management of Window Powershell, you only need to run the `set-executionpolicy remotesigned` command for the deployment. In Windows, we recommend using the `serverless deploy`  command.

### How do I deploy if my development environment is outside Mainland China?
Problem: Serverless Framework checks whether the user is in Mainland China by default during deployment. If your development environment is outside Mainland China and you want to use the Mainland China edition of Serverless Framework, you can configure it as follows:

Solution: add `SERVERLESS_PLATFORM_VENDOR=tencent` in the `.env` file to start the Mainland China edition by default, which provides an interactive quick deployment process (for more information, please see [Getting Started](https://intl.cloud.tencent.com/document/product/1040/36249)).

### What should I do if Serverless Framework prompts that `Cannot get secretId/Key, your account could be sub-account or does not have access`?
Problem: the error message is `Cannot get secretId/Key, your account could be sub-account or does not have access, please check if SLS_QcsRole role exists in your account, and visit https://console.cloud.tencent.com/cam to bind this role to your account.` 

Solution: this error is caused by insufficient account permissions. You can update the configuration as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).
If you have any other questions or feedback, please submit a [ticket](https://console.cloud.tencent.com/workorder/category) or [GitHub issue(https://github.com/serverless-components?q=tencent) for assistance.

### How do I deploy if my environment does not have permission to access the public network and can access the public network only through a proxy?

Problem: your environment does not have permission to access the public network and can access the public network only through a proxy, and a network failure is reported when `sls deploy` is executed.

Solution: add the following configuration to the `.env` file
```
HTTP_PROXY=http://127.0.0.1:12345 # Your proxy
HTTPS_PROXY=http://127.0.0.1:12345 # Your proxy
```
123
