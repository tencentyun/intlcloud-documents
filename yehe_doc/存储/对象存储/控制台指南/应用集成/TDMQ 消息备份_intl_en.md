## Overview

COS introduces the [SCF](https://intl.cloud.tencent.com/document/product/583)-based TDMQ Message Backup feature for users to dump TDMQ messages to COS, facilitating data analysis, download, and more.

TDMQ, based on the open-source Apache [Pulsar](https://pulsar.apache.org/) project, is a Tencent Cloud−developed distributed messaging middleware at the financial level, featuring cross-region strong consistency, and high reliability and concurrence.

If a backup rule has been configured for a bucket, SCF will dump messages generated in TDMQ to the COS bucket according to the specified time granularity.

## Notes

- If you have added a TDMQ message backcup rule to your bucket via the COS console, the function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete the function. Otherwise, your rule may not take effect.
- Currently, regions that support backing up TDMQ messages to COS include Guangzhou, Shanghai, Hong Kong (China), Beijing, Chengdu, Singapore, and Silicon Valley.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Application Integration**. Then, find **TDMQ Message Backup**.
3. Click **Configure Backup Rules** to go to the configuration page.
4. Click **Add Function**.
>! If you haven’t activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
>
5. On the page that is displayed, configure the following items:
 - **Function Name**: uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Associated Bucket**: a COS bucket that stores TDMQ messages
 - **Time Granularity**: an interval (5−15 minutes) to aggregate messages according to the message volume. Each message file can be up to 500 MB and contain up to 5,000 pieces of messages.
 - **SCF Authorization**: (required) SCF needs to be authorized to read TDMQ messages and dump the messages to the specified bucket.
6. Click **Next** to configure TDMQ. The configuration items are described as follows:
 - **Cluster**: a TDMQ cluster as the message source. Only TDMQ clusters in the same region are supported.
 - **Namespace**: a namespace in the cluster
 - **Topic**: a topic used as the message source
 - **Subscription**: topic subscription. If the current subscriptions do not meet your requirements, you can go to the **TDMQ console** > [Consumption Management](https://console.cloud.tencent.com/tdmq/topic-subscription?rid=1&clusterId=pulsar-5rqmwvrxv8&env=default&topic=zetest) to create a subscription.
 - **Start Point**: start point of historical messages
 - **Role**: select the TDMQ role (a TDMQ-specific concept, which is different from that mentioned in Tencent Cloud), which is the minimum unit for permission division within TDMQ. You can create multiple roles and grant them different message production/consumption permissions in different namespaces.
 - **Role Key**: select the TDMQ role key, which is an authentication tool. You can add a key in the client to access TDMQ to produce/consume messages. Each role has a unique key corresponding to itself.
 - **Address**: A VPC address is required and the TDMQ cluster must be connected to the VPC.
>! An IP address in the corresponding VPC subnet must be available and support DHCP.
>
7. Click **Next** to configure delivery. The configuration items are described as follows:
**Destination Path**: a path to deliver the backup messages. If this field is not specified, the files will be stored in the root directory of the bucket. To use a prefix, end it with a slash (/).
8. Click **Confirm**.
You can perform the following operations on the created function:
 - Click **View Log** to view the historical running status of the TDMQ message backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console for viewing the error log details.
 - Click **Edit** to modify the TDMQ message backup rule.
 - Click **Delete** to delete an unwanted TDMQ message backup rule.
