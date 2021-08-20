### 1. How to obtain the package name for an Android project?
You can obtain the package name in the `Mainfest.xml` file of your Android project.
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
	package="com.huawei.player"
	android:versionCode="20181111"
	android:versionName="1.0">
```

### 2. How to obtain the bundle ID for an iOS project?
You can obtain the bundle ID in `General > Identity` in Xcode, as shown below:
![](https://main.qcloudimg.com/raw/56571d560da04bf6563ccae91d32b75a.png)

### 3. Can I renew a trial license after it expires?
You can use a trial license for 28 days at most. When it first expires after 14 days, you can renew it for another 14 days. After 28 days, please [purchase an official license](https://intl.cloud.tencent.com/document/product/1071/38546).

### 4. Can I change the package name for an Android project or the bundle ID for an iOS project if I use a trial license?
Yes, you can.
In the **CSS console**, go to [**MLVB SDK** > **License Management**](https://console.cloud.tencent.com/live/license) and click **Edit** to change the bundle ID and package name.

### 5. Can I change the package name for an Android project or the bundle ID for an iOS project if I use an official license?
No, you can’t.

### 6. Can I use 1 license for multiple applications at the same time?
Each license can be bound to only 1 package name and bundle ID. If you want to use MLVB features in multiple applications, you need to purchase multiple licenses.

  
