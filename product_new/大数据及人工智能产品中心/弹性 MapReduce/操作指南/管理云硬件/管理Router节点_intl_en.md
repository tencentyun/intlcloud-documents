
## Scenario
Generally, processes such as Hive, Hue, and Spark are deployed on a master node by default, and tasks are deployed and submitted there too. If the cluster is very large or has too many applications deployed, the master node may run out of memory. In this case, one or more router nodes can be added to share the load of processes of the master node. They can be used in the same way as the master node to relieve the pressure on it.

A router node can be used as a submitter; therefore, you can submit Yarn, Hive, and Spark computation tasks to the cluster through it.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and select **Cloud Hardware Management** in the left sidebar.
2. On the cloud hardware list page, click **Add Router Node**.
3. On the router adding page, you can choose the **required** and **optional** components (based on your business needs) to be deployed on the router node.
![](https://main.qcloudimg.com/raw/6020ac84b9db1fdd1f6c6a5a3319b676.png)
4. Click **Next** to configure the payment type, disk type, quantity, and other items. Multiple router nodes can be added at a time.
![](https://main.qcloudimg.com/raw/476a4836ed2c98a5a5c6c759ab4a5f2a.png)
5. After confirming that everything is correct, click **Purchase**. After making the payment, you can return to the console to view the newly added router nodes.
