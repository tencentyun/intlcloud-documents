## Overview

This document describes how to receive alarm notifications via WeCom.

## Use Limits

Regarding sending WeCom group messages, the number of messages sent by each bot cannot exceed 20 per minute. If you have many alarm policies, we recommend that you create multiple bots and associate alarm policies with different bots. Otherwise, multiple alarm policies may trigger alarms simultaneously, and you may fail to receive some alarm notifications as a result.

>? After you successfully create WeCom bots and configure the callback address, CLS will automatically push the alarm messages to the WeCom bots. This way, you can receive alarm notifications through a WeCom group.
>


## Directions

### Adding bot in WeCom

#### WeCom for PC

1. On WeCom for PC, find the target WeCom group for receiving alarm notifications.
2. Right-click the WeCom group.
3. In the pop-up window, click **Add Group Bot**.
4. In the pop-up window, click **Create a Bot**.
5. In the pop-up window, enter a custom bot name and click **Add**.
6. Click **Copy Address** to copy the webhook address and [configure alarm webhook](#return).


#### WeCom for Web

1. On WebCom for Web, open the target WeCom group for receiving alarm notifications.
2. Click the group settings icon in the upper-right corner.
3. On the group settings page, choose **Group Bots** -> **Add a Bot**.
4. On the management page for adding bots, enter a custom name for the new bot.
5. Click **Add**. Copy the webhook address and [configure alarm webhook](#return).
>? If you want to configure a WeCom group bot, please see [WeCom > Configuring Group Bot](https://work.weixin.qq.com/help?doc_id=13376).
>

<span id="return"></span>
### Configuring alarm webhook

In the CLS notification channel, enter the webhook address and click **OK**.


After the configuration is completed successfully, when an alarm policy is triggered, you will receive alarm notifications sent by group bots through the WeCom group.

