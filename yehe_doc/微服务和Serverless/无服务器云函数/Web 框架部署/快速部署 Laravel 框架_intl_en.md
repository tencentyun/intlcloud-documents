## Overview

This document describes how to use an HTTP-triggered function to quickly migrate a local Laravel service to the cloud.


>?This document mainly describes how to deploy in the console. You can also complete the deployment on the command line. For more information, see [Deploying Framework on Command Line](https://intl.cloud.tencent.com/document/product/583/41586).

## Prerequisites

Before using SCF, you need to sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/register) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629) first.

## Directions

### Template deployment: Quick deployment of Laravel project
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Functions** on the left sidebar.
2. Select the region and namespace where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select **Template**, enter `WebFunc` in the search box to filter all HTTP-triggered function templates, select the **Laravel template**, and click **Next**. 
4. On the **Create** page, you can view and modify the specific configuration information of the template project.
5. Click **Complete**. After creating the HTTP-triggered function, you can view its basic information on the **Function management** page.
6. Click **Trigger management** on the left to view the access path and access your deployed Laravel project as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/pAr4156_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220094135.png)
7. Click the access path URL to access the Laravel project as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/94aY9_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220094118.png)



### Custom deployment: Quick migration of local project to cloud

#### Local development

1. Refer to [Getting Started on macOS](https://laravel.com/docs/8.x#getting-started-on-macos) to set up the Laravel development environment locally.
2. Create the sample Laravel project locally. Enter the project directory and run the following command to initialize it.
<dx-codeblock>
:::  sh
composer create-project --prefer-dist laravel/laravel blog
:::
</dx-codeblock>
3. Run the following command to start the sample project locally. Below is the sample code:
<dx-codeblock>
:::  sh
$ php artisan serve --host 0.0.0.0 --port 9000
   Laravel development server started: <http://0.0.0.0:9000>
   [Wed Jul  7 11:22:05 2021] 127.0.0.1:54350 [200]: /favicon.ico
:::
</dx-codeblock>
4. Visit `http://0.0.0.0:9000` in a browser, and you can access the sample Laravel project locally as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/JQwu544_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220094225.png)



#### Deployment in cloud


Perform the following steps to make simple modifications to the initialized project, so that it can be quickly deployed through an HTTP-triggered function. The steps of project transformation are as follows:



1. **Add the `scf_bootstrap` bootstrap file**
Create the `scf_bootstrap` bootstrap file in the project root directory. This file is used to configure environment variables, specify service bootstrap commands, and make sure that your service can be started normally through this file.
>!
>- `scf_bootstrap` must have the executable permission of `755` or `777`.
>- If you want to output environment variables in the log, you need to add the `-u` parameter before the bootstrap command, such as `python -u app.py`.
2. **Modify the file read/write path**
In the SCF environment, only files in the `/tmp` directory are readable/writable. If you select other directories, write will fail due to the lack of permissions. Therefore, you need to inject environment variables in the `scf_bootstrap` file to adjust the output directory of the Laravel framework:
```
#!/bin/bash

# Inject the SERVERLESS flag
export SERVERLESS=1
# Modify the template compilation cache path, as only `/tmp` is readable/writable in SCF
export VIEW_COMPILED_PATH=/tmp/storage/framework/views
# Modify `session` to store it in the memory (array type)
export SESSION_DRIVER=array
# Output logs to `stderr`
export LOG_CHANNEL=stderr
# Modify the application storage path
export APP_STORAGE=/tmp/storage

# Initialize the template cache directory
mkdir -p /tmp/storage/framework/views
```
3. **Modify the listening address and port**
The listening port in the HTTP-triggered function must be `9000`, so you need to specify the listening port in `scf_bootstrap` through the following command:
```sh
/var/lang/php7/bin/php artisan serve --host 0.0.0.0 --port 9000
```
 The content of `scf_bootstrap` is as follows:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/2Yeg847_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221220095253.png)

4. **Deploy Laravel**
After the local configuration is completed, run the bootstrap file and make sure that your service can be normally started locally. Then, perform the following steps to deploy Laravel:
    1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Functions** on the left sidebar.
    2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
    3. Select **Create from scratch** and configure the options as prompted:
        - **Function type**: Select **HTTP-triggered function**.
        - **Function name**: Enter the name of your function.
        - **Region**: Enter your function deployment region, such as Chengdu.
        - **Runtime environment**: Select **Php7**.
        - **Submitting method**: Select **Local folder** and upload your local project.
        -**Function codes**: Select the specific local folder where the function code is.
    4. After the deployment is completed, click the generated URL to access your Laravel application as shown below: 
![](https://main.qcloudimg.com/raw/a30df3d4ef68cc608bd01871f23bfba0.png)



#### Development management

After the deployment is completed, you can quickly access and test your web service in the SCF console and try out various features of SCF, such as layer binding and log management. In this way, you can enjoy the advantages of low cost and flexible scaling brought by the serverless architecture.
