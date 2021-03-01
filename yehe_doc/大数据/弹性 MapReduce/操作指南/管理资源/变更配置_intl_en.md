## Feature Overview
In actual use, you may find that the configurations of the nodes in your cluster need to be upgraded, especially when the CPU or memory resources of the master nodes are insufficient. This document describes how to change the instance configuration in the [EMR console](https://console.cloud.tencent.com/emr).

## Prerequisites
1. The instance will be shut down during the change. Please note that the shutdown may affect the normal use of the cluster and even interrupt your business.
2. After the configurations of pay-as-you-go nodes are changed, the billing tier will restart from the first tier.
3. The configurations of local-disk models cannot be changed.
4. The size of data disks and system disks cannot be changed.
5. The target configurations must be higher than or equal to the current configurations.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click a cluster ID/name on the **Cluster List** page to go the cluster details page.
2. On the cluster details page, click **Cluster Resource** > **Resource Management**, select the instance to be changed as needed, and click**Change Configuration** in the **Operation** column.
3. On the configuration adjustment page, confirm the relevant information, read carefully the notes, and select **I have read and understood the notes and agree to the operation**.
![](https://main.qcloudimg.com/raw/9449daf9a2f23296a5809e067a2278ac.png)
![](https://main.qcloudimg.com/raw/f9a125d7198c26904e82ac37936a7123.png)![](https://main.qcloudimg.com/raw/9a7f927da4e46d3c2fe1d0db1ea39d08.png)
4. Select the target configuration, confirm the cost, and click **Start Adjustment** to adjust the configuration.
