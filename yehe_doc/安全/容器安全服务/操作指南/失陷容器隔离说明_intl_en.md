In case of container attacks in the business environment, such as container escape, viruses, trojans, infectious worms, horizontal detection or attacks by compromised containers, or malicious container pull by attackers due to cluster/node vulnerabilities or improper configuration, you need to quickly isolate the container network.
>? As isolating the container network may affect normal business operations, we recommend you first confirm that the container is risky and isolation is necessary to avoid intrusions.

## Isolating the Container Network
You can use the container network isolation feature on the [Runtime Security](https://console.cloud.tencent.com/tcss/runtime/containerEscape), [Advanced Prevention](https://console.cloud.tencent.com/tcss/defend/processDetection), or [Asset Management](https://console.cloud.tencent.com/tcss/asset) page. The effect may differ by module as shown below:
<table>
<thead>
<tr>
<th>Module Name</th>
<th>Feature Details</th>
</tr>
</thead>
<tbody><tr>
<td>Container escape</td>
<td rowspan=5>If the container is isolated successfully in case of a security event, the system will disconnect the container from the network and mark the security event as processed.</td>
</tr>
<tr>
<td>Reverse shell</td>
 </tr>
<tr>
<td>Abnormal process</td>
 </tr>
<tr>
<td>File tampering</td>
 </tr>
<tr>
<td>High-risk syscall</td>
 </tr>
<tr>
<td>Virus scanning</td>
<td>Isolating the container alone cannot eliminate virus or trojan risks. Therefore, after the container is isolated successfully in case of a security event, the system will disconnect the container from the network but will not mark the security event as processed. To change the event status, you need to have the viruses or trojans in the container automatically isolated or isolate them manually.</td>
</tr>
</tbody></table>

#### Runtime security or advanced prevention
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Runtime Security** > **Container Escape** on the left sidebar.
2. On the **Container Escape** page, select the target container and click **Process** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/4bc22a0bbe96e54ad9d9eedfe4c46a43.png) 
3. Select **Isolate the container**, enter the remarks, and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0e70c8951f642f6aa74a291c9bdc66ad.png" style="zoom:50%;" />

#### Asset management
1. On the [**Asset Management**](https://console.cloud.tencent.com/tcss/asset) page, click **Container**.
2. On the **Container** page, select the target container and click **Isolate the container**.
![](https://qcloudimg.tencent-cloud.cn/raw/c89dd6e5e2d25d32efd6f9f5077ef47c.png)
3. In the pop-up window, click **OK**.
>! If the container is isolated, it will be disconnected from the network.

## Canceling Isolation of the Container Network
To recover the container network after processing the risks in the container, click **More** > **Cancel isolation** in the security event list on the [**Runtime Security**](https://console.cloud.tencent.com/tcss/runtime/containerEscape) or [**Advanced Prevention**](https://console.cloud.tencent.com/tcss/defend/processDetection) page, or click [**Asset Management**](https://console.cloud.tencent.com/tcss/asset) > **Container**, select the target container, and click **Cancel isolation**.
![](https://qcloudimg.tencent-cloud.cn/raw/ffad9a8da1b349aee8513f039461b66f.png)

## Viewing the Container Isolation Status
The container isolation status is refreshed as one of the container asset attributes on the [**Runtime Security**](https://console.cloud.tencent.com/tcss/runtime/containerEscape), [**Advanced Prevention**](https://console.cloud.tencent.com/tcss/defend/processDetection), or [**Asset Management**](https://console.cloud.tencent.com/tcss/asset) page. For example, if you successfully isolate the container network in the security event list on the **Runtime Security** > **Container Escape** page, you can see that the container is in the **Isolated** status in the list on the **Asset Management** > **Container** page. Similarly, if you isolate the container network in the list on the **Asset Management** > **Container** page, the status will be refreshed in the list on the **Runtime Security** or **Advanced Prevention** page.

You can click the container isolation status drop-down list above the list to filter container events.
![](https://qcloudimg.tencent-cloud.cn/raw/622337f1883170df1ac200869e60608c.png)