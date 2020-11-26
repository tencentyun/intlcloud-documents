This document describes how to quickly install Serverless Framework through [binary installation](#binary) or [npm](#npm).

## Installation Methods
<span id="binary"></span>
### Method 1. Binary installation

If Node.js is not installed in your local environment, you can install it directly in binary mode:

>!Starting from September 1, 2020, Serverless components are no longer supported for Node.js 10.0 or above, please upgrade as needed.
### macOS/Linux 

Open the command line and enter the following command:
```sh
$ curl -o- -L https://slss.io/install | bash
```

If you have already installed a binary version, you can run the following command to upgrade it:
```sh
$ serverless upgrade
```

#### Windows 

Windows supports installation through [Chocolatey](https://chocolatey.org/). Open the command line and enter the following command:

```sh
$ choco install serverless
```
If you have already installed a binary version, you can run the following command to upgrade it:
```sh
$ choco upgrade serverless
```

<span id="npm"></span>
## Method 2. Installation through npm
>!It is recommended that you use Node.js 10.0 or above; otherwise, errors may occur during Component V2 deployment.

Run the following command on the command line:
```sh
$ npm install -g serverless
```
>? If macOS prompts that you have no permission, you need to run `sudo npm install -g serverless` for installation.

If you have already installed Serverless Framework, you can run the following command to upgrade it to the latest version:
```sh
$ npm update -g serverless
```
Please make sure Node.js is installed in your system environment as instructed in [Node.js Installation Guide](https://nodejs.org/zh-cn/download/).
## View Version Information
After the installation is completed, run the `serverless -v` command to view the version information of Serverless Framework:
```sh
$ serverless -v
```




