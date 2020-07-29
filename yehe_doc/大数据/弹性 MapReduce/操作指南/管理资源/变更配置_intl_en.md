
## Feature Overview
In actual use, you may find that the configurations of nodes in your cluster need to be upgraded, especially when the CPU or memory resources of the MASTER nodes are insufficient. This document describes how to adjust the instance configuration in the [EMR Console](https://console.cloud.tencent.com/emr).

## Prerequisites
1. The instance will be shut down during the scaling. Please note that the shutdown may affect the normal use of the cluster and even interrupt the business.
2. After the configurations of pay-as-you-go nodes are adjusted, the billing tier will restart from the first tier.
3. You can only upgrade the CPU and memory configurations in the same model. Upgrade across models and degrade are not supported.
4. The size of the data and system disks cannot be changed.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Cluster List**, and click the ID/Name of the target cluster to enter the cluster details page.
2. Select **Cluster Resource** on the cluster details page to enter the **Resource Management** page. Select the instance to be adjusted based on your business needs and node type and select **Operation** > **Change Configuration**.
3. On the configuration adjustment page, confirm the relevant information, read the notes carefully, and indicate your consent.
![](https://main.qcloudimg.com/raw/9449daf9a2f23296a5809e067a2278ac.png)
![](https://main.qcloudimg.com/raw/f9a125d7198c26904e82ac37936a7123.png)
4. Select the target configuration. After confirming the cost, click **Start Adjustment** to adjust the configuration.
