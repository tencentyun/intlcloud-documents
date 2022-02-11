This document describes how to view exception alarm messages from DBbrain in the TDSQL-C console.

DBbrain's [exception alarm](https://intl.cloud.tencent.com/document/product/1035/37177) notification service pushes instance exception alarm messages to you in real time, allowing you to conveniently and promptly discover database exceptions and diagnose problems.
All pushed exception alarm messages are displayed in the historical message list, so you can quickly view and locate previously pushed exception diagnosis problems.

## Viewing Alarm
### Method 1
Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb). If an exception diagnosis problem occurs on an instance when you are in the console, a window will pop up in the top-right corner of the console in real time to push the exception alarm message notification, which contains the database instance information such as instance ID, instance name, diagnosis item, and start time, so you can quickly and conveniently stay on top of the running status of the database instance.
- You can click **View Exception Diagnosis Details** in the message notification to view the specific diagnosis details and optimization advice for the instance.
- If you check **No alarm again today** in the message notification, when an exception diagnosis problem occurs in a database instance under your account, no exception alarm messages will be pushed to you in a pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/087767a6d17fb013d509cfd5d72bb77d.png)

### Method 2
Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb), select **Instance List**, **Task List**, **Parameter Template**, or **Recycle Bin** on the left sidebar, and click **Exception Alarm** in the top-right corner to expand the list of historical exception alarm messages. The number of alarms generated in the instances under your account is displayed next to the button.

In the expanded list of historical exception alarm messages, you can view all pushed exception alarm messages. You can view them by region and click a message to view the diagnosis details of the exception alarm event.

![](https://qcloudimg.tencent-cloud.cn/raw/d7b555db2e8876261006b333e3a5aab8.png)
