
You can install Serverless Cloud Framework through npm.




[](id:npm)
## Installing via npm
#### Prerequisites
Before installing through npm, you need to make sure that Node.js (**later than v12**) and npm have been installed in your environment (for more information, see [Node.js Installation Guide](https://nodejs.org/zh-cn/download/)) .
```sh
$ node -v
v12.18.0

$ npm -v
7.0.10
```

>!
>- To ensure the installation speed and stability, we recommend you use cnpm for installation: download and install cnpm first, and then replace all the npm commands used below with cnpm commands.
>- `scf` is short for the `serverless-cloud-framework` command.

#### Installation steps

Run the following command on the command line:
```sh
npm i -g serverless-cloud-framework
```
>?If macOS prompts that you have no permission, you need to run `sudo npm i -g serverless-cloud-framework` for installation.

If you have already installed Serverless Cloud Framework, you can run the following command to upgrade it to the latest version:
```sh
npm update -g serverless-cloud-framework
```

#### Viewing version information
After the installation is completed, run the `scf -v` command to view the version information of Serverless Cloud Framework:
```sh
scf -v
```


[](id:binary)
## Relevant Operations
Next step: Getting started
 - [Quick Deployment of Function Template](https://intl.cloud.tencent.com/document/product/1040/39133)
 - [Quick Creation of Application Template](https://intl.cloud.tencent.com/document/product/1040/39134)

