## Overview

TDMQ message backup is provided by COS based on [SCF](https://www.tencentcloud.com/document/product/583) to dump TDMQ messages to COS, which facilitates data analysis and download.

TDMQ is a proprietary finance-grade distributed message middleware developed based on [Pulsar](https://pulsar.apache.org/), an open-source project of Apache. It features high cross-region consistency, reliability, and concurrency. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1110/42904).

If a backup rule has been configured for a bucket, SCF will dump messages generated in TDMQ to a COS bucket according to the specified time granularity.

## Notes

- If you have added a TDMQ message backup rule to your bucket via the COS console, the function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- Currently, regions that support backing up TDMQ messages to COS include Guangzhou, Shanghai, Hong Kong (China), Beijing, Chengdu, Singapore, and Silicon Valley.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **App Integration** > **Data Backup** and find **TDMQ Message Backup**.
3. Click **Configure Backup Rule** to go to the rule configuration page.
4. Click **Add Function**.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. In the pop-up window, configure the following items:

 - **Function Name**: Uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: A COS bucket that stores TDMQ messages
 - **Time Granularity**: An interval (5−15 minutes) to aggregate messages according to the message volume. Each message file can be up to 500 MB and contain up to 5,000 pieces of messages.
 - **SCF Authorization**: (required) SCF needs to be authorized to read TDMQ messages and dump the messages to the specified bucket.
6. Click **Next** to configure TDMQ as follows:

 - **Cluster**: A TDMQ cluster as the message source. Only TDMQ clusters in the same region are supported.
 - **Namespace**: A namespace in the cluster
 - **Topic**: A topic used as the message source
 - **Subscription**: Select a subscription. If existing subscriptions cannot meet your needs, you can create a new one in the [TDMQ console](https://console.cloud.tencent.com/tdmq/cluster?rid=1).
 - **Start Point**: Start point of historical messages
 - **Role**: Select the TDMQ role (a TDMQ-specific concept, which is different from that mentioned in Tencent Cloud), which is the minimum unit for permission division within TDMQ. You can create multiple roles and grant them different message production/consumption permissions in different namespaces.
 - **Role Key**: Select the TDMQ role key, which is an authentication tool. You can add a key in the client to access TDMQ to produce/consume messages. Each role has a unique key corresponding to itself.
 - **Address**: It must be a VPC access address. The TDMQ cluster should be connected to the VPC. For more information, see [VPC Access](https://intl.cloud.tencent.com/document/product/1110/42932).
>! An IP address in the corresponding VPC subnet must be available and support DHCP.
>
7. Click **Next** to configure delivery. The configuration item is as follows:
**Destination Path**: A path to deliver the backup messages. If this field is not specified, the files will be stored in the root directory of the bucket. To use a prefix, end it with a slash (/).
8. Click **Confirm**.
You can perform the following operations on the created function:
 - Click **Log** to view the historical running status of TDMQ message backup. If an error is reported, you can click **Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **More** > **Edit** to modify a TDMQ message backup rule.
 - Click **More** > **Delete** to delete an unwanted TDMQ message backup rule.
