## Overview

This document describes how to view the topic details and producer connection after you create a topic in the CKafka console.

## Directions

### Step 1. View topic details

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, click **Topic Management** to view the topic information and enter the topic list page.
4. On the topic list page, click the right triangle icon on the left of the topic name to view the topic details.
![](https://qcloudimg.tencent-cloud.cn/raw/7f6529767f555abba5f9a0d31fddc51f.png)
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
        <td>The partition name.</td>
    </tr>
    <tr>
        <td>Leader</td>
        <td>The leader processes all read/write requests in the partition, and the follower passively and periodically copies the data on the leader.</td>
    </tr>
    <tr>
        <td>Replica</td>
        <td>The replica list.</td>
    </tr>
    <tr>
        <td>ISR</td>
        <td>Replicas with synced messages.</td>
    </tr>
    <tr>
        <td>Start Offset</td>
        <td>The last position of message consumption.</td>
    </tr>
    <tr>
        <td>End Offset</td>
        <td>The last position of message write.</td>
    </tr>
    <tr>
        <td>Messages</td>
        <td>The number of stored messages.</td>
    </tr>
    <tr>
        <td>Unsynced Replicas</td>
        <td>The number of unsynced replicas. You can filter partitions with unsynced replicas.</td>
    </tr>
    </tbody>
</table>




### Step 2. View the producer connection

> ?Currently, you can view the producer connections only of instances on v2.4 or later.

1. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
2. On the instance details page, select **Topic Management** and click **Producer Connection** in the **Operation** column to view the list of producers connected to the topic.
    ![](https://qcloudimg.tencent-cloud.cn/raw/b6d5b5f3b3699dacc36ece753768838c.png)
