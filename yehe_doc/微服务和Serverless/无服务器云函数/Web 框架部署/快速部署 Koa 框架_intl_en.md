## Overview

This document describes how to quickly deploy a local Koa project to the cloud through an HTTP-triggered function.


>?This document mainly describes how to deploy in the console. You can also complete the deployment on the command line. For more information, see [Deploying Framework on Command Line](https://intl.cloud.tencent.com/document/product/583/41586).


## Prerequisites

Before using SCF, you need to sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/register) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629) first.


## Directions

### Template deployment: Quick deployment of Koa project

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Functions** on the left sidebar.
2. Select the region and namespace where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select **Template**, enter `koa` in the search box to filter function templates, select the **Koa template**, and click **Next**. 
4. On the **Create** page, you can view and modify the specific configuration information of the template project.
5. Click **Complete**. After creating the HTTP-triggered function, you can view its basic information on the **Function management** page.
6. Click **Trigger management** on the left to view the access path and access your deployed Koa project as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/RFtr104_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220093813.png)
7. Click the access path URL to access the Koa project as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/cQft953_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220093828.png)


### Custom deployment: Quick migration of local project to cloud


#### Prerequisites

The Node.js runtime environment has been installed locally.

#### Local development

1. Refer to the [Koa.js](https://koajs.com/) official documentation to install the Koa environment and initialize your Koa project. The following takes `hello world` as an example. The content of `app.js` is as follows:
```js
// app.js
const Koa = require('koa');
const app = new Koa();

const main = ctx => {
  ctx.response.body = 'Hello World';
};

app.use(main);
app.listen(3000);
```
2. In the root directory, run the following command to directly start the service locally.
```shell
node app.js
```
3. Visit `http://localhost:3000` in a browser, and you can access the sample Koa project locally.



#### Deployment in cloud

You need to make simple modifications to the initialized project, so that the project can be quickly deployed through an HTTP-triggered function. The project transformation here is usually divided into the following two steps:

- Change the listening address and port to `0.0.0.0:9000`.
- Add the `scf_bootstrap` bootstrap file.

The detailed directions are as follows:
1. In the sample Koa project, change the listening port to `9000` as shown below: 
![](https://main.qcloudimg.com/raw/193b4e029355a0956eb5bfcb154c9ad3.png)
2. Create the `scf_bootstrap` bootstrap file in the project root directory and add the following content to it (which is used to configure environment variables and start services):
<dx-codeblock>
:::  sh
#!/bin/bash
/var/lang/node12/bin/node app.js
:::
</dx-codeblock>
3. After the creation is completed, you need to run the following command to modify the executable permission of the file. By default, the permission `777` or `755` is required for it to start normally. Below is the sample code:
<dx-codeblock>
:::  sh
chmod 777 scf_bootstrap
:::
</dx-codeblock>
4. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Functions** on the left sidebar.
5. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
6. Select **Create from scratch** and configure the options as prompted: 
	- **Function type**: Select **HTTP-triggered function**.
	- **Function name**: Enter the name of your function.
	- **Region**: Enter your function deployment region, which is **Guangzhou** by default.
	- **Runtime environment**: Select **Nodejs 12.16**.
	- **Submitting method**: Select **Local folder** and upload your local project.
	-**Function codes**: Select the specific local folder where the function code is.
7. Click **Complete**.




#### Development management
After the deployment is completed, you can quickly access and test your web service in the SCF console and try out various features of SCF, such as layer binding and log management. In this way, you can enjoy the advantages of low cost and flexible scaling brought by the serverless architecture. 
