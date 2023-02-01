## Overview

This document describes how to quickly deploy a local Express project to the cloud through an HTTP-triggered function.


>?This document mainly describes how to deploy in the console. You can also complete the deployment on the command line. For more information, see [Deploying Framework on Command Line](https://intl.cloud.tencent.com/document/product/583/41586).



## Prerequisites
Before using SCF, you need to sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/account/register) and complete the [identity verification](https://www.tencentcloud.com/document/product/378/3629) first.

## Directions


### Template deployment: Quick deployment of Express project


1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Functions** on the left sidebar.
2. Select the region and namespace where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select **Template**, enter `WebFunc` in the search box to filter all HTTP-triggered function templates, select **ExpressDemo**, and click **Next** as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/gLx2086_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219155013.png)
4. On the **Create** page, you can view and modify the specific configuration information of the template project.
5. Click **Complete**. After creating the HTTP-triggered function, you can view its basic information on the **Function management** page.
6. Click **Trigger management** on the left to view the access path and access your deployed Express project as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/ebf66a5d16ecfd1470c32e1942b691cd.png)
7. Click the access path URL to access the Express project as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/enhL062_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219154911.png)




### Custom deployment: Quick migration of local project to cloud


#### Prerequisites

The Node.js runtime environment has been installed locally.

#### Local development

1. Run the following command to install the Express framework and `express-generator` scaffold and initialize the sample Express project.
```shell
npm install express --save
npm install express-generator --save
express WebApp
```
2. Run the following command to enter the project directory and install the required dependencies:
```shell
cd WebApp
npm install
```
3. After the installation is completed, run the following command to directly start the service locally.
```shell
npm start
```
4. Visit `http://localhost:3000` in a browser, and you can access the sample Express project locally.



#### Deployment in cloud

You need to make simple modifications to the initialized project, so that the project can be quickly deployed through an HTTP-triggered function. The project transformation here is usually divided into the following two steps:

- Change the listening address and port to `0.0.0.0:9000`.
- Add the `scf_bootstrap` bootstrap file.

The detailed directions are as follows:
1. In the sample Express project, you can specify the listening address and port through the environment variable in the `./bin/www` file. If you don't specify it, port **3000** will be listened on by default as shown below: 
![](https://main.qcloudimg.com/raw/a32fd560e9a6e58e6a1f6a46356324e6.png)
2. Create the `scf_bootstrap` bootstrap file in the project root directory and add the following content to it (which is used to configure environment variables and start services):
<dx-codeblock>
:::  shell
#!/bin/bash
export PORT=9000
npm run start
:::
</dx-codeblock>
3. After the creation is completed, you need to run the following command to modify the executable permission of the file. By default, the permission `777` or `755` is required for it to start normally. Below is the sample code:
<dx-codeblock>
:::  shell
chmod 777 scf_bootstrap
:::
</dx-codeblock>
4. After the local configuration is completed, run the following command to start the file (with execution in the `scf_bootstrap` directory as an example) and make sure that your service can be normally started locally.
<dx-codeblock>
:::  shell
./scf_bootstrap
:::
</dx-codeblock>
5. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Functions** on the left sidebar.
6. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
7. Select **Create from scratch** and configure the options as prompted as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/0b74aad993d675acf5a96b8900f5d0f9.png)
	- **Function type**: Select **HTTP-triggered function**.
	- **Function Name**: Enter the name of your function.
	- **Region**: Enter your function deployment region, which is **Guangzhou** by default.
	- **Runtime environment**: Select **Nodejs 12.16**.
	- **Submitting method**: Select **Local folder** and upload your local project.
	-**Function codes**: Select the specific local folder where the function code is.
8. Click **Complete**.



#### Development management
After the deployment is completed, you can quickly access and test your web service in the SCF console and try out various features of SCF, such as layer binding and log management. In this way, you can enjoy the advantages of low cost and flexible scaling brought by the serverless architecture as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ebH5264_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219161310.png)