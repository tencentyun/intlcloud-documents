This document describes how to create a CKafka trigger and invoke a function.

### Step 1. Create a function
1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list-create?rid=1&ns=default).
2. On the function creation page, select **Template**, search for `CKafka`, and select	
**CkafkaSCFCOS** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d89b622a7b1ceecb4ed32811404f3940.png)
2. Click **Next**.



### Step 2. Configure a trigger
On the **Function configuration** page, set the basic configurations of the function.
1. In **Trigger configurations**, select **Custom** to create a trigger as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ebce10b5fa8aa354cff54970c65b3c5d.png)
Select **CKafka trigger** and configure the name, topic, and other information of the CKafka instance as the message source as prompted. You can also choose to [create a CKafka instance](https://console.cloud.tencent.com/ckafka/index?rid=1).
>! Make sure that your function and CKafka instance are in the same VPC.
>
2. Click **Complete**.

### Step 3. Manage the trigger
After the function is created, go to the function details page, and you can see the created trigger in **Trigger management**. You can also turn triggers on or off there.
