## Overview

WooCommerce is a popular tool for building independent e-commerce websites. It is open source, free of charge and easy to use. With powerful features, it allows you to quickly build an independent WordPress-based e-commerce website. This image comes pre-installed with WordPress (including WooCommerce plugin), Nginx, MariaDB, PHP software.


## Directions

### Creating a Lighthouse Instance Using WooCommerce Application Image
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse). On the **Instances** page, click **Create**.
2. On the Lighthouse purchase page, purchase a Lighthouse instance with needed configurations selected.
For image configuration, select **Application image** > **WooCommerce 6.5.1**. Configure other parameters as instructed in [Purchase Methods](https://intl.cloud.tencent.com/document/product/1103/41404).
<dx-alert infotype="explain" title="">
- To set up live streaming service using a created instance, you can use the WooCommerce application image to [reinstall system](https://intl.cloud.tencent.com/document/product/1103/41560).
- In this example, we uses the application image WooCommerce 6.5.1. Note that the image may undergo version upgrades and updates. The actual version on the purchase page shall prevail.
</dx-alert>


### Logging in to the Website Admin Page[](id:login)
1. On the instance details page, select **Pre-installed application** tab, and enter the application details page.
2. [](id:Step2)In the **Pre-installed software** section, click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin:-3px 0px;"> to copy the command for getting WordPress admin account and password.
![](https://qcloudimg.tencent-cloud.cn/raw/5b495d8acac0b4e66e002f697f1e0adb.png)
3. In the **Pre-installed software** section, click **Log in** beside the command or at the upper right corner.
4. [](id:Step4)In the pop-up login window, paste the command obtained in [Step 2](#Step2) and press **Enter**.
Then, you can obtain admin account (admin) and password (wordpress_password).
![](https://qcloudimg.tencent-cloud.cn/raw/24a91d82cb71b14dff4db24ed0be8aa0.png)
5. Record admin account and password, close the login window, and go back to the application details page.
6. In the **Pre-installed software** section, click **Admin address**.
![](https://qcloudimg.tencent-cloud.cn/raw/9199d3cb7c38c5ec51670cb95988238e.png)
7. In the opened browser window, enter the account and password recorded in [Step 4](#Step4), and click **Log in**.
8. Select **WooCommerce** > **Home** in the left sidebar. After entering the page as shown below, you can start configuring your own independent e-commerce website.
![](https://qcloudimg.tencent-cloud.cn/raw/c3f958d021128402006e770d6c646252.png)
To get started with WooCommerce, see [WooCommerce](https://woocommerce.com/documentation/plugins/woocommerce/getting-started/).


## Related Operations

### Switching WordPress Admin Page Language

1. Log in to the admin page as instructed in [Logging in to the Website Admin Page](#login) Step 1 - Step 7.
2. Select **Settings** in the left sidebar to enter the "General options" page.
3. Find **Site language** and select the target language. 
4. Scroll to the bottom of the page and click **Save changes**.


### Using WordPress Theme
The free Kadence and Astra themes are installed by default, and other WordPress themes are also available. This section introduces you how to switch, add and update WordPress themes.

1. Log in to the admin page as instructed in [Logging in to the Website Admin Page](#login) Step 1 - Step 7.
2. Select **Appearance** > **Theme** in the left sidebar.
3. On the **Theme** page, you can do the following:
<dx-tabs>
::: Add a theme
On the page of adding a theme, click **Upload theme** to install a new theme.
:::
::: Switch a theme
On the **Theme** page, select the target theme, and click **Enable** to switch the theme.
:::
</dx-tabs>

This document takes the Kadence theme installed by default as an example to introduce how to use the independent website template in the Kadence theme to make the online store more beautiful. The operation steps are as follows:
1. Log in to the admin page as instructed in [Logging in to the Website Admin Page](#login) Step 1 - Step 7.
2. Select **Appearance** > **Theme** in the left sidebar, go to the **Theme** page, and click the Kadence theme.
3. On the details page of the Kadence theme, click **Kadence**.
4. Select the **Starter Templates** tab and click **Install Kadence Starter Templates**.
![](https://qcloudimg.tencent-cloud.cn/raw/3a581c9dadc012923f5ec32fc5a242af.png)
5. Select a template on the page. In this example, the **Outdoor Shop** template is selected. Click on the template.
![](https://qcloudimg.tencent-cloud.cn/raw/ba902b5d415ecbeda9a52a5758187860.png)
6. After editing the template as needed, select **Single Page** or **Full Site** in the **IMPORT OPTIONS** in the lower left corner of the page. In this example, **Full Site** is selected.
7. Check the **Must-knows** in the **Import Starter Template** pop-up window, and import.
<dx-alert infotype="notice" title="">
This method will overwrite your site customizer settings, widgets, and menus. If you are testing different starter templates, it is recommended that you enable "Delete Previously Imported Posts and Images".
</dx-alert>
8. The following page indicates that you have successfully applied the template to your online store. You can click **Finished! View your site** to go to the store homepage.
![](https://qcloudimg.tencent-cloud.cn/raw/7d158c44d2860a27dbb6301b832653f7.png)


### Enabling HTTPS access
You can install an SSL certificate and enable HTTPS access for your WooCommerce instance as instructed in [Installing Certificate on NGINX Server](https://intl.cloud.tencent.com/document/product/1103/47406).
