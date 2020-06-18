
## Operation Scenarios
This document guides you in how to create products and applications and configure applications in the TPNS Console.

## Prerequisites
You have a Tencent Cloud account. For more information, please see [Signing Up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions
### Creating Product
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and click **Product Management** on the left sidebar.
2. Go to the product management page and click **Add Product**.
3. On the product adding page, enter the product name and product details and select a product type.
4. If you check Android, iOS, or macOS below, the system will create an application on the selected platform by default.
5. Click **OK** to create the product.
![](https://main.qcloudimg.com/raw/463013c99e476af32767de8b2d48ff49.png)

### Creating application
After you create a product, if you haven't added the default application, you can follow the steps below to create an application. Only one application can be created per platform. After applications have been created for all three platforms, no new applications can be created.

#### Android application
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Product Management** on the left sidebar.
2. On the product list page, select the product you have created and click **Add Application** and select the **Android** platform.
3. Enter the application name and click **OK** to create the application.
![](https://main.qcloudimg.com/raw/760969260ae6bda7b55a82adb5d2f76b.png)

#### iOS application
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Product Management** on the left sidebar.
2. On the product list page, select the product you have created and click **Add Application** and select the **iOS** platform.
3. Enter the application name and click **OK** to create the application.
![](https://main.qcloudimg.com/raw/6d3601fe62081955cb575aec267289b6.png)

#### macOS application
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Product Management** on the left sidebar.
2. On the product list page, select the product you have created and click **Add Application** and select the **macOS** platform.
3. Enter the application name and click **OK** to create the application.
![](https://main.qcloudimg.com/raw/035516a4f5179f315090e2afd41e08d1.png)


### Applying for trial
After creating the application, you can click **Apply for Trial/Test** on the service management page to complete the trial application in the following steps:
1. Click **Initial Product Experience**.
2. Enter your company name, contact number, email, and other information.
3. Click **OK** to complete the application for trial.
4. After your application is approved, you can start trying the push service.

>
>- Please ensure the accuracy of the entered information; otherwise, your application may be rejected.
>- A trial application supports up to 1,000 devices in a test. If the limit is exceeded, the trial may be terminated. Therefore, do not use it for commercial purpose to avoid potential losses.



### Configuring application
After you create an application, you can follow the steps below to configure it.


#### Android configuration
1. Go to the product list page, select the Android application, and click **Configuration Management**.
2. Enter the application package name for the Android platform and click **Save** to complete basic configuration.
3. You can choose to enable the vendor channel configuration as needed.


#### iOS configuration
1. Go to the product list page, select the iOS application, and click **Configuration Management**.
2. Enter the `BundleID` for the iOS platform and click **Save** to complete basic configuration.
3. Go to the configuration management page and enter the certificate password in the **Push Certificate** field.
4. Click **Upload Certificate** to upload your iOS push certificate to the management platform and complete iOS application configuration.
![](https://main.qcloudimg.com/raw/c93ef2fa5c51e6a98ee1fba98fd27eb9.png)

#### macOS configuration
1. Go to the product list page, select the macOS application, and click **Configuration Management**.
2. Enter the `BundleID` for the macOS platform and click **Save** to complete basic configuration.
3. Go to the configuration management page and enter the certificate password in the **Push Certificate** field.
4. Click **Upload Certificate** to upload your macOS push certificate to the management platform and complete macOS application configuration.
![](https://main.qcloudimg.com/raw/0237161819b29ef2b38f02aa3b270106.png)


