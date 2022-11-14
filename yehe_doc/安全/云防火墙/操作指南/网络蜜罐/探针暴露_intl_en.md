To use the network honeypot service, please associate probes first. You can create probes as follows.

## Creating probes
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw) and click **Network Honeypots** in the left navigation pane.
2. On the **Network honeypot** page, click **Probes**.
![](https://qcloudimg.tencent-cloud.cn/raw/3008f692d515dd0475197e4f8ac6b3a7.png)
3. On the **Probes** page, click **Create probe**.
3. In the **Create probe** window displayed, select a region, instance name, deployment mode, and honeypot service, and then click **OK**.
>? Different deployment modes require different parameters. For more information, please see [Parameters](#explain).

![](https://qcloudimg.tencent-cloud.cn/raw/e2324c9c522b909298a0f291261720ba.png)

**Parameters**[](id:explain)

 - Region: All regions in China are available. The region cannot be modified after the instance is created.
 - Instance name: Enter the name of the instance.
 - Deployment mode
     - Private IP: Select a subnet, and an ENI and private IP will be created. You can set the specified port of this IP to forward traffic to the honeypot service.
     - Public IP: Deploy a probe on an existing public IP to forward all traffic to the specified port of this IP to the honeypot service.
     - Load balancer: Deploy a probe on an existing CLB instance to forward all traffic of the path on the specified domain name to the honeypot service.
 - Select a subnet: This should be set when the deployment mode is private IP.
 - IP address: This should be set when the deployment mode is private IP.
 - Elastic IP: This should be set when the deployment mode is public IP. Select **Create EIP**.
 - Deployment instance: This should be set when the deployment mode is load balancer. Set this as needed.
 - Domain name: 	This should be set when the deployment mode is load balancer. Set this as needed.
 - Forwarder: This should be set when the deployment mode is load balancer. Select a CVM instance in the VPC of the current CLB instance as the backend service of the current listener. Only Linux CVMs are supported.
 - Honeypot service: Choose **Quick select** or **Advanced settings**.
    - Quick select: Click **Quick select** and select the desired honeypot service.
>? As the web honeypot service needs to use an existing SSH/MySQL honeypot as bait, the web honeypot will not automatically associate bait after quick selection. If you click **Quick select** and select the web honeypot when creating a probe, the honeypot service will not be effective right away. You need to find the corresponding web honeypot editor and associate it with an SSH/MySQL honeypot, and then the web honeypot service will take effect.

 ![](https://qcloudimg.tencent-cloud.cn/raw/dd93e594f3aedb13b406339a1a72b67f.png)
- Advanced settings: You can add an existing honeypot or create one to associate.
  - Add existing: Click **Add existing**, select the desired honeypot, and modify the listening port or input path as required.
>?
>- When the deployment mode is public IP, you can modify the listening port.
>- When the deployment mode is load balancer, you can modify the input path.

![](https://qcloudimg.tencent-cloud.cn/raw/d19c6d64f62a15b5b45defd026c77d53.png)
	
  - Create: Click **Create**, configure the parameters, and click **OK** to add the honeypot service to the **Create probe** window.

 


## Managing probes
- **Filtering/Sorting**
  - On the **Probes** page, click the search box to filter probe events by keywords such as **probe ID** or **probe name**.
- Click **Region**, **VPC**, **Deployment method**, **Deployment instance**, and **Forwarder** in the header of the probe list to filter probe events.
  - Click **Forward to honeypot** and **Hit count** in the header of the probe list to display probe events in ascending or descending order.
- **Enabling probes**
 1. On the **Probes** page, you can enable probes individually or batch enable probes as follows.
    - Select a probe ID and click ![](https://qcloudimg.tencent-cloud.cn/raw/8cac7be9ccea6507c5c6929c59bea379.png) or **Enable probe**.
    - Select multiple probe IDs and click **Enable probe**.
 2. In the confirmation window displayed, click **OK** to enable the probe(s).
- **Disabling probes**
 1. On the **Probes** page, you can disable probes individually or batch disable probes as follows.
    - Select a probe ID and click ![](https://qcloudimg.tencent-cloud.cn/raw/84f13fcacfe7ed9b2bf9716f493d106d.png) or **Disable probe**.
- Select multiple probe IDs and click **Disable probe**.
 2. In the confirmation window displayed, click **OK** to disable the probe(s).


## Modifying probes
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw) and click **Network Honeypots** in the left navigation pane.
2. On the **Network honeypot** page, click **Probes**.
3. On the **Probes** page, select a probe event and click **Modify**.
4. In the **Modify probe** window displayed, modify the instance name and honeypot service type, and then click **OK** to save the modifications.

## Deleting probes
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw) and click **Network Honeypots** in the left navigation pane.
2. On the **Network honeypot** page, click **Probes**.
1. On the **Probes** page, you can delete probes individually or batch delete probes.
 - Select a probe ID and click **Delete** or **Delete probe**.
 - - Select multiple probe IDs and click **Delete probe**.
2. In the confirmation window displayed, click **OK** to delete the probe(s).
