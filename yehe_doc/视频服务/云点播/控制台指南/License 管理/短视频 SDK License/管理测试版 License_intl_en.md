A UGSV SDK license is used to activate the use rights of the UGSV SDK. You can apply for, renew, and view a trial license in the console. For more information on UGSV SDK features, please see [UGSV](https://intl.cloud.tencent.com/document/product/1069/37914).
## Trial License Application
You can apply for a trial license to try out various features available in the UGSV SDK Basic Edition for free. The license is valid for 14 days upon initial application and can be renewed for 14 days (with a validity period of up to 28 days). The steps are as follows:

### Step 1. Create a trial license
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/license) and select **License Management** > **[UGSV SDK License](https://console.cloud.tencent.com/vod/license/video)** on the left sidebar.

2. Click **Apply Now** to access the license configuration page and enter the `App Name`, `Package Name`, and `Bundle ID`.

3. Click **Create for Free**.

### Step 2. Save the trial license
After the free trial license is successfully created, the page will display the information of the generated license. You need to pass in two parameters `Key` and `LicenseUrl` during initial SDK configuration. Please save the information properly.
![](https://qcloudimg.tencent-cloud.cn/raw/1500204df3029e9bbb23aa7161ad94bd.png)

## Renewing a Trial License
You can check the validity period of the trial license in the [VOD console](https://console.cloud.tencent.com/vod/license), which is up to 28 days. Before the trial license expires in 14 days after application, you need to renew it by following the steps below:
### Step 1. Apply for license renewal
Go to the **[UGSV SDK License](https://console.cloud.tencent.com/vod/license/video)** page and click **Renew** in the top-right corner of the trial license section.

### Step 2. Complete license renewal
After the pop-up window prompts that the renewal is successful, the **Renew** button in the top-right corner will disappear, indicating that the trial license is renewed for 14 days.


## Viewing a Trial License
After the license is configured successfully, wait for a while (subject to the network conditions) and then you can view the license information by calling the following methods:

- iOS:
```
NSLog(@"%@", [TXUGCBase getLicenceInfo]);
```
- Android:
```
TXUGCBase.getInstance().getLicenceInfo(context);
```

## Using a License
Call the following methods to configure the license before calling the relevant APIs of the SDK:

- For iOS, we recommend you add the following in `[AppDelegate application:didFinishLaunchingWithOptions:]`:
```
[TXUGCBase setLicenceURL:LicenceUrl key:Key];
```
- For Android, we recommend you add the following in `application`:
```
TXUGCBase.getInstance().setLicence(context, LicenceUrl, Key);
```
