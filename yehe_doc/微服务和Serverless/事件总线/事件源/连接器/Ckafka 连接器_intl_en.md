## Overview


You can configure a CKafka connector to consume content in CKafka message queues. A CKafka connector is implemented in the **pull pattern**. It automatically pulls CKafka content and routes events to relevant services through event rules. This document describes how to create a CKafka connector and the CKafka connector data structure.


## Prerequisites

You have [created an event bus](https://intl.cloud.tencent.com/document/product/1108/42285).



## Directions


1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb/) and select **Event Bus** on the left sidebar.
2. In the **Event Bus** list, select the event bus for which you want to configure a CKafka connector.
3. Click **Add** in the connector configuration section on the **Event Bus Details** page 
4. Enter the relevant information as prompted 
 Here, select **CKafka** for **Connector Type** and enter other configuration items as prompted.
   <dx-alert infotype="notice" title="">
Currently, only delivery for Tencent Cloud CKafka instances is supported. Please confirm that no username and password have been configured for your CKafka instances; otherwise, the connector may fail to get messages.
</dx-alert>
5. Click **OK**.
6. Select **Event Rule** on the left sidebar.
7. In the drop-down lists at the top of the **Event Rule** page, select the same connector information as that set during connector creation and click **Create Event Rule** 
8. Enter the relevant information as prompted 
Here, select **CKafka** for **Tencent Cloud Service Type** and configure the event target.
9. Click **OK**.

     


#### CKafka connector data structure description

```json
 {       
        "specversion":"0",       
        "id":"13a3f42d-7258-4ada-da6d-023a333b4662",    
        "type":"connector:kafka",   
        "source":"ckafka.cloud.tencent",   
        "subjuect": "qcs::ckafka:ap-guangzhou:uin/1250000000:ckafkaId/uin/1250000000/ckafka-123456",     
        "time":"1615430559146",   
        "region":"ap-guangzhou",       
        "datacontenttype":"application/json;charset=utf-8",   
        "data":{             
             "topic":"test-topic",         
             "Partition":1,         
             "offset":37,         
             "msgKey":"test",         
             "msgBody":"Hello from Ckafka again!"      
           }
}
```

The parameters are as detailed below:

| Parameter | Description |
| ---------------- | ------------------------------------------------------------ |
| topic            | CKafka delivery topic.     |
| Partition | Event source partition. One topic can contain one or more partitions. CKafka uses partition as an allocation unit.                                                   |
| offset        | Consumer group, which specifies the consumption start point.                                      |
| msgKey            | CKafka message key.                                               |
| msgBody          | CKafka message body.                                                |









