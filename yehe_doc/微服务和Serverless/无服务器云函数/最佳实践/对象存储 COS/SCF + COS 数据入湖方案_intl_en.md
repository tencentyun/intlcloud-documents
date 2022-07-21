## Overview

The data lake formation scheme of the serverless architecture is to capture and record the information of a batch of data after starting a data call through a function trigger. This implements various capabilities such as structure conversion, data format conversion, and data compression in the function. In this document, SCF and COS are used to back up TDMQ messages.

## Directions

### Creating COS bucket

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar and click **Create Bucket** to create the source COS bucket.
3. Set the **Name** to **scf-data-lake**, the **Region** to **Guangzhou**, and the **Access Permission** to **Private Read/Write** (default), and click **OK**.

### Creating TDMQ resources

1. Create resources such as cluster and topic in the TDMQ console. For more information, see [Resource Creation and Preparation](https://intl.cloud.tencent.com/document/product/1110/42915).
2. Connect the TDMQ cluster to a VPC. For more information, see [VPC Access](https://intl.cloud.tencent.com/document/product/1110/42932).

### Configuring function through COS app integration 

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **App Integration** on the left sidebar and select **TDMQ Message Backup** in **Data Migration and Backup** as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/867bfe564a2adb5dd6a19ad44a06b5c7.png)
3. On the **TDMQ Message Backup** page, select the region of the created COS bucket and click **Add Function**.   
4. In the **Create TDMQ Message Backup Function** pop-up window, enter the **Function Name** such as `data-lake`, associate the created `scf-data-lake` bucket, select **Authorize SCF Service**, and then click **Next**.
5. Click **Next** to configure TDMQ as follows:
   - **Cluster**: A TDMQ cluster as the message source. Only TDMQ clusters in the same region are supported.
   - **Namespace**: A namespace in the cluster
   - **Topic**: A topic used as the message source
   - **Subscription**: Select a subscription. If existing subscriptions cannot meet your needs, you can create a new one in [Consumption Management](https://console.cloud.tencent.com/tdmq/topic-subscription?rid=1&clusterId=pulsar-5rqmwvrxv8&env=default&topic=zetest) in the TDMQ console.
   - **Start Point**: Start point of historical messages
   - **Role**: Select the TDMQ role (a TDMQ-specific concept, which is different from that mentioned in Tencent Cloud), which is the minimum unit for permission division within TDMQ. You can create multiple roles and grant them different message production/consumption permissions in different namespaces.
   - **Role Key**: Select the TDMQ role key, which is an authentication tool. You can add a key in the client to access TDMQ to produce/consume messages. Each role has a unique key corresponding to itself.
   - **Address**: It must be a VPC access address.
   <dx-alert infotype="notice" title="">
   There must be an available IP in the VPC subnet, and DHCP must be supported.
   </dx-alert>
6. Click **Next** to configure delivery. The configuration item is as follows:
   - **Delivery Path**: It is the delivery path prefix of the backups. If it is not specified, backups will be stored in the root directory of the bucket. The specified prefix must end with a slash (/).
7. Click **Confirm**.
   You can perform the following operations on the created function:
   - Click **View Log** to view the historical running status of TDMQ message backup. If an error is reported, you can click **View Log** to quickly redirect to the SCF console to view the error log details.
   - Click **Edit** to modify a TDMQ message backup rule.
   - Click **Delete** to delete an unwanted TDMQ message backup rule.



### Testing function 
1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq).
2. Click **Topic Management** on the left sidebar and select the target region, cluster, and namespace.
3. On the **Topic Management** list page, click **Send Message** on the right of the associated topic.
4. Enter the message content of up to 64 KB in the pop-up window.
5. Click **Submit**.
6. Go to the details page of the associated COS bucket. For example, check whether a file has been created in the **Delivery Path** defined in `scf-data-lake`, and if so, the TDMQ message backup is successful.
