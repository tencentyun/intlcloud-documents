## Overview

COS introduces the [SCF](https://intl.cloud.tencent.com/document/product/583)-based CKafka Message Backup feature for users to dump CKafka messages to COS, facilitating data analysis, download, and more.

Based on the open-source Apache Kafka message queuing engine, Tencent Cloud Kafka (CKafka) provides high-throughput and highly scalable message queuing services. For more information, please see [CKafka Product Overview](https://intl.cloud.tencent.com/document/product/597/10066).

If a backup rule has been configured for a bucket, messages generated in a CKafka instance will be dumped to the COS bucket according to the specified time granularity.

## Notes

- If you have added a CKafka message backup rule to your bucket via the COS console, the function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- SCF-available regions support backing up CKafka messages to COS, including Guangzhou, Shanghai, Hong Kong (China), Beijing, Chengdu, Singapore, Mumbai, Toronto, Silicon Valley, and more. For more supported regions, please see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Application Integration**. Then, find **CKafka Message Backup**.
3. Click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
>! If you haven't activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. In the pop-up window, configure the following information:

 - **Function Name**: uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: a COS bucket that stores CKafka messages
 - **Time Granularity**: You can set an interval (5−15 minutes) to aggregate messages according to the message volume. The dumping performance is affected by the number of files aggregated, the number of partitions, and the value of `partition_max`. For more information, please see **Partition** in [Glossary](https://intl.cloud.tencent.com/document/product/597/32275).
 - **SCF Authorization**: (required) SCF needs to be authorized to read messages of CKafka instances and dump the messages to the specified bucket.
6. Click **Next** to configure CKafka. The configuration items are as follows:

 - **Instance**: a CKafka instance as the message source. Only instances in the same region are supported.
 - **Topic**: a topic used as the message source
 - **Start Point**: the topic offset for dumping the backup messages
 - **Address**: a VPC address is required. CKafka instances that use a classic network require a routing policy. For more information, please see [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555).
>! An IP address in the corresponding VPC subnet must be available and support DHCP.
>
7. Click **Next** to configure delivery. The configuration item is as follows:

**Destination Path**: a path to deliver the backup messages. If this field is not specified, the files will be stored in the root directory of the bucket. To use a prefix, end it with a slash (/).
8. Click **Confirm**.

You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of the CKafka message backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **Edit** to modify the CKafka message backup rule.
 - Click **Delete** to delete an unwanted CKafka message backup rule.

