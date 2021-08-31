This document describes how to receive alarm notifications through a WeCom group.

## Use Limits

Regarding sending WeCom group messages, the number of messages sent by each bot cannot exceed 20 per minute. If you have many alarm policies, we recommend that you create multiple bots and associate alarm policies with different bots. Otherwise, multiple alarm policies may trigger alarms simultaneously, and you may fail to receive some alarm notifications as a result.



>? After you successfully create WeCom bots and configure the callback address, Cloud Monitor will automatically push the alarm messages to the WeCom bots. This way, you can receive alarm notifications through a WeCom group.

## Step 1: Add a Bot on WeCom

#### WeCom for PC

1. On WeCom for PC, find the target WeCom group for receiving alarm notifications.
2. Right-click the WeCom group. In the window that appears, click **Add Group Bot**.
3. In the window that appears, click **Create a Bot**.
4. In the window that appears, enter a custom bot name and click **Add**.
5. Copy the webhook address and configure the API callback by following [Step 2](#step2).
![](https://main.qcloudimg.com/raw/d44f83956609d5d6700721e787770c3a.png)

#### WeCom for Web

1. On WebCom for Web, open the target WeCom group for receiving alarm notifications.
2. Click the group settings icon in the upper-right corner.
3. On the group settings page, choose **Group Bots** > **Add a Bot**.
4. On the management page for adding bots, enter a custom name for the new bot.
5. Click **Add**, copy the webhook address, and configure the API callback by following [Step 2](#step2).

<span id="step2"></span>

## Step 2: Configure the Alarm API Callback

Go to [Cloud Monitor Console - Create Alarm Policy](https://console.cloud.tencent.com/monitor/policylist/create), enter the webhook address, and click **Complete**. 
![](https://main.qcloudimg.com/raw/6c5dcf93ba7498f44faa33dbbcaa82ad.png)

After the configuration is completed successfully, when an alarm policy is triggered or the alarm is resolved, you will receive alarm notifications sent by group bots through the WeCom group, as shown in the following figure:

![](https://main.qcloudimg.com/raw/e3cc8e94135f26dbc3bc695664fa8763.png)

