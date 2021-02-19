## Overview
You can quickly install Serverless Framework through [npm](#npm) or [binary installation](#binary).


## Installation

[](id:npm)
### Method 1. Installation through npm
#### Prerequisites
Before installing through npm, you need to make sure that Node.js (above v10) and npm have been installed in your environment (for more information, please see [Node.js Installation Guide](https://nodejs.org/zh-cn/download/)) .
```sh
$ node -v
v12.18.0

$ npm -v
7.0.10
```

>!To ensure the installation speed and stability, we recommend you use cnpm for installation: download and install cnpm first, and then replace all the npm commands used below with cnpm commands.

#### Installation steps

Run the following command on the command line:
```sh
npm install -g serverless
```
>?If macOS prompts that you have no permission, you need to run `sudo npm install -g serverless` for installation.

If you have already installed Serverless Framework, you can run the following command to upgrade it to the latest version:
```sh
npm update -g serverless
```

#### Viewing version information
After the installation is completed, run the `serverless -v` command to view the version information of Serverless Framework:
```sh
serverless -v
```


[](id:binary)
### Method 2. Binary installation

If Node.js is not installed in your local environment, you can install it directly in binary mode:

#### macOS/Linux 

Open the command line and enter the following command:
```sh
curl -o- -L https://slss.io/install | bash
```

If you have already installed a binary version, you can run the following command to upgrade it:
```sh
serverless upgrade
```

#### Windows 

Windows supports installation through [Chocolatey](https://chocolatey.org/). Open the command line and enter the following command:

```sh
choco install serverless
```
If you have already installed a binary version, you can run the following command to upgrade it:
```sh
choco upgrade serverless
```


#### Viewing version information
After the installation is completed, run the `serverless -v` command to view the version information of Serverless Framework:
```sh
serverless -v
```

## Relevant Operations
Next step: getting started
 - [Quick Deployment of Function Template](https://intl.cloud.tencent.com/document/product/1040/39133)
 - [Quick Creation of Application Template](https://intl.cloud.tencent.com/document/product/1040/39134)


