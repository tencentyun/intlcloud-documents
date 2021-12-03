## Operating System Description[](id:OS)

- Changes to the OS only affect new nodes and reinstalled nodes, not existing nodes.
- Nodes in the same cluster can use different OS versions without affecting cluster functionality.
- One script does not suit all operating systems. After configuring a node with a script, run a test to make sure it is compatible with the operating system.
- If you want to use custom images, [submit a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&level3_id=718&radio_title=%E5%AE%B9%E5%99%A8%E9%9B%86%E7%BE%A4%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98&queue=97&scene_code=16798&step=2) for further assistance.
## Operation Directions

### Changing the default OS of a cluster
>? Before changing the default OS of a cluster, read [Operating System Description](#OS) carefully to learn about the relevant risks.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, select **View Cluster Credential** for the target cluster to go to the basic information page of the cluster.
3. In **Node and Network Information**, click <img src="https://main.qcloudimg.com/raw/12834a28b9839ffe9a3723ca23ba19ce.png" style="margin:-3px 0px"> next to **Default OS**. See the figure below:
![](https://main.qcloudimg.com/raw/1bdc4b288f01e31c93504d21dc865c6f.png)
4. On the **Set Cluster OS** page, change the OS and click **Submit**. See the figure below:
![](https://main.qcloudimg.com/raw/9bd3d607c7897232a02df96ca52558dd.png)

