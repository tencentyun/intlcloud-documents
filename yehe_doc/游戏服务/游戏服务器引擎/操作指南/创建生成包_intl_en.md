## Overview

This document describes how to create an asset package, which will be uploaded to and deployed in GSE for game hosting.

## Prerequisites

You have completed the [GSE Application Form](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6) and your application has been approved.

## Directions

1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and click **Asset** on the left sidebar.
2. Click **Create** in the top-left corner.
3. You can create an asset package by uploading one on the console page ("Page Upload") .

#### Page upload
Enter the basic asset package information, such as name and version, select the OS and the submission mode, upload the code, and click **OK**.
   - Asset Package Name: descriptive name of the asset package to be created, which does not need to be unique and can be modified and updated.
   - Asset Package Version: detailed information of asset package version, which is used to distinguish between different asset package versions.
   - OS: OS on which the game server asset package runs. It cannot be modified after the asset package is created and is CentOS 7.16 by default.
   - Submission Mode: currently, only local upload zip package is supported.
   - Upload Codes: the asset package requires [integrating gRPC Framework](https://intl.cloud.tencent.com/document/product/1055/37418). The asset package directory must contain all the components necessary for running your game server, including executable files, dependency packages, and installation scripts of the game server. It needs to be compressed into a zip package.
     - Server executable: a file required for running the game server. The asset package can contain multiple server executables, provided that they are built for the same platform.
     - Dependency: any file required for running the server executable.
     - Installation script: script used to execute the tasks for installing the asset package on the GSE-hosted server. This file must be placed in the root directory of the asset package and will run once during fleet creation.
![](https://main.qcloudimg.com/raw/776e5e422d9ce4afb68de44356e4a303.png)



4. After the asset package is successfully created, you can edit or delete it, [create a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675) for it, or perform other operations on the asset list page.

