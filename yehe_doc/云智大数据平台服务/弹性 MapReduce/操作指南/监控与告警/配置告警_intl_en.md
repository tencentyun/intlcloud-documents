## Operation Scenarios
EMR has been connected to Cloud Monitor. You can configure alarm policy for EMR servers and service monitoring metrics in the Cloud Monitor Console.

## Directions
1. Log in to the Cloud Monitor Console and click **Create** on the **[Alarm Policy](https://console.cloud.tencent.com/monitor/policylist)** page.
![](https://main.qcloudimg.com/raw/624095be6772081ea7a6b1c9191b676e.png)
2. Select an EMR service or server monitoring metric alarm policy from the **Policy Type** drop-down list.
 - Service monitoring metrics include HDFS, YARN, Presto, HBase, Spark, Hive, and ZooKeeper.
 - Server monitoring metrics include memory, file handle, CPU, process, etc.
![](https://main.qcloudimg.com/raw/55593982839191bd9f83e331f91c1b30.png)
3. Configure the **alarm object**. There are three methods: "all objects", "select certain objects" (default), and "select instance groups". You can select objects as needed. If there is no instance group, you can click **Create Instance Group** to create one.
![](https://main.qcloudimg.com/raw/b3e822f3c2592da181c4ad81efab67a4.png)
4. Set the **alarm trigger**. You can either choose a trigger template or configure a trigger on your own. For more information on how to set an alarm trigger, please see [Creating Alarm Policies](https://intl.cloud.tencent.com/document/product/248/6215).
![](https://main.qcloudimg.com/raw/c92810fba840f4b079ba9a2b595a3048.png)
5. Configure the **alarm channel**. Specifically, configure the alarm recipient (recipient, recipient group), valid time period, and receipt channel (email, SMS) as needed.
![](https://main.qcloudimg.com/raw/24762d7963bbd302fdfadd1926839faf.png)
6. The callback API is capable of pushing alarm messages to URLs accessible over the public network through HTTP POST requests. You can take further actions based on the alarm messages pushed by the [Callback API](https://intl.cloud.tencent.com/document/product/248/9066).
7. The quotas for alarm SMS messages and policy groups are the same as those listed in the [use limits](https://intl.cloud.tencent.com/document/product/248/32803) of Cloud Monitor.
