## Overview

Serverless Web IDE is an IDE for functions launched by Tencent Cloud Serverless in partnership with CODING based on CloudStudio, an integrated development environment for browsers. It delivers an on-cloud development experience comparable to native IDEs.

Serverless Web IDE supports:

- Complete function development, deployment, and testing capabilities.
- Terminal capabilities. Common development tools such as pip and npm and programming language development environments already supported by SCF are pre-configured in it.
- The basic capabilities of a complete IDE, such as smart prompt and code autocomplete.
- User-defined IDE configuration, which ensures a consistent IDE user experience for the development of different functions.


>! 
>- We will keep the personalized configuration and code status in Serverless Web IDE for you. To ensure that function modifications will take effect, deploy the modifications to the cloud in a timely manner.
>- We recommend you use the latest version of Google Chrome to get the best IDE user experience.


## Use Directions


1. Log in to the [Serverless console](https://console.cloud.tencent.com/scf/index?rid=1) and select **Function Service** on the left sidebar.
2. In the function list, click a function name to enter the function details page.
3. On the **Function Management** page, select **Function Code** > **Online editing** to view and edit the function.

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
  - **Manual deployment**: In manual deployment mode, you can trigger function deployment to the cloud by clicking **Deploy** in the top-right corner of the IDE.
  - **Automatic deployment**: In automatic deployment mode, you can trigger function deployment to the cloud by saving the function (pressing Ctrl + S or Command + S).
- **Online dependency installation**: Currently, this feature is supported only for the Node.js runtime environment. After online dependency installation is enabled, dependencies will be installed automatically according to the configuration in `package.json` when the function is deployed. For more information, see [Online Dependency Installation](https://intl.cloud.tencent.com/document/product/583/38105).

>!
>
>- The root directory of the function is `/src`, and the deployment operation will package and upload the files in the `/src` directory by default. Place the files that you want to deploy to the cloud in the `/src` directory.
>- In automatic deployment mode, you can trigger function deployment to the cloud by saving the function. Therefore, we recommend you not enable automatic deployment for functions with traffic.

You can switch between manual and automatic deployment and enable/disable online dependency installation by selecting from the drop-down list in the operation section in the top-right corner of the IDE. **Automatic Deployment: Disabled** indicates the manual deployment mode.
![](https://main.qcloudimg.com/raw/9163631af3f336bf490092fc58f0f749.png)



### Function testing

You can click **Test** in the operation section in the top-right corner of the IDE to trigger the function and view the result in the output.

- **Select testing template**: Click **Testing Template** in the operation section of the IDE to select a function testing triggering event.
- **Create testing template**: If existing testing templates cannot meet your testing requirements, you can select **Create testing template** from the testing template drop-down list to customize a test event, which will be stored in JSON format in the `scf\_test\_event` folder in the `/src` root directory of the function and deployed to the cloud with the function as shown below:
  ![](https://main.qcloudimg.com/raw/83f22130739e5cc144a26180c010e4dd.png)


### Viewing log

You can view the function testing result in the output, including the returned data `Response`, the log `Output`, and the function execution summary `Summary`.
![](https://main.qcloudimg.com/raw/671a3995602c9dfd28ddf1cc0c963920.png)


### More operations

In addition to operations such as function deployment and testing as well as testing template adding, the list expanded by right-clicking the function file in the Resource Manager contains all operations related to the function, including:

- **Generating `serverless.yml`**: You can write the current configuration of the function into the `serverless.yml` configuration file and use the Serverless Framework command line tool for further development;
- **Discarding current modifications**: You can re-pull the function deployed in the cloud to overwrite the current workspace.

## IDE Operations

The common commands, runtime environments, and preset extensions in Serverless Web IDE and their versions are as listed below:

### Commands
<table>
<thead>
<tr>
<th style="text-align:center">Command</th>
<th style="text-align:center">Version</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center">python3</td>
<td style="text-align:center">Python 3.7.12<br>`python3` follows the latest Python 3 version by default.</td>
</tr>
<tr>
<td style="text-align:center">python37</td>
<td style="text-align:center">Python 3.7.12</td>
</tr>
<tr>
<td style="text-align:center">python36</td>
<td style="text-align:center">Python 3.6.1</td>
</tr>
<tr>
<td style="text-align:center">python27</td>
<td style="text-align:center">Python 2.7.13</td>
</tr>
<tr>
<td style="text-align:center">python</td>
<td style="text-align:center">Python 2.7.13</td>
</tr>
<tr>
<td style="text-align:center">node</td>
<td style="text-align:center">Node.js 16.13.1<br>The `node` command follows the latest Node.js version by default. Node.js 14.18, 12.16, and 10.15 are also installed in the environment. You can run the `n` command in the terminal to switch the version.</td>
</tr>
<tr>
<td style="text-align:center">php80</td>
<td style="text-align:center">PHP 8.0.13</td>
</tr>
<tr>
<td style="text-align:center">php74</td>
<td style="text-align:center">PHP 7.4.26</td>
</tr>
<tr>
<td style="text-align:center">php72</td>
<td style="text-align:center">PHP 7.2.2</td>
</tr>
<tr>
<td style="text-align:center">php56</td>
<td style="text-align:center">PHP 5.6.33</td>
</tr>
<tr>
<td style="text-align:center">php</td>
<td style="text-align:center">PHP 7.2.2</td>
</tr>
<tr>
<td style="text-align:center">pip3</td>
<td style="text-align:center">pip 22.0.4 (Python 3.7)</td>
</tr>
<tr>
<td style="text-align:center">pip37</td>
<td style="text-align:center">pip 22.0.4 (Python 3.7)</td>
</tr>
<tr>
<td style="text-align:center">pip36</td>
<td style="text-align:center">pip 21.3.1 (Python 3.6)</td>
</tr>
<tr>
<td style="text-align:center">pip</td>
<td style="text-align:center">pip 20.3.4 (Python 2.7)</td>
</tr>
<tr>
<td style="text-align:center">npm</td>
<td style="text-align:center">8.1.2</td>
</tr>
<tr>
<td style="text-align:center">Composer</td>
<td style="text-align:center">2.2.9</td>
</tr>
</tbody>
</table>

### Common tools
<table>
<thead>
<tr>
<th width="50%" style="text-align:center">Tool</th>
<th style="text-align:center">Version</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center">YARN</td>
<td style="text-align:center">1.22.18</td>
</tr>
<tr>
<td style="text-align:center">wget</td>
<td style="text-align:center">1.14</td>
</tr>
<tr>
<td style="text-align:center">Zip and unzip</td>
<td style="text-align:center">6</td>
</tr>
<tr>
<td style="text-align:center">Git</td>
<td style="text-align:center">2.24.1</td>
</tr>
<tr>
<td style="text-align:center">zsh</td>
<td style="text-align:center">5.0.2</td>
</tr>
<tr>
<td style="text-align:center">dash</td>
<td style="text-align:center">0.5.10.2</td>
</tr>
<tr>
<td style="text-align:center">make</td>
<td style="text-align:center">3.82</td>
</tr>
<tr>
<td style="text-align:center">Jupyter</td>
<td style="text-align:center">4.6.3</td>
</tr>
<tr>
<td style="text-align:center">Pylint</td>
<td style="text-align:center">1.9.5</td>
</tr>
<tr>
<td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/583/36267">Serverless Framework CLI</a></td>
<td style="text-align:center">3.2.1</td>
</tr>
</tbody>
</table>


### Runtime environments
<table>
<thead>
<tr>
<th width="50%" style="text-align:center">Runtime Environment</th>
<th style="text-align:center">Version</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center">Node.js</td>
<td style="text-align:center">16.13, 14.18, 12.16, and 10.15</td>
</tr>
<tr>
<td style="text-align:center">Python</td>
<td style="text-align:center">3.7, 3.6, and 2.7</td>
</tr>
<tr>
<td style="text-align:center">PHP</td>
<td style="text-align:center">8.0, 7.4, 7.2, and 5.6</td>
</tr>
</tbody>
</table>


### Extensions

<table>
<thead>
<tr>
<th width="50%" style="text-align:center">Extension</th>
<th style="text-align:center">Version</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center">Python</td>
<td style="text-align:center">2020.11.371526539</td>
</tr>
<tr>
<td style="text-align:center">Jupyter</td>
<td style="text-align:center">2020.12.411183155</td>
</tr>
<tr>
<td style="text-align:center">PHP-IntelliSense</td>
<td style="text-align:center">2.3.14</td>
</tr>
<tr>
<td style="text-align:center">ESLint</td>
<td style="text-align:center">2.1.13</td>
</tr>
<tr>
<td style="text-align:center">Prettier</td>
<td style="text-align:center">5.8.0</td>
</tr>
</tbody>
</table>


## Quota Limits

- IDE provides 5 GB of storage space for each user. If it is used up, you will not be able to perform write operations. Clean it up in time.
- To ensure a smooth experience, we recommend you not open more than 3 functions on multiple browser pages at the same time.

## Notes

Performing the following operations in the IDE may cause security risks such as data leakage. If you have to perform them, do so with caution:

- Install high-risk open-source components such as phpMyAdmin and Struts 2.

## FAQs

#### 1. What should I do if an exception occurs during IDE loading?
If IDE cannot be normally started due to a workspace exception, you can click **Having problems?** in the top-right corner of the IDE and click **Reset Workspace** on the pop-up page to initialize the workspace.

#### 2. What should I do if the function can be executed successfully in the terminal but fails to be executed after I click **Test**?

   The online IDE terminal and the SCF cloud runtime environment are independent of each other. The execution result returned after you click **Test** is the actual execution result of the function.

#### 3. What should I do if the result doesn't meet the expectation when I run a command in the terminal?

   If you run a dependent package installation command, make sure that you run it under the `src` directory.

   Check the command version before running a command. For the commands supported by default, see [Common commands](#ide-.E6.93.8D.E4.BD.9C).

