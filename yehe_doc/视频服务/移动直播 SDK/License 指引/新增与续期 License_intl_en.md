## Trial License

### Applying for trial license

You can apply for a trial license to try out MLVB International. The license is valid for 14 days and can be renewed once (for another 14 days).

>! If you renew a trial license within the first 14 days, the license will expire 28 days after the time of license application; if you renew a trial license that has expired once, the renewed license will expire 14 days after renewal.
> - For example, if you apply for a trial license at 10:28:41 on August 12, 2021, it will expire 14 days later at 10:28:41 on August 26, 2021.
>- You can renew the trial license once for free. If you renew it within the first 14 days, it will expire at 10:28:41 on September 9, 2021; if you renew it after the first 14 days, for example, at 22:26:20 on August 30, 2021, it will expire at 22:26:20 on September 13, 2021.

Follow the steps below to apply for a trial license:

1. Log in to the CSS console, go to **MLVB SDK** > **[License Management](https://console.intl.cloud.tencent.com/live/license)**, and click **Get License**.

   ![](https://qcloudimg.tencent-cloud.cn/raw/49e40218bbe80536940e5fb313450860.png)

2. Enter an application name, package name, and bundle ID and click **Confirm**.

   ![](https://qcloudimg.tencent-cloud.cn/raw/680f5ac056286d90e10b03e931252d59.png)

3. After the free trial license is successfully created, the page will display the information of the license. You need to pass in `Key` and `LicenseUrl` during the initialization of the SDK. Please store the information properly.

   ![](https://qcloudimg.tencent-cloud.cn/raw/e22b61bc11e73c7ea57bdc58df527046.png)

>?
>- You can modify the bundle ID and package name bound with a trial license by clicking **Edit**. After modification, click **Confirm**.
>- You can enter `-` if you don’t have a package name or bundle ID to bind yet.

### Renewing trial license

A newly applied trial license is valid for 14 days, after which you can renew it **once** for another 14 days by clicking **Edit** and then **Confirm**.

![](https://qcloudimg.tencent-cloud.cn/raw/a693874fc6d0d658170913beaef8bd2f.png)

As shown below, the validity period has been extended.

![](https://qcloudimg.tencent-cloud.cn/raw/cd5f234437e6facf4157401a0d98af98.png)

>? You can renew a trial license **only once**, which means a trial license is valid for up to 28 days. To continue using the MLVB SDK after 28 days, you need to [purchase an official license](https://intl.cloud.tencent.com/document/product/1071/38546#.E6.AD.A3.E5.BC.8F.E7.89.88-license).

## Official License

### Purchasing official license

1. [Purchase an official license](https://buy.intl.cloud.tencent.com/mlvb) for one-year access to the MLVB International SDK. An official license expires at 00:00:00 the next day after the purchase date a year later. For pricing details, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1071/38114).

>? For example, assume that you purchased an official license at 14:16:52 on December 1, 2021. The license would expire at 00:00:00 on December 2, 2022.

2. Go to **MLVB SDK** > **[License Management](https://console.intl.cloud.tencent.com/live/license)**, click **Create**, enter an application name, package name, and bundle ID, and click **Confirm**.

   ![](https://qcloudimg.tencent-cloud.cn/raw/276281c94f5c6e53af157d480608bd12.png)

   >? 
   >- Before clicking **Confirm**, double-check the bundle ID and package name. You can modify the information if it is inconsistent with what you submit to app stores. **License information cannot be modified after submission.**
   >- **You cannot modify the information of an official license.** However, you can, after purchasing a new license, click **Create** to create a new license (instead of using it to renew your existing license) and bind it to a new bundle ID/package name.

3. After an official license is successfully created, the page will display the information of the license. You need to pass in `Key` and `LicenseUrl` during the initialization of the SDK. Please store the information properly.

   ![](https://qcloudimg.tencent-cloud.cn/raw/7969480ebb9126eb0fbc5cb8f7ff4bc8.png)

### Renewing official license

You can go to **MLVB SDK** > **[License Management](https://console.intl.cloud.tencent.com/live/license)** to view the validity period of your license. If your license has expired, you can follow the steps below to renew it:

1. Find the target license and click **Renew**.

   ![](https://qcloudimg.tencent-cloud.cn/raw/bbaf91140cf38c5dd3cafdbd8313b5b1.png)

2. Verify the renewal information, including the application name and new validity period, and click **Renew** to go to the payment page.

   ![](https://qcloudimg.tencent-cloud.cn/raw/cf7d6888853a6b234f989a40f4b77df9.png)

3. Check the new validity period.

   >! **You cannot modify the information of an official license.** However, you can, after purchasing a new license, click **Create** to create a new license (instead of using it to renew your existing license) and bind it to a new bundle ID/package name.

