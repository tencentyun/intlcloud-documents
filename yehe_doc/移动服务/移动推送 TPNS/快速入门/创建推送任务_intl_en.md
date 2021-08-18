## Overview
This document describes how to create a push task in the TPNS console.

## Prerequisites
You have purchased the TPNS service. For more information, please see [Purchase Directions](https://intl.cloud.tencent.com/document/product/1024/37863).

## Directions
### Downloading SDK
1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. On the left sidebar, click **Message Management** > **[SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload)**.
3. On the **Download SDK** page, select the version you need to download, click **Download**, and configure according to the instructions.

### Configuring push parameters
1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. On the left sidebar, click **Message Management** > **Task List**.
3. On the **Task List** page, click **Create Push**.
4. On the **Create Push** page, select **Notification bar message** for **Push Type** and enter the notification title and content. The preview of the notification will be displayed on the right. Other push settings are as follows:
 - **Push Plan**: if there are many push tasks, you are advised to categorize them and collect their statistics by push target.
 - **Push Time**: you can select **Immediate**, **Scheduled**, or **Loop**.
 - **Push Target**: you can select **All devices**, **Tag combination**, **Batch accounts**, **Account**, or **Token**.
 - **Advanced Settings**: TPNS also supports the following advanced settings:

    - **Grouping and Collapsing**: you can control whether and how to collapse notifications in the device notification center.
    - **Badge Number**: this refers to the number of messages that have arrived but not been clicked. Only the TPNS, Huawei, and Mi channels support automatically increasing the number by 1.
    - **Extra Parameter(s)**: you can select extra parameters in the data format of key:value for more diverse push content.
    - **Notification Image**: after you enter the image URL, notifications delivered through certain channels will display the image.
    - **Notification Audio**: after you enter the audio URL, notifications delivered through the TPNS channel will contain the audio.
    - **Offline Storage**: set the offline retention time between 0 and 72 hours. The default value is 24 hours. Up to three latest pushes can be retained.
    - **Open Location**: set the click action for the push, supporting application, custom intent, URL, and in-app activity.
    - **Reminder**: set the reminder method, custom ringtone, etc.
    - **Multi-Package Name Push**: TPNS supports push with multiple package names.
    - **Channel Policy**: select channels through which the push can be delivered. Smart assignment policy and custom policy are supported.
5. After selecting the push content, you can select a test device to verify the push effect before officially sending the push.
	i. Click **Test Preview**.

	ii. Select a test device on the test preview page.

	iii. Click **Confirm** to push to the test device. The push status will be returned on the current page.

6. Click **Confirm**.

7. Click **Confirm** to push officially. The push status will be returned on the current page.

The push status is shown in the figure below:

8. Click **Confirm** to go to the push record page, where the push records of both the test push and official push are displayed.


