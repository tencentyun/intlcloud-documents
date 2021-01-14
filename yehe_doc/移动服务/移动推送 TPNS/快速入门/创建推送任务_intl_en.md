## Overview
This document describes how to create a push task in the TPNS Console.

## Prerequisites
You have purchased the TPNS service. For more information, please see [Purchase Directions](https://intl.cloud.tencent.com/document/product/1024/37863).

## Directions
### SDK download
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and click **Toolbox** > **[SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload)** on the left sidebar.
2. Enter the SDK download page, select the version you want to download, click **Download**, and configure as instructed.

### Push parameter settings
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Push Management** > **Task List** on the left sidebar.
2. Enter the task list page, select **Create Push**, click **Notification Message**, and enter the notification title and content on the page. The preview of the notification will be displayed on the right. Other push settings are as follows:
 -  Push Plan: if there are many push tasks, we recommend you categorize them and collect their statistics by push target.
 -  Push Time: you can select the instant, scheduled, or loop mode.
 -  Push Target: you can choose to push by all devices, tag combination, batch accounts, account, or token.
 -  Advanced Settings: TPNS also supports other advanced settings, including:
    -  Collapse by Group: you can control whether and how to collapse notifications in the device notification center.
	  - Badge Number: this refers to the number of messages that have arrived but not been clicked. Only TPNS, Huawei, and Mi channels support the feature of auto increase by 1.
	  -  Extra Parameter(s): you can select additional parameters in the format of `key-value` to enrich the push content.
    -  Notification Image: after the image URL is entered, notifications delivered through certain channels will display the image.
	  -  Notification Audio: after the audio URL is entered, notifications delivered through the TPNS channel can contain audio.
    -  Offline Storage: set the offline retention time between 0 and 72 hours. The default value is 24 hours. Up to 3 latest pushes can be retained.
    -  Open Location: set the click action for the push, including application, custom intent, URL, and in-app activity.
    -  Reminder: set the reminder method, custom ringtone, etc.
    -  Multi-Package Name Push: TPNS supports push with multiple package names.
    -  Channel Policy: select channels through which the push can be delivered. Smart assignment policy and custom policy are supported.
![](https://main.qcloudimg.com/raw/f08fe25ffa6f98dbfc8284210e51771c.png)
3. After selecting the push content, you can select a test device to verify the push effect before officially sending the push.
	1. Click **Test Preview**.
	![](https://main.qcloudimg.com/raw/52f3e001387d609b02ca516ade9de4b8.png)
	2. Select a test device on the test preview page.
	![](https://main.qcloudimg.com/raw/487d9a262a16b53a6ecfe4b3a9c7fd03.png)
	3. Click **OK** to push to the test device. The push status of the test device will be returned on the current page.
	![](https://main.qcloudimg.com/raw/ee089f432f0a2c176eec4f529746d2d2.png)
4. Click **Confirm**. If the test device successfully completes the push, click **Confirm Push** > **Confirm** to push officially. The official push status will be returned on the current page.
![](https://main.qcloudimg.com/raw/8f4167558b7f12c8ee3643013e8828aa.png)
![](https://main.qcloudimg.com/raw/12fbc836860e4e5356ff3856a26aa84c.png)
The push status is as shown below:
![](https://main.qcloudimg.com/raw/6303c38e09baca92358f8ff12c9a416d.png)
5. Click **Confirm** to directly redirect to the push record page, where the push records of the test push and official push are displayed respectively as shown below:
![](https://main.qcloudimg.com/raw/6fa760f9d074b8cfda960b0fcf3a64d2.png)

