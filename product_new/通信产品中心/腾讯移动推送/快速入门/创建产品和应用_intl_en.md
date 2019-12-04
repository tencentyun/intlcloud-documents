## Operation scenarios
This document guides you in how to create products and applications in the TPNS Console.

## Prerequisites
You have a Tencent Cloud account. For details, see the [Sign Up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985) tutorial.



## Directions
### Creating a product
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns), and click **Product Management** in the left sidebar.
2. Enter the **Product Management** page, and click **Add a Product**.
3. Enter the **Add a Product** page, and enter the product name and product details. Select the product type, and add any additional information such as the enterprise name and contact method.
4. Click **OK** to create the product.
![](https://main.qcloudimg.com/raw/5287576e5f84d3d76defb12ae488c63b.png)


## Creating an application
After you create a product, you can follow these instructions to create an application. Only one application can be created per platform. After applications have been created for all three platforms, no new applications can be created.
#### Android applications
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns), and select **Application Management** > **Application List** in the left sidebar.
2. Enter the **Application List** page, and select the product you have created. Click **Create an Application**.
3. Enter the **Create an Application** page, enter the application name, and check off the platform **Android**.
4. Enter the application package name, and configure a third-party channel (optional).
![](https://main.qcloudimg.com/raw/760969260ae6bda7b55a82adb5d2f76b.png)
5. After entering all needed information, click **OK** to create the Android application.



#### iOS applications
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns), and select **Application Management** > **Application List** in the left sidebar.
2. Enter the **Application List** page, and select the product you have created. Click **Create an Application**.
3. Enter the **Create an Application** page, enter the application name, and check off the platform **iOS**. Then click **OK and Upload Certificate**.
![](https://main.qcloudimg.com/raw/6d3601fe62081955cb575aec267289b6.png)
4. Enter the **Edit Application** page, and enter the Bundle ID and push certificate password. Click **Upload Certificate** and upload a certificate file with a “.p12” suffix. For more information, see [iOS Push Certificates](https://cloud.tencent.com/document/product/548/36664).
![](https://main.qcloudimg.com/raw/c93ef2fa5c51e6a98ee1fba98fd27eb9.png)
5. Click **OK** to create the iOS application.

#### macOS applications
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns), and select **Application Management** > **Application List** in the left sidebar.
2. Enter the **Application List** page, and select the product you have created. Click **Create an Application**.
3. Enter the **Create an Application** page, enter the application name, and check off the platform **macOS**. Then click **OK and Upload Certificate**.
![](https://main.qcloudimg.com/raw/035516a4f5179f315090e2afd41e08d1.png)
4. Enter the **Edit Application** page, and enter the Bundle ID and push certificate password. Click **Upload Certificate** and separately upload the macOS developer environment certificate and the production environment certificate. For more information, see [macOS Push Certificates](https://cloud.tencent.com/document/product/548/37095).
![](https://main.qcloudimg.com/raw/0237161819b29ef2b38f02aa3b270106.png)
5. Click **OK** to create the macOS application.


