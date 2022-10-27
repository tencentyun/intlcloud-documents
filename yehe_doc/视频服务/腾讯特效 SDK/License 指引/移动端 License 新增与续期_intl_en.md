Tencent Effect offers various beauty filters and effects. To use the Tencent Effect SDK, you can purchase a Tencent Effect package or capability for a one-year license. For the billing details, see [Pricing Overview](https://www.tencentcloud.com/document/product/1143/45371).

After obtaining a license, you can bind it to a new application or use it to extend the validity of Tencent Effect for an existing application in the [Tencent Effect console](https://console.tencentcloud.com/xmagic).
This document shows you how to add a trial or official license, as well as how to renew an existing license.

[](id:test)
## Trial License

### Applying for a trial license[](id:create_test)

You can apply for a trial license to try out the Tencent Effect SDK. A trial license is valid for 14 days and can be renewed once (28 days in total).
The Tencent Effect package offered for trial is the full-featured [package S1 - 04](https://www.tencentcloud.com/document/product/1143/45376). You can also choose specific features of the Tencent Effect SDK to try. Note that package S1 - 04 includes X1-01 keying, but does not offer other keying features.

>! **You need to pass our review before you are issued a Tencent Effect license**. A trial license becomes valid the moment you pass the review. If you renew the trial license after the first 14 days, the new expiration time of the license will be 14 days from the time of renewal.
>- After you submit your company information, the status of the Tencent Effect module will change to **Review in progress**. The review process usually takes 1-2 days. Suppose you submitted your company information on `2022-05-24 12:47:33` and passed the review on `2022-05-24 15:23:46`. The trial license would expire 14 days later on `2022-06-09 00:00:00` .
>- You can renew the trial license once for free. If you renew it within the first 14 days, it will expire on `2022-06-23 00:00:00` ; if you renew it after the first 14 days, for example, on `2022-08-06 22:26:20` , it will expire on `2022-08-22 00:00:00`.

In the console, you can either **create a trial license for a new application** or **activate Tencent Effect for trial for an existing application**.
<dx-tabs>
::: Create a new trial license

1. Log in to the [Tencent Effect console](https://console.tencentcloud.com/xmagic) and select **Mobile Licenses** on the left sidebar. Click **Create trial license**.
![](https://qcloudimg.tencent-cloud.cn/raw/54ac63cd985f1170b2d74eaac4d0cd1d.png)
2. Enter the app name, package name, and bundle ID. Select the capabilities to try (**Advanced S1 - 04**, **Capability X1-01**, and **Capability X1-02**). **Enter your company name, select the industry, and upload your company’s business license**. Click **Create**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e3d3bb59025c79ac4d46f45c67d1cc27.png" style="zoom:50%;" />
3. After the trial license is successfully created, you will see the license URL and key, **which you need to pass in when initializing the SDK, so save a copy of the information**. Note that the license information becomes valid only after you pass the review.
![](https://qcloudimg.tencent-cloud.cn/raw/6b8d5e0cca6b37e136040a50a17d5099.png)
> ?
>- To modify the bundle ID and package name bound to a trial license, click **Edit** on the right and, after modification, click **Confirm**. Note that you will need to **go through the review process again** before you can continue to use the Tencent Effect module.
> <img src="https://qcloudimg.tencent-cloud.cn/raw/b2a4f9588cc7f0ba5131e631ace94d10.png" style="zoom:50%;" />
>- You can enter `-` if you don’t have a package name or bundle ID to bind yet.

:::
::: Activate Tencent Effect for trial for an existing application
Follow the steps below to activate Tencent Effect for trial for an existing application:
1. Select an existing trial license and click **Try more capabilities**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/31d21e8d61ed556276a44706a244d804.png" style="zoom: 50%;" />
2. Select the capabilities to try (**Advanced S1 - 04**, **Capability X1-01**, and **Capability X1-02**). **Enter your company name, select the industry, and upload your company’s business license**. Click **Create**. 
<img src="https://qcloudimg.tencent-cloud.cn/raw/99f950a4bb1396e31d69f2c28cdab64f.png" style="zoom:50%;" />
:::
</dx-tabs>

3. After you submit the information, the status of the Tencent Effect module will change to **Review in progress**. You can click **Review details** to view the information you submitted.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a349ab1958dc407c362fad72485dab5d.png" style="zoom:67%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/34446b73133115d11e18b54393361b98.png" style="zoom:67%;" />
4. After you pass the review, the status of the module will change to **Normal**, which indicates that the trial license has been issued. You can start exploring Tencent Effect.
![](https://qcloudimg.tencent-cloud.cn/raw/516e3b714bd158a452022c4c563e0756.png)
>? If you **fail to pass the review**, you can click **Review result** to view the details, including the reason for rejection. To resubmit information for review, click **Try again**.
![](https://qcloudimg.tencent-cloud.cn/raw/d787f5e69875a0de1294a8dd0ab519f3.png)

[](id:renewal_test)
### Renewing a trial license
A trial license is valid for 14 days by default. You can renew it **once** to extend the validity by another 14 days: Just click **Renew** in the **Tencent Effect** module and then click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/688ba0f794f4ec63857583a436d78e7a.png)

>? A trial license for Tencent Effect **can be renewed only once**, which means you can use a trial license for 28 days at most. To continue using Tencent Effect after your trial license expires, please purchase an [official license](#create_formal).

[](id:upgrade_test)
### Upgrading to an official license
To upgrade to an official license, please [purchase a Tencent Effect package](https://buy.cloud.tencent.com/vcube?type=magic) first and perform the following steps:
1. Click **Upgrade** in the Tencent Effect module.
![](https://qcloudimg.tencent-cloud.cn/raw/d1915913278cbf6f3c188141cdcdea5f.png)
2. Click **Bind**, select a Tencent Effect package you purchased, and click **Confirm**. An official license will be activated for the application. You don’t need to go through the review process again. If you don’t have any packages to bind, go to the [Purchase Page](https://buy.cloud.tencent.com/vcube?type=magic) to buy a package.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9466fa0917c9220d849603ab6a29b190.png" style="zoom:50%;" />

[](id:formal)
## Official License
[](id:create_formal)

### Purchasing an official license
You can purchase a [Tencent Effect capability](https://buy.intl.cloud.tencent.com/vcube) to get a license to use the Tencent Effect SDK. A license is valid for a year and expires at 00:00:00 the next day. To learn about the features of different SDK editions, see [Pricing Overview](https://www.tencentcloud.com/document/product/1143/45376).

After purchasing a package, follow the steps below:
1. Bind the license. You can either **bind the license to a new application** or **use it to activate Tencent Effect for an existing application**. 
<dx-tabs>
::: Bind an official license to a new application
1. Log in to the [Tencent Effect console](https://console.cloud.tencent.com/vcube) and select **Mobile Licenses** on the left sidebar. Click **Create official license**.  
![](https://qcloudimg.tencent-cloud.cn/raw/1840aafe0ac1fc54485f9d4a4b15b98a.png) 
2. Enter the app name, package name, and bundle ID, select **Tencent Effect**, and click **Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f128fdb87a0cc07762bbb75e86b460e9.png" style="zoom:50%;" />
3. Click **Bind**, select a Tencent Effect package you have purchased, and click **Confirm**. If there are no packages to bind, go to the [Purchase Page](https://buy.cloud.tencent.com/vcube?type=magic) to buy a package. 
<img src="https://qcloudimg.tencent-cloud.cn/raw/db5cf0bb61ea8063d25a11dfafb89e90.png" style="zoom:50%;" />
>? Before clicking **Confirm**, double-check the bundle ID and package name and make sure they are identical to what you submit to app stores. **The information cannot be modified after submission.** 

:::
::: Activate Tencent Effect for an existing application
1. Select an existing official license to which you want to add the **Tencent Effect** capability and click **Activate more capabilities**.
![](https://qcloudimg.tencent-cloud.cn/raw/7d00d56c1dd4c1658f4fde736276d322.png)
2. Select **Tencent Effect** and click **Next**.  
![](<img src="https://qcloudimg.tencent-cloud.cn/raw/d88b7f921e294eafec2bbdbaab65edec.png" style="zoom: 25%;" />
3. Click **Bind**, select a Tencent Effect package you have purchased, and click **Confirm**. If there are no packages to bind, go to the [Purchase Page](https://buy.intl.cloud.tencent.com/vcube) to buy a package.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0df1ab29aec13532934eed6457b8936d.png" style="zoom:55%;" />)
:::
</dx-tabs>
2. If the status of the Tencent Effect module is **Normal**, it indicates that the license has been issued. You can start exploring Tencent Effect.
![](https://qcloudimg.tencent-cloud.cn/raw/75200f8c745038400c568ca5e4d241af.png)


[](id:upgrade_formal)
### Extending the validity of Tencent Effect
You can go to the [Mobile Licenses](https://console.tencentcloud.com/xmagic) page of the Tencent Effect console to view the validity of a license. To extend the validity of Tencent Effect for an application, follow the steps below:
1. Select the license you want to renew and click **Renew** in the Tencent Effect module.
![](https://qcloudimg.tencent-cloud.cn/raw/a4b37fc395ce6ea395541825167ad284.png)
2. Select a package that is of **the same type** as the current one. The page will display the start and end time of the renewed period. Click **Confirm**. If you don’t have a package to bind, go to the [Purchase Page](https://buy.intl.cloud.tencent.com/vcube) to buy one.
<img src="https://qcloudimg.tencent-cloud.cn/raw/decbe36048335926e3a964a6ae923fbe.png" style="zoom:50%;" />
>! Currently, you can only use the same type of package to renew a Tencent Effect license. For example, if your current license is package S1 - 04, you need to buy another S1 - 04 package to renew it. If you want to use a different type of package, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) or contact sales.
3. Check the new validity period.
>! **You cannot modify the information of an official license.** If you want to use a package you purchased for a new application, click **Create official license** to bind it to a new application.