## Scenario
The startup script of a node can help you initialize the node before the node becomes ready. The configured script is executed when the node starts. If you purchase multiple CVM instances at a time, the custom data will run on all of them.

## Use Limits

- Do not modify configurations such as those for kubelet, kube-proxy, and docker on the TKE node in the startup script.
- If the startup script fails to be executed, it will not be executed again. Therefore, you must ensure the executability of the script or ensure that a retry mechanism is available.
- You can view the script and its log file in the `/usr/local/qcloud/tke/userscript` path of the node.

## Directions

You can configure the startup script for a node in the following scenarios:
- [Configuring the node startup script when creating a cluster or a node](#CreateClusterOrCreateNode)
- [Configuring the node startup script when adding an existing node](#CreateCVM)
- [Configuring the node startup script when creating a scaling group](#CreateFlexGroup)

<span id="CreateClusterOrCreateNode"></span>
### Configuring the node startup script when creating a cluster or a node
- When [creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637), click **Advanced Settings** on the "CVM Configuration" page and complete custom data as a startup script, as shown in the following figure:
![](https://main.qcloudimg.com/raw/fd22ee1caca15449ea74114d5462c6a4.png)
- When [adding a node](https://intl.cloud.tencent.com/document/product/457/30652), click **Advanced Settings** on the "CVM Configuration" page and complete custom data as a startup script, as shown in the following figure:
![](https://main.qcloudimg.com/raw/7b793fca3791823d14c45d17df6aa106.png)

<span id="CreateCVM"></span>
### Configuring the node startup script when adding an existing node
- When [adding an existing node](https://intl.cloud.tencent.com/document/product/457/30652#addExistingNode), click **Advanced Settings** on the "CVM Configuration" page and complete custom data as a startup script, as shown in the following figure:
![](https://main.qcloudimg.com/raw/94f828deadbc7bfc4d9ed8357ddfc84d.png)

<span id="CreateFlexGroup"></span>
### Configuring the node startup script when creating a scaling group
- When [creating a scaling group](https://intl.cloud.tencent.com/document/product/457/30638), click **Advanced Settings** on the "Launch Configuration" page and complete custom data as a startup script, as shown in the following figure:
![](https://main.qcloudimg.com/raw/13fb463e4ea280910701110ab20b09ab.png)




