## Feature Overview
The cluster script feature allows you to run a script on multiple nodes at a time for higher efficiency. Only one cluster script can be run in a cluster at a time. If a cluster script is running (such as installing a third-party software or modifying the running environment of the cluster), you cannot submit and execute new cluster scripts.

>!
>- Only files in COS can be selected as the script to run.
>- Only nodes in the current cluster can be selected to run the script on.
>- You can set custom parameters based on your business requirements.
>- The EMR console does not verify the scripts you run. Therefore, running a custom script is risky, so please operate with caution.

## Prerequisites
- The cluster script feature is only available for clusters that are running.
- The script to be run must be a shell script file in the COS STANDARD storage class.
- To use the cluster script feature, you must grant EMR the permission to access COS.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click a cluster ID in the cluster list to go the instance information page. Click **Cluster Scripts** > **Set Task**.
![](https://main.qcloudimg.com/raw/1a361319fc4a2f500c03d4506dd0281e.png)                      
2. Set the **Task Name**, **Script**, **Nodes**, and **Custom Parameter** fields. After that, click **Run** to generate a task in the task list.
![](https://main.qcloudimg.com/raw/5f9805e96432d2997c04fe3fb09458e7.png)
3. There are various task statuses depending on the execution results, including successful, failed, partially failed, etc. You can click **Details** to view details.
![](https://main.qcloudimg.com/raw/9b1425a37ce28e469490943f88a476e8.png)
![](https://main.qcloudimg.com/raw/af3c17449632829bf34373ec4414be09.png)
4. A cluster script may run successfully on some nodes and fail on other nodes. You can batch copy the failed nodes to run the script again.
