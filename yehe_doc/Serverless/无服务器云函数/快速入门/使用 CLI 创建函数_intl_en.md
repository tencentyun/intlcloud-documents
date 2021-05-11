## Overview
This document describes how to use the SCF component provided by Serverless Framework to quickly create and deploy an SCF project. For more information on components and how to use them, please see [Components Overview](https://intl.cloud.tencent.com/document/product/1040/33163)
>?The SCF CLI tool has been disused since February 2020. We recommend you use the more rich-featured and convenient Serverless Framework CLI tool for project development.
>

## Prerequisites
- Serverless Framework has been installed. For more information, please see [Installing Serverless Framework](https://intl.cloud.tencent.com/document/product/583/36263).
- Your account has the Serverless Framework permissions. For more information, please see [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/583/36270).

## Directions

### Creating function
Run the following command to quickly create a function in the Node.js language: 
```
sls init scf-demo
```
>?`scf-demo` in the command is the Node.js template by default, and you can replace it with function templates in other languages, such as `scf-golang`, `scf-php`, and `scf-python`.

### Deploying function
Run the following command in the `scf-demo` directory to deploy the function:
```
sls deploy
```
A QR code will pop up. Please scan it to authorize and start deployment. After successful deployment, SCF resources will be automatically created.
>?If authentication fails, please authorize as instructed in [Account and Permission Configuration](https://intl.cloud.tencent.com/document/product/1040/36793).

### View function information
Run the following command to view the information of the deployed SCF resources:
```
sls info
```

### Removing function
Run the following command to remove the deployed SCF resources:
```
sls remove
```
>?For more information on how to use Serverless Framework CLI to manipulate SCF functions, please see [Serverless Framework CLI](https://intl.cloud.tencent.com/document/product/583/36267).
