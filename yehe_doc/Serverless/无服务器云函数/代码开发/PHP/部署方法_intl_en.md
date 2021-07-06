## Overview

Tencent Cloud SCF provides the following function deployment methods. For more information about how to create and update a function, see [Create and Update a Function](https://intl.cloud.tencent.com/document/product/583/19806).

- Uploading and deploying a ZIP package, as instructed in [Installing and Deploying Dependencies](#install)
- Editing and deploying functions via the console, as instructed in [Deployment Through Console](https://intl.cloud.tencent.com/document/product/583/32741).
- Using the command line, as instructed in [Deployment Through Serverless Framework CLI](https://intl.cloud.tencent.com/document/product/583/32741).



## Installing and Deploying Dependencies[](id:install)

Currently, the SCF standard PHP only supports writing to the `/tmp` directory, and other directories are read-only. Therefore, you need to install, package and upload the local dependent library for use. The PHP dependency package can be uploaded with function codes to the cloud.



### Locally installing dependency packages

#### Dependency manager

In PHP, dependencies can be managed with the composer package manager.

#### Directions

1. Create a local folder `/code` to store the codes and dependent files, and create the dependency package configuration file `composer.json` in the code root directory and configure the dependency information. Here takes the installation of `requests` as an example, and the `composer.json` file is as follows:
<dx-codeblock>
:::  json
{
	"require": {
		"rmccue/requests": ">=1.0"
	}
}
:::
</dx-codeblock>
2. Run the following command in the '/code' folder to install according to the dependent package and version specified in the configuration file.
```sh
composer install
```
 <dx-alert infotype="notice" title="">
Because the function is running on CentOS 7, install the dependency package in the same environment to avoid errors. For detailed directions, see [Using Container Image](https://intl.cloud.tencent.com/document/product/583/39009).
</dx-alert>



### Packaging and uploading

You can upload dependencies together with the project, and use them through the `require` statement in function codes.

The zip package for deploying functions can be generated automatically by a local folder via the console or manually. All the packaging should be under the project directory to place codes and dependencies in the root directory of the zip package. For more information, see [Packaging requirements](https://intl.cloud.tencent.com/document/product/583/32741).
