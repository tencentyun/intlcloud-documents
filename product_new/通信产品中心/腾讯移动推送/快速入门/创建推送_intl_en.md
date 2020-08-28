## Operation Scenario
This document guides you how to create a push notification in the TPNS console.
## Prerequisites
You have already purchased TPNS service. 


## Steps

### Downloading SDK
1. Log in to [TPNS Console](https://console.cloud.tencent.com/tpns), and click **Download SDK** in the left sidebar.
2. Enter the **Download SDK** page, select the version you need to download, and click **Download**. Perform configurations according to the guidelines.

### Configuring push parameters
1. Go to the **Application List** page. Select the paid app, and click **Create Push**.
2. Go to the mobile push page, and click **Push Notifications**. Enter the notification title and notification content. The notification preview will be displayed on the right side of the page.
	◦Push time configuration: Supports instant, scheduled, and loop modes.
	◦Push target configuration: Supports push to all users and to specific users. Specific users include: Individual token, individual account, custom tag, and device attributes.
	◦Additional parameters: You can select additional parameters in the data format of key:value, for more push content.
	◦Rich media content: You can add rich media content, by entering the URL corresponding to an image.
	◦Advanced settings: TPNS also supports other advanced settings, including the following content:
	  - Badge number: number of messages reached but not clicked.
      - GroupID:  a field for aggregated statistics of multiple push tasks.
	  - Offline retention: sets the offline storage period in 0-72 hours. Up to 3 latest push messages can be saved offline.
	  - Click open: Sets push click open actions. Actions include apps, in-app pages, URLs, and client customization.
	  - Reminder formats: Sets reminder formats, custom ringtones, etc.
	  - Multiple package name push: Supports push with multiple package names.
	![](https://main.qcloudimg.com/raw/ccf9efd21508458cb77332449bde6b6a.png)
3. After selecting push content, click **Confirm Push**. After completing the push, you will be automatically redirected to the push record page.

