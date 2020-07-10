This document describes how to quickly install Serverless Framework through [binary installation](#binary) or [npm](#npm).

<span id="binary"></span>
## Method 1. Binary installation

If Node.js is not installed in your local environment, you can install it directly in binary mode:

### macOS/Linux 

Open the command line and enter the following command:
```sh
$ curl -o- -L https://slss.io/install | bash
```

If you have already installed a binary version, you can run the following command to upgrade it:
```sh
$ serverless upgrade
```

### Windows 

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

Run the following command on the command line:
```sh
$ npm install -g serverless
```
> If macOS prompts that you have no permission, you need to run `sudo npm install -g serverless` for installation.

If you have already installed Serverless Framework, you can run the following command to upgrade it to the latest version:
```sh
$ npm update -g serverless
```

After the installation is completed, run the `serverless -v` command to view the version information of Serverless Framework:
```sh
$ serverless -v
```

>If Node.js is not installed in your environment, you can install it as instructed in [Node.js Installation Guide](https://nodejs.org/zh-cn/download/) based on your system environment.



