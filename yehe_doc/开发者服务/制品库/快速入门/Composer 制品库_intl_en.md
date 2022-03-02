This document describes how to store Composer artifacts in CODING-AR for centralized artifact management and version control. The following sections introduce how to create an artifact, configure authentication, and pull and push artifacts.

## Open CODING-AR

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Preparations

>! Before you begin:
> -   Install Composer.
> -   Create an artifact repository (see [Basic Operations](https://intl.cloud.tencent.com/document/product/1136/44804)).
> -   Select Composer as the repository type.

## Create a Composer Package (Optional) [](id:composer)

### Install Composer
Run the following command to install Composer.
<dx-codeblock>
:::  bash
curl -sS https://getcomposer.org/installer | php
:::
</dx-codeblock>
Add an environment variable for global access.
<dx-codeblock>
:::  bash
mv composer.phar /usr/local/bin/composer
:::
</dx-codeblock>


### Initialize[](id:init)
Create a demo directory.
<dx-codeblock>
:::  bash
mkdir composer-demo && cd composer-demo
:::
</dx-codeblock>
Initialize the Composer package. Enter the required information when asked.
<dx-codeblock>
:::  bash
composer inits
:::
</dx-codeblock>
After initialization, a `composer.json` configuration file will be added to the directory.

## Configure the Authentication File
Go to the directory where the Composer package is located and create an `auth.json` file. You can select manual or automatic configuration.

### Automatic configuration
Click **Generate configuration from access token** and then copy the content to the `auth.json` file.
![](https://qcloudimg.tencent-cloud.cn/raw/de3c2d8f5e423d7ed9120c8e63920b2a.png)

### Manual configuration
Copy the commands on the webpage and replace `[PASSWORD]` with your service password.

## Push an Artifact
Run the commands on the CODING-AR page to compress Composer package files into a `zip` package and then push it to the repository using tools such as `cURL`.
![](https://qcloudimg.tencent-cloud.cn/raw/2099fd7d7ae9093514680135a78c54a8.png)
Enter the password configured in `auth.json` and replace `<version>` with the specific version number.
![](https://qcloudimg.tencent-cloud.cn/raw/bbdee0cef010657e77dce17be10fb0e3.png)
After the push is successful, you can view the package in CODING-AR.
![](https://qcloudimg.tencent-cloud.cn/raw/995c325e351c4ad52eba95ef47817d5e.png)

## Pull an Artifact
Go to the Composer package directory and set the repository URL. You can use the commands in CODING.
![](https://qcloudimg.tencent-cloud.cn/raw/e3920b43e9582a9edaec8d8ec5e13aba.png)

Replace the Composer source with the CODING repository (optional).
<dx-codeblock>
:::  bash
composer config repo.packagist false
:::
</dx-codeblock>
Replace `<package>` with the package to be pulled and run the pull command.
<dx-codeblock>
:::  bash
composer require < PACKAGE >:< VERSION >
:::
</dx-codeblock>
Enter your service email address and password to pull the package.
<img src = "https://qcloudimg.tencent-cloud.cn/raw/1a0558b99d6698d8a763d16191f3481c.png" style="width: 100%">

## Configure a Proxy
If you try to pull an artifact that does not exist in the CODING private repository, the system will try to pull from the configured proxy. You can add a third-party artifact source to obtain artifacts from the specific repository. Without the need for configuration, CODING will retrieve artifacts in sequence from top to bottom.
![](https://qcloudimg.tencent-cloud.cn/raw/9d9df265987bbbedd471f71a46dbb009.png)

