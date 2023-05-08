This document describes how to merge topic partitions in the CLS console. By merging partitions in the adjacent range, the number of topic partitions can be reduced to avoid resource waste.

## Must-knows

- Each log topic has at least one partition. If you only have one partition, you cannot merge it.
- Only one object adjacent to the specified topic partition can be merged at a time.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Log Topic** to go to the log topic list page.
3. Find the target topic partition and click its ID/name to enter the **Basic Info** page.
4. In the **Topic Partition Management** section, find the target topic partition and click **Edit** as shown below:
<img src="https://main.qcloudimg.com/raw/874cb934c61a4a89ae74931fcc1c408e.png"/>
6. In the pop-up window, select **Merge** as the **Operation** and select the object to be merged as shown below:
<img src="https://main.qcloudimg.com/raw/e7b755a98381afea764ed14c01066340.png" style="width: 60%;" />
5. Click **OK**.

