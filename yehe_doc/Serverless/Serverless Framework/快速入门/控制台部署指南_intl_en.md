## Overview

For common framework components, you can quickly develop and deploy your applications in the [Serverless SSR console](https://console.cloud.tencent.com/sls?from=quickstart).

#### Currently supported frameworks
- Express
- WordPress
- Koa
- Egg.js
- Next.js
- Nuxt.js
- Flask
- Laravel
- SpringBoot

## Prerequisites
Before deploying your application in the console, you must complete the following permission configuration:

#### Authorizing by root account
1. Log in to the [Serverless SSR console](https://console.cloud.tencent.com/sls?from=quickstart) and click **Authorize** to enter the CAM console.
2. On the **Role** list page in the CAM console, check whether the **SLS_QcsRole** and **CODING_QCSRole** service roles have been created successfully.
>!If you have already created `CODING_QCSRole`, please check whether it has complete permissions. It requires the following basic policies: `QcloudSLSFullAccess`, `QcloudSSLFullAccess`, and `QcloudAccessForCODINGRole`. If any policy is missing, please add it manually.
3. You can start to use the service after making sure that both the roles and permissions meet the requirements.

#### Granting permissions to sub-account
If the **Serverless Framework** and **Coding DevOps** services haven't been activated yet, please contact the root account to activate them and create the roles (as instructed in [Directions](#1)).


## Directions
### Step 1. Create an application
1. Log in to the [SSR console](https://console.cloud.tencent.com/ssr).
2. Click **Create Application** to enter the project creation page.
3. Enter the basic application information as prompted on the page.
 - Application Name: it can contain 2–63 lowercase letters, digits, and hyphens and must start with a lowercase letter and end with a digit or lowercase letter. It cannot be changed once the application is created.
 - Environment: select `dev`, `test`, or `prod`. Custom environment is also supported.
 - Region: it is the same as the region supported by SCF. For more information, please see [Region List](https://intl.cloud.tencent.com/document/api/583/17238).
 - Creation Method: you can create an application from an **[application template](#1)** or by **[importing an existing project](#2)**. You can choose either method based on your actual needs.
>?If you choose to create an application by importing an existing project, you need to make certain modifications to some frameworks. For more information, please see the relevant framework migration documentation.
4. Click **Create**, and the application will be automatically deployed for you. You can view the deployment log of the project.

<span id="1"></span>
#### Creating application from application template

If you choose to create an application from a template, you can quickly create a web application by selecting a project template provided in the console. During template-based deployment, the following configuration will be completed for you by default:
1. Create a layer (**for the Node.js framework only**) and store the project dependency package `node_modules` in the layer. For more information on how to use a layer, please see [Overview](https://intl.cloud.tencent.com/document/product/583/37039).
2. Create a COS bucket (**for Next.js and Nuxt.js frameworks only**), separate the static resources, and host them in the COS bucket.

You can also configure more capabilities for your project in **Advanced Configuration**, such as custom domain name and detailed function configuration.

>?When configuring a custom domain name, please make sure that an ICP filing has been obtained and a CNAME record has been configured for it. For more information, please see [Custom Domain Name and Certificate](https://intl.cloud.tencent.com/document/product/628/11791).

 <span id="2"></span>
 #### Importing existing project
 The Serverless console allows you to migrate an existing project through **code hosting** and **folder upload**.

 - Code hosting
 Currently, **GitHub, GitLab, Gitee**, and public custom code repositories are supported. You can have your application automatically updated by selecting the trigger method for it.

 - Folder upload
 You can directly import a local project by uploading the folder. For the Node.js framework, Serverless Framework will automatically create a layer and pass the dependency package `node_modules` into the layer to complete the deployment.




### Step 2. Manage resources
On the [Serverless SSR](https://console.cloud.tencent.com/ssr) page, click the target application to enter the application details page and view the basic information output after the project is deployed as well as monitoring metric data such as the number of requests and error statistics. This makes it easy for you to manage your project.



### Step 3. Deploy for development
Click **Deploy** at the top of the application details page, and you can quickly modify the configuration of your project and upload it for re-deployment. Three methods are supported: **local upload, code hosting, and CLI development**.
