
This document describes how to view exception alarm messages from DBbrain in the TencentDB for MySQL console.

DBbrain's [exception alarms](https://intl.cloud.tencent.com/document/product/1035/37177) notification service pushes MySQL instance exception alarm messages to you in real time, allowing you to conveniently and promptly discover database exception diagnosis problems.
All pushed exception alarm messages are displayed in the historical message list, so you can quickly view and locate previously pushed exception diagnosis problems.

## Viewing an Exception Alarm
### Option 1
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). If an exception diagnosis problem occurs on an instance when you are in the console, a window will pop up in the top-right corner of the console in real time to push the exception alarm message notification, which contains the database instance information such as instance ID, instance name, diagnosis item, and start time. This allows you to quickly learn the diagnosis of the database instance.
- You can click **View Exception Diagnosis Details** in the message notification to view the specific diagnosis details and optimization advice for the instance.
- If you check **No alarm again today** in the message notification, when an exception diagnosis problem occurs in a database instance under your account, no exception alarm messages will be pushed to you in a pop-up window.

![](https://main.qcloudimg.com/raw/22f1e14880499e6d18ff38f019b74d2d.png)

### Option 2
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select **Instance List**, **Task List**, **Parameter Template**, **Recycle Bin** or **Placement Group** on the left sidebar, and click **Exception Alarm** in the top-right corner to expand the list of historical exception alarm messages. The number of alarms generated in the instances under your account is displayed next to the button.
![](https://main.qcloudimg.com/raw/18bda2b422ce5c221001f885bd8279a4.png)
In the expanded list of historical exception alarm messages, you can view all pushed exception alarm messages. You can view them by region and click a message to view the diagnosis details of the exception alarm event.
![](https://main.qcloudimg.com/raw/b2fcff416f3db287aa8b44b536bd33bd.png)
