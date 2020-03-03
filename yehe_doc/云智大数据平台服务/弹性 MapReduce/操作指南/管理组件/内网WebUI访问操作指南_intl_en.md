When creating an EMR cluster, if you do not check "Enable Public Network Access for Cluster Master Node", you cannot access the WebUIs of relevant components through the native WebUI access addresses on the component management page. This document describes how to view native component WebUIs in a cluster where the public network access to master node is not enabled.
## Private Network Access

You can use a browser to access a component's WebUI over the private network. Below are the links to native WebUIs of each component:

| Component     | Link                      |
| ---------- | ------------------------- |
| HDFS UI    | `http://{cluster private IP}:4008`  |
| YARN UI    | `http://{cluster private IP}:5004`  |
| HBASE UI   | `http://{cluster private IP}:6001`  |
| HIVE UI    | `http://{cluster private IP}:7003`  |
| HUE UI     | `http://{cluster private IP}:13000` |
| RANGER UI  | `http://{cluster private IP}:6080`  |
| STROM UI   | `http://{cluster private IP}:15001` |
| OOZIE UI   | `http://{cluster private IP}:12000` |
| GANGLIA UI | `http://{cluster private IP}:1800`  |
| PRESTO UI  | `http://{cluster private IP}:9000`  |
| ALLUXIO UI | `http://{cluster private IP}:19999` |

## Binding an EIP

You can bind an elastic public IP (EIP) to the master node by following the steps below to access component WebUIs from a browser over the public network:
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), enter the **Cloud Hardware Management** page, select the master node to which to bind an EIP, and click the instance ID to enter the CVM Console.
![](https://main.qcloudimg.com/raw/1320e6c28fa4a13289c7bdf671e42517.png)
2. Adjust the network bandwidth settings of the CVM instance to which the EIP will be bound and make sure that its bandwidth is not 0; otherwise, the node cannot be connected.
In the CVM instance list in the CVM Console, select **More** > **Resource Adjustment** > **Adjust Network** for the target instance.
![](https://main.qcloudimg.com/raw/aef059daeec7e0094375874239f044ee.png)
Adjust the bandwidth upper limit to an appropriate value to ensure that the bandwidth of the CVM instance is greater than 0.

3. Click the ID of the CVM instance to enter its basic information page and switch to the ENI tab.
![](https://main.qcloudimg.com/raw/04a0956edc818210b2069607d5a675a1.png)
![](https://main.qcloudimg.com/raw/cbc735040d7134e3f4027de39f764a2f.png)
4. Click **Bind** to bind an existing EIP to the current CVM instance or create an EIP for binding.
![](https://main.qcloudimg.com/raw/77f7d3d97919e23ed604bae0c3ccb08e.png)
After binding the EIP, in the ENI tab, you can see that there is EIP information in the "Bound Public IP" section of the primary ENI.
![](https://main.qcloudimg.com/raw/f8d83f9aade43573c9720dabc231144a.png)
5. Check whether the CVM instance can be accessed over the public network.
You can use the `ping` or `ssh` command to check whether the EIP has taken effect. **Make sure that the inbound rules of the security group allow ICMP and port 22**.
6. Access the native WebUIs of components.
EMR v1.3.1, v2.0.1, v2.1.0, and v3.00 support Apache Knox, and access requests to native component WebUIs over the public network will pass through Knox by default. For specific UI links to each component and Knox usage, please see [Knox Development Guide](https://intl.cloud.tencent.com/document/product/1026/31167).

>After an EIP is bound, the access addresses of native component WebUIs in the EMR Console will stay unchanged. If you need to change the addresses in the console, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
