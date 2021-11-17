## Overview


You can configure a TDMQ connector to consume content in TDMQ message queues. A TDMQ connector is implemented in the **pull pattern**. It automatically pulls TDMQ content and routes events to relevant services through event rules. This document describes how to create a TDMQ connector and the TDMQ connector data structure.


## Prerequisites

You have [created an event bus](https://intl.cloud.tencent.com/document/product/1108/42285).



## Directions


1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb/) and select **Event Bus** on the left sidebar.
2. In the **Event Bus** list, select the event bus for which you want to configure a TDMQ connector.
3. Click **Add** in the connector configuration section on the **Event Bus Details** page 
4. Enter the relevant information as prompted 
	 Here, select **TDMQ** for **Connector Type** and enter other configuration items as prompted.
5. Click **OK**.
6. Select **Event Rule** on the left sidebar.
7. In the drop-down lists at the top of the **Event Rule** page, select the same connector information as that set during connector creation and click **Create Event Rule** 
8. Enter the relevant information as prompted 
Here, select **TDMQ** for **Tencent Cloud Service Type** and configure the event target.
9. Click **OK**.

     


#### TDMQ connector data structure description

```json
{
   {
    "specversion": "0",
    "id": "13a3f42d-7258-4ada-da6d-023a333b4662",
    "type": "connector:tdmq",
    "source": "tdmq.cloud.tencent",
    "subjuect": "qcs::tdmq:$region:$account:topicName/$topicSets.clusterId/$topicSets.environmentId/$topicSets.topicName/$topicSets.subscriptionName",
    "time": "1615430559146",
    "region": "ap-guangzhou",
    "datacontenttype": "application/json;charset=utf-8",
    "data": {
					"topic":  "persistent://appid/namespace/topic-1",
            "tags": "testtopic",
					"TopicType": "0",
					"subscriptionName": "xxxxxx",
					"toTimestamp": "1603352765001",
            "partitions": "0",
					"msgId": "123345346",
					"msgBody": "Hello from TDMQ!"
    }
}
```

The parameters are as detailed below:

| Parameter | Description |
| ---------------- | ------------------------------------------------------------ |
| topic            | Complete topic path, such as `persistent://appid/namespace/topic-1`.      |
| subscriptionName | Subscription name.                                                   |
| timestamp        | Timestamp accurate down to the millisecond.                                         |
| tags             | TDMQ tag.                                                  |
| msgId            | TDMQ message ID.                                               |
| msgBody          | TDMQ message body.                                                |
| topictype        | Topic type: <br><li>0: general message.<br><li>1: global sequential message.<br><li>2: local sequential message.<br><li>3: retry queue.<br><li>4: dead letter queue. |







