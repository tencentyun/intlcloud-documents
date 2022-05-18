## Overview

Maintenance time is a very important concept for CKafka. To ensure the stability of your CKafka instance, the backend system performs maintenance operations on the instance during the maintenance window from time to time. We highly recommend you set an acceptable maintenance time for your business instance, usually during off-peak hours, so as to minimize the potential impact on your business.

>?
> - The default system maintenance time is 23:00 and lasts one hour. You can modify the time for CKafka Pro Edition instances but not for Standard Edition instances.
>- Before maintenance is carried out for CKafka, notifications will be sent to the contacts configured in your Tencent Cloud account through SMS and email.

## Setting Maintenance Time

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. In the **Basic Info** module, click **Edit** next to the system maintenance time.
4. In the pop-up window, select **Maintenance Window** and **Maintenance Time** and click **OK**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/3a704cdf77023480676a38ab9757c81b.png)
5. Click **OK**.

