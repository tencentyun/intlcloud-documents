This document describes how to quickly install Serverless Framework through [binary installation](#binary) or [npm](#npm).

## Installing
<span id="binary"></span>
### Method 1. Binary installation

If Node.js is not installed in your local environment, you can install it directly in binary mode:
>!You are recommended to use Node.js 10.0 or above; otherwise, Component v2 may report errors during deployment.

#### macOS/Linux 

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
### Method 2. Installation through npm
>!You are recommended to use Node.js 10.0 or above; otherwise, Component v2 may report errors during deployment.

Run the following command on the command line:
```sh
$ npm install -g serverless
```
>?If macOS prompts that you have no permission, you need to run `sudo npm install -g serverless` for installation.

If you have already installed Serverless Framework, you can run the following command to upgrade it to the latest version:
```sh
$ npm update -g serverless
```

If Node.js is not installed in your environment, you can install it as instructed in [Node.js Installation Guide](https://nodejs.org/en/download) based on your system environment.



## Viewing Version Information
After the installation is completed, run the `serverless -v` command to view the version information of Serverless Framework:
```sh
$ serverless -v
```
