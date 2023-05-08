## Overview

This document shows you how to create products and applications in the Tencent Push Notification Service console and how to configure applications.

## Prerequisites

You have a Tencent Cloud account. For details, see the [Sign Up for a Tencent Cloud Account](https://www.tencentcloud.com/document/product/378/17985) tutorial.

## Directions

### Creating a product

1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns), and click **Product Management** in the left sidebar.
2. On the **Product Management** page, click **Add Product**.
3. In the pop-up window, enter the product name and product description, and select a product category and service access point. For more information on service access points, see [Global Deployment](https://intl.cloud.tencent.com/document/product/1024/35233).
4. When you put a check mark next to Android, iOS, or macOS below, the system will by default create applications for the selected platform.
	 ![](https://main.qcloudimg.com/raw/463013c99e476af32767de8b2d48ff49.png)
5. Click **OK** to complete the product creation, and click **View User Guide** to integrate the product as instructed.
	 ![](https://main.qcloudimg.com/raw/e7f9a7562d4a9f147bcc7bd8ada11e91.png)

### Creating an application

After you create a product, if you have not yet added a default application, you can follow these instructions to create an application. Only one application can be created per platform. After applications have been created for all three platforms, no new applications can be created.

#### Android applications

1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns), and click **Product Management** in the left sidebar.
2. On the product list page, select the created product, click **Add Application**, and select **Android** as the platform.
3. Enter the application name, and click **OK** to create the application.
	 ![](https://main.qcloudimg.com/raw/a396a109314535259cd25fed253e73db.png)

#### iOS applications

1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns), and click **Product Management** in the left sidebar.
2. On the product list page, select the created product, click **Add Application**, and select **iOS** as the platform.
3. Enter the application name, and click **OK** to create the application.
	 ![](https://main.qcloudimg.com/raw/55933b66e480455ddbc366245ed48419.png)

#### macOS applications

1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns), and click **Product Management** in the left sidebar.
2. On the product list page, select the created product, click **Add Application**, and select **macOS** as the platform.
3. Enter the application name, and click **OK** to create the application.
	 ![](https://main.qcloudimg.com/raw/b674b49fe1aafebdd6e71e8d71487471.png)

### Configuring applications

After you create an application, you can follow the steps below to configure it.

#### Android

1. Go to the **Product List** page, select Android platform applications, and click **Configuration Management**.
2. Enter the name of the Android platform application, and click **Save** to complete basic configuration.
3. Vendor channel configurations can be enabled according to your requirements.

#### iOS

1. Go to the **Product List** page, select iOS platform applications, and click **Configuration Management**.
2. Enter the BundleID for the iOS platform, and click **Save** to complete basic configuration.
3. Go to the configuration management page, click **Upload Certificate**, enter the certificate password and select a certificate to upload.
4. Click **Submit** to upload your iOS push certificate to the management platform, and complete iOS application configuration.
	 ![](https://main.qcloudimg.com/raw/e389eda368763dcd46cd6c7b4b800c63.png)

#### macOS configuration

1. Go to the **Product List** page, select macOS platform applications, and click **Configuration Management**.
2. Enter the BundleID for the macOS platform, and click **Save** to complete basic configuration.
3. Go to the configuration management page, click **Upload Certificate**, enter the certificate password and select a certificate to upload.
4. Click **Submit** to upload your iOS push certificate to the management platform, and complete iOS application configuration.
	 ![](https://main.qcloudimg.com/raw/e389eda368763dcd46cd6c7b4b800c63.png)
### Obtaining the application information in the console

After successful configuration, you can obtain the application's **AccessID**, **AccessKey**, and **SecretKey**, which are described as follows.

#### AccessID: Unique identifier of the application. Use cases:
1. SDK integration
2. Authentication signature generation during a RESTful API call

#### AccessKey: Client authentication key of the application. Use case:
SDK Integration

#### SecretKey: Server authentication key of the application. Use case:
Authentication signature generation during a RESTful API call

