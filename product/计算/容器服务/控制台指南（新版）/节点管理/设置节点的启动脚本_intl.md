## Operation Scenario

Setting the startup script of a node can help you initialize the node before the node is ready, i.e., running the configured script when the node starts. If you purchase multiple CVM instances at a time, the custom data will run on all of them.

## Usage Restrictions

- It is recommended that you restrain yourself from modifying configurations such as Kubelet, kube-proxy, and docker on the TKE node through the startup script.
- If the startup script fails to run, it will not be retried. You should ensure the executability and retry mechanism of the script.
- The script and its generated log files can be viewed in /data/ccs_userscript/.

## Steps

You can set the node startup script in the following three scenarios:
- [Setting the node startup script when creating a cluster or node](#CreateClusterOrCreateNode)
- [Setting the node startup script when adding an existing node](#CreateCVM)
- [Setting the node startup script when creating a scaling group](#CreateFlexGroup)

<span id="CreateClusterOrCreateNode"></span>
### Setting the Node Startup Script When Creating a Cluster or Node

- When [creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637), on the "CVM configuration" page, click **Advanced settings** and enter the custom data as startup script. See the figure below:
![](https://main.qcloudimg.com/raw/560dcc9134c038e134eb5bc51e97c509.png)
- When [creating a node](https://intl.cloud.tencent.com/document/product/457/30652), on the "CVM configuration" page, click **Advanced settings** and enter the custom data as startup script. See the figure below:
![](https://main.qcloudimg.com/raw/ad152b5cfe371fbc973a7174658eea04.png)

<span id="CreateCVM"></span>
### Setting the Node Startup Script When Adding an Existing Node

- When [adding an existing node](https://intl.cloud.tencent.com/document/product/457/30652#addExistingNode), on the "CVM configuration" page, click **Advanced settings** and enter the custom data as startup script. See the figure below:
![](https://main.qcloudimg.com/raw/ad152b5cfe371fbc973a7174658eea04.png)

<span id="CreateFlexGroup"></span>
### Setting the Node Startup Script When Creating a Scaling Group

- When [creating a scaling group](https://intl.cloud.tencent.com/document/product/457/30638#AutomaticAddAndRemove), on the "CVM configuration" page, click **Advanced settings** and enter the custom data as startup script. See the figure below:
![](https://main.qcloudimg.com/raw/560dcc9134c038e134eb5bc51e97c509.png)




