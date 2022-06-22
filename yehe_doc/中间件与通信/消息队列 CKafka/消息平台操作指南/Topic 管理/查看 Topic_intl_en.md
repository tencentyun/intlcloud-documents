## Overview

This document describes how to view the topic details and producer connection after you create a topic in the CKafka console.

## Directions

### Step 1. View topic details

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, click **Topic Management** to view the topic information and enter the topic list page.
4. On the topic list page, click the right triangle icon on the left of the topic name to view the topic details.
![](https://qcloudimg.tencent-cloud.cn/raw/bda6f0af5afdae2b51bbaa5ecf8d0faa.png)
<table>
    <thead>
    <tr>
        <th>Item</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Partition Name</td>
        <td>Partition name</td>
    </tr>
    <tr>
        <td>Leader</td>
        <td>The leader processes all read/write requests in the partition, and the follower passively and periodically copies the data on the leader</td>
    </tr>
    <tr>
        <td>Replica</td>
        <td>Replica list</td>
    </tr>
    <tr>
        <td>ISR</td>
        <td>Replicas with synced messages</td>
    </tr>
    <tr>
        <td>Start Offset</td>
        <td>The last position of message consumption</td>
    </tr>
    <tr>
        <td>End Offset</td>
        <td>The last position of message write</td>
    </tr>
    <tr>
        <td>Messages</td>
        <td>Number of stored messages</td>
    </tr>
    <tr>
        <td>Unsynced Replicas</td>
        <td>Number of unsynced replicas. You can filter partitions with unsynced replicas</td>
    </tr>
    </tbody>
</table>




### Step 2. View the producer connection

1. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
2. On the instance details page, select **Topic Management** and click **Producer Connection** in the **Operation** column to view the list of producers connected to the topic.
   ![](https://qcloudimg.tencent-cloud.cn/raw/5964448721f3c3a94d4deced5ec2ba88.png)



