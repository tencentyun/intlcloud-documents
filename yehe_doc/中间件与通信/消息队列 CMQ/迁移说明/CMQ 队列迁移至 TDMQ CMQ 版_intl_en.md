## Overview

This document takes the Java client as an example to describe how to migrate a CMQ queue to TDMQ for CMQ.

**Migration principle**
<img src="https://main.qcloudimg.com/raw/bd0a7851575796b8c954eeeb6dcf8144.png" width="569">


**Scheme overview**
<img src="https://main.qcloudimg.com/raw/a6e13ca122d8524b365c83b53ec05c9b.png" width="569">


**Overall process**
<dx-steps>
- Migrate the CMQ queue and topic metadata to TDMQ for CMQ in the CMQ console.
- Keep the old consumer unchanged, create a new consumer, and connect it to the TDMQ for CMQ queue.
- The producer stops producing messages for the original CMQ queue and switches the production stream to the TDMQ for CMQ queue.
- The old CMQ consumer continues consuming existing messages in the original CMQ queue. After the consumption is completed, deactivate it.
</dx-steps>


## Prerequisites

You have deployed CMQ queue producer and consumer services as instructed in [SDK for TCP](https://intl.cloud.tencent.com/document/product/406/34256), and they are running normally. The following migration process takes the SDK for TCP as an example.

## Directions

### Step 1. Migrate the metadata

1. Log in to the [CMQ console](https://console.cloud.tencent.com/cmq).
2. Select **Queue** on the left sidebar, select a **Region**, and click **Sync to TDMQ** at the top of the page.
3. In the pop-up window, click **Start** to migrate all queue and topic metadata in the region to TDMQ for CMQ.
   ![](https://main.qcloudimg.com/raw/0d1d65697c56dfa776c6036a52eb3d79.png)
4. After the migration is completed, log in to the [TDMQ](https://console.cloud.tencent.com/tdmq) console.
5. Select **Queue Service** on the left sidebar, select the same **Region**, and you can see the queues migrated to TDMQ for CMQ.
	 ![](https://main.qcloudimg.com/raw/f74407c4a979dc3b01cb18c4d37ed729.png)

### Step 2. Create a consumer

1. Create a consumer and connect it to the target TDMQ for CMQ queue.
```java
Consumer consumer = new Consumer();
        // VPC address: http://{region}.mqadapter.cmq.tencentyun.com. CVM instances in a VPC can be accessed over the private network
        // Public network address: https://cmq-{region}.public.tencenttdmq.com
        consumer.setNameServerAddress("http://****.com");
        // Set `SecretId`, which is required and can be obtained from the console
        consumer.setSecretId("****");
        // Set `SecretKey`, which is required and can be obtained from the console
        consumer.setSecretKey("****");
        // Set the signature algorithm, which is optional and is SHA1 by default
        consumer.setSignMethod(ClientConfig.SIGN_METHOD_SHA256);
        // Set the maximum number of messages that can be pulled in batches, which ranges from 1 to 16
        consumer.setBatchPullNumber(16);
        // Set the wait timeout period, which is 10s by default. You can pass in the specific wait time in methods such as `consumer.receiveMsg`
        consumer.setPollingWaitSeconds(6);
        // Set the request timeout period, which is 3,000 ms by default
        // If you set the wait timeout period to 6s and request timeout period to 5,000 ms, the final timeout period will be (6 * 1000 + 5000) ms
        consumer.setRequestTimeoutMS(5000);
        // Name of the queue from which messages are pulled
        final String queue = "****";
```
	- NameServerAddress: API call address, which can be copied in **Queue Service** > **API Request Address** in the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq).
![](https://main.qcloudimg.com/raw/bbc5dc77a8475304377d00cc92028e01.png)

	- SecretId and SecretKey: TencentCloud API key, which can be copied in **Access Key** > **API Key Management** in the [CAM console](https://console.cloud.tencent.com/cam/overview).
		![](https://main.qcloudimg.com/raw/867837e2b1e6d347ecb04d7085938c08.png)
	- queue: Queue name.

2. Run the code and check whether the consumer service can run normally with no errors reported.

3. In **Queue Service** > **Send Message** in the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq), send a test message to the message recipient to check whether the consumer service can consume normally.
   ![](https://main.qcloudimg.com/raw/1c2f1532860b51440bbf2a42285fb644.png)
Normal consumption is as shown below:
   ![](https://main.qcloudimg.com/raw/959a9b688673054d7449913d71f89b4b.png)


### Step 3. Switch the production stream

1. Change the `NameServer` value of the original producer to the access address of the TDMQ for CMQ queue, which can be copied in **Queue Service** > **API Request Address** in the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq).
2. Run the message production program to check whether the producer service can send messages normally.
   ![](https://main.qcloudimg.com/raw/7c258f9b7cfd517f1bb6f735416c0f44.png)

### Step 4. Deactivate the old consumer

After the old CMQ consumer has consumed all existing messages in the original CMQ queue, deactivate it.

On the **Monitoring** page in **Queue Service** > **Queue** in the [CMQ console](https://console.cloud.tencent.com/cmq), you can view the number of heaped messages in the CMQ queue. If it is 0, existing messages in the original CMQ queue have all been consumed.

![](https://main.qcloudimg.com/raw/30e7cd4d0a9ccad13a72a8d4c6bfe2e6.png)
