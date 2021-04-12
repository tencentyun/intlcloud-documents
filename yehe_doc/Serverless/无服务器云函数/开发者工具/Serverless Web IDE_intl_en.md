

## Overview

Serverless Web IDE is an IDE for functions launched by Tencent Cloud Serverless in partnership with CODING based on CloudStudio, an integrated development environment for browsers. It delivers an on-cloud development experience comparable to native IDEs.

Serverless Web IDE supports:

- Complete function development, deployment, and testing capabilities.
- Terminal capabilities. Common development tools such as pip and npm and programming language development environments already supported by SCF are pre-configured in it.
- The basic capabilities of a complete IDE, such as smart prompt and code autocomplete.
- User-defined IDE configuration, which ensures a consistent IDE user experience for the development of different functions.


>! 
>- We will keep the personalized configuration and code status in Serverless Web IDE for you. To ensure that function modifications will take effect, please deploy the modifications to the cloud in a timely manner.
>- We recommend you use the latest version of Google Chrome to get the best IDE user experience.


## How to Use


1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. In the function list, click a function name to enter the function details page.
3. On the **Function Management** page, select **Function Code** > **Edit Code** to view and edit the function.

## Overview

This document describes the Serverless Web IDE tool in detail as shown below in order from left to right:
![](https://main.qcloudimg.com/raw/7b1bf95f8cc2b1640fa3184784fafae5.png)

1. **Resource Manager**
2. **File editing section**
3. **Function operation section**
4. **Command line terminal**


## Function Operations

In Serverless Web IDE, you can edit, deploy, and test function code. Common operations such as function testing and deployment and testing template selection are configured in the operation section in the top-right corner of the IDE as shown below:
![](https://main.qcloudimg.com/raw/c7ebb49e0b7a9ed4825c8d064704325c.png)

### Function deployment

Serverless Web IDE enables you to deploy a function either manually or automatically and to install dependencies online.

- **Deployment mode**:
  - **Manual deployment**: in manual deployment mode, you can trigger function deployment to the cloud by clicking **Deploy** in the top-right corner of the IDE.
  - **Automatic deployment**: in automatic deployment mode, you can trigger function deployment to the cloud by saving the function (pressing Ctrl + S or Command + S).
- **Online dependency installation**: currently, this feature is supported only for the Node.js runtime environment. After online dependency installation is enabled, dependencies will be installed automatically according to the configuration in `package.json` when the function is deployed. For more information, please see [Online Dependency Installation](https://intl.cloud.tencent.com/document/product/583/38105).
>!
>- The root directory of the function is `/src`, and the deployment operation will package and upload the files in the `/src` directory by default. Please place the files that you want to deploy to the cloud in the `/src` directory.
>- In automatic deployment mode, you can trigger function deployment to the cloud by saving the function. Therefore, we recommend you not enable automatic deployment for functions with traffic.

You can switch between manual and automatic deployment and enable/disable online dependency installation by selecting from the drop-down list in the operation section in the top-right corner of the IDE. **Automatic Deployment: Disabled** indicates the manual deployment mode.
![](https://main.qcloudimg.com/raw/9163631af3f336bf490092fc58f0f749.png)



### Function testing

You can click **Test** in the operation section in the top-right corner of the IDE to trigger the function and view the result in the output.

- **Select testing template**: click **Testing Template** in the operation section of the IDE to select a function testing triggering event.
- **Create testing template**: if existing testing templates cannot meet your testing requirements, you can select **Create testing template** from the testing template drop-down list to customize a test event, which will be stored in JSON format in the `scf\_test\_event` folder in the `/src` root directory of the function and deployed to the cloud with the function as shown below:
![](https://main.qcloudimg.com/raw/83f22130739e5cc144a26180c010e4dd.png)


### Viewing log

You can view the function testing result in the output, including the returned data `Response`, the log `Output`, and the function execution summary `Summary`.
![](https://main.qcloudimg.com/raw/671a3995602c9dfd28ddf1cc0c963920.png)


### More operations

In addition to operations such as function deployment and testing as well as testing template adding, the list expanded by right-clicking the function file in the Resource Manager contains all operations related to the function, including:
- **Generating `serverless.yml`**: you can write the current configuration of the function into the `serverless.yml` configuration file and use the Serverless Framework command line tool for further development;
- **Discarding current modifications**: you can re-pull the function deployed in the cloud to overwrite the current workspace.

## IDE Operations

The extensions, common tools, and runtime environments configured in Serverless Web IDE and their versions are as follows:

### Common tools

|                             Tool                             |   Version   |
| :----------------------------------------------------------: | :------: |
|                             npm                              |  6.14.8  |
|                             Yarn                             | 1.22.10  |
|                             pip                              |  20.2.3  |
|                             wget                             |   1.14   |
|                          zip and unzip                          |    6     |
|                             Git                              |  2.24.1  |
|                             zsh                              |  5.0.2   |
|                             Dash                             | 0.5.10.2 |
|                             make                             |   3.82   |
|                           Jupyter                            |  4.6.3   |
|                            Pylint                            |  1.9.5   |
| [Serverless Framework CLI](https://intl.cloud.tencent.com/document/product/583/36267) |  3.2.1   |

### Runtime environments

| Runtime Environment | Version  |
| :------: | :---: |
| Node.js  | 12.16 |
|  Python  |  3.6  |
|   PHP    |  7.2  |
|   Java   |  1.8  |
|  Go  | 1.14  |

### Extensions

|       Extension       |       Version        |
| :--------------: | :---------------: |
|      Python      | 2020.11.371526539 |
|     Jupyter      | 2020.12.411183155 |
| PHP-IntelliSense |      2.3.14       |
|      ESLint      |      2.1.13       |
|     Prettier     |       5.8.0       |

## Quota Limits
- IDE provides 5 GB of storage space for each user. If it is used up, you will not be able to perform write operations. Please clean it up in time.
- To ensure a smooth experience, we recommend you not open more than 3 functions on multiple browser pages at the same time.

## Notes

Performing the following operations in the IDE may cause security risks such as data leakage. If you have to perform them, please do so with caution:
- Install high-risk open-source components such as phpMyAdmin and Struts 2.
