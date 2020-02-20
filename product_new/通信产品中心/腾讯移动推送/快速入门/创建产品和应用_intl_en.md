
## Operation Scenarios
This document shows you how to create products and applications in the TPNS Console and how to configure applications.

## Prerequisites
You have a Tencent Cloud account. For details, see the [Sign Up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985) tutorial.

## Steps
### Creating a product
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns), and click **Product Management** in the left sidebar.
2. Go to the **Product Management** page and click **Add a Product**.
3. Go to the **Add a Product** page, enter the product name and product details, and select the product type.
4. When you put a check mark next to Android, iOS, or macOS below, the system will by default create applications for the selected platform.
5. Click **OK** to create the product.
![](https://main.qcloudimg.com/raw/463013c99e476af32767de8b2d48ff49.png)

### Creating an application
After you create a product, if you have not yet added a default application, you can follow these instructions to create an application. Only one application can be created per platform. After applications have been created for all three platforms, no new applications can be created.

#### Android applications
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns), and click **Product Management** in the left sidebar.
2. On the **Product List** page, select the product you have created, and click **More** > **Create an Application**.
3. On the **Create an Application** page, enter the application name, and put a check mark next to the platform **Android**.
4. Enter the application name, and click **OK** to create the application.
![](https://main.qcloudimg.com/raw/760969260ae6bda7b55a82adb5d2f76b.png)

#### iOS applications
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns), and click **Product Management** in the left sidebar.
2. On the **Product List** page, select the product you have created, and click **More** > **Create an Application**.
3. On the **Create an Application** page, enter the application name, and put a check mark next to the platform **iOS**.
4. Enter the application name, and click **OK** to create the application.
![](https://main.qcloudimg.com/raw/6d3601fe62081955cb575aec267289b6.png)

#### macOS applications
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns), and click **Product Management** in the left sidebar.
2. On the **Product List** page, select the product you have created, and click **More** > **Create an Application**.
3. On the **Create an Application** page, enter the application name, and put a check mark next to the platform **macOS**.
4. Enter the application name, and click **OK** to create the application.
![](https://main.qcloudimg.com/raw/035516a4f5179f315090e2afd41e08d1.png)


### Applying for beta
After you create an application, you can click **Apply for Beta/Testing** on the services management page. Perform the following steps to apply for beta:
1. Click **Initial Product Experience**.
2. Add information including the enterprise name, contact phone number, and email address.
3. Click **Confirm** to complete the application for beta.
4. Wait for approval, after which you can start using the beta push service.

>
- Try to ensure the accuracy of the information provided to ensure that the application is approved.
- A maximum of 100 devices can participate in testing for beta applications. If this limit is exceeded, the beta may be terminated. To avoid loss, do not use beta applications for commercial purposes.



### Configuring applications
After the application has been created, you can perform the following steps to configure it.


#### Android configuration
1. Go to the **Product List** page, select Android platform applications, and click **Configuration Management**.
2. Enter the name of the Android platform application, and click **Save** to complete basic configuration.
3. Vendor channel configurations can be enabled according to your requirements.


#### iOS configuration
1. Go to the **Product List** page, select iOS platform applications, and click **Configuration Management**.
2. Enter the BundleID for the iOS platform, and click **Save** to complete basic configuration.
3. Go to the configuration management page. In the **Push Certificate** box, enter the certificate password.
4. Click **Upload Certificate** to upload your iOS push certificate to the management platform, and complete iOS application configuration.
![](https://main.qcloudimg.com/raw/c93ef2fa5c51e6a98ee1fba98fd27eb9.png)

#### macOS configuration
1. Go to the **Product List** page, select macOS platform applications, and click **Configuration Management**.
2. Enter the BundleID for the macOS platform, and click **Save** to complete basic configuration.
3. Go to the configuration management page. In the **Push Certificate** box, enter the certificate password.
4. Click **Upload Certificate** to upload your macOS push certificate to the management platform, and complete macOS application configuration.
![](https://main.qcloudimg.com/raw/0237161819b29ef2b38f02aa3b270106.png)


