## Scenario
Elastic IP, or ElP, is a static IP designed for dynamic cloud computing and a fixed public IP in a certain region. With EIP, you can quickly remap an address to another instance in your account or NAT gateway instance to avoid instance failure. This document describes how to use EIPs.

## Prerequisites

You have logged in to the [CVM Console](https://console.cloud.tencent.com/cvm).

## Directions

### Apply for EIPs 

1. In the left sidebar, click **[Public IP](https://console.tencentcloud.com/cvm/ip)** to enter the EIP management page.
2. Click **Apply** in the EIP management page.
3. In the pop-up “Apply for EIP” window, select the region, IP address type, billing method and bandwidth limit, and enter the number of EIPs you want to apply for.
4. Click **OK** to complete the EIP application.
5. After the application is completed, you can see in the list the EIP you have applied for, which is in an unbound status.

<span id = "jump2">  </span>
### Bind EIPs to cloud products

1. In the left sidebar, click **[Public IP](https://console.tencentcloud.com/cvm/ip)** to enter the EIP management page.
2. In the EIP management page, select the EIP which you want to bind to a cloud product and click **More** > **Bind**.
<dx-alert infotype="notice" title="">
 If the EIP has been bound to a instance, please unbind it first.
</dx-alert>
3. In the pop-up “Bind resources” window, select the resource to be bound to the EIP and click **OK**.
4. In the pop-up window, click **OK** to complete binding the EIP to the cloud product.

### Unbind EIPs from cloud products

1. In the left sidebar, click **[Public IP](https://console.tencentcloud.com/cvm/ip)** to enter the EIP management page.
2. In the EIP management page, select the EIP which you want to unbind from the cloud product and click **More** > **Unbind**.
3. In the pop-up “Unbind EIP” window, confirm the unbinding information and click **OK**.
4. In the pop-up window, click **OK** to complete unbinding the EIP from the cloud product.
<dx-alert infotype="notice" title="">
 After unbinding, the cloud product instance may be assigned a new public IP, which may be different from the one before binding.
</dx-alert>

<span id = "jump">  </span>
### Release EIPs

1. In the left sidebar, click **[Public IP](https://console.tencentcloud.com/cvm/ip)** to enter the EIP management page.
2. In the EIP management page, select the EIP which you want to release from the cloud product and click **More** > **Release**.
3. In the pop-up “Are you sure you want to release the selected EIPs?” window, select **Release the above EIPs** and click **Release**.

### Adjust Bandwidth
1. In the left sidebar, click **[Public IP](https://console.tencentcloud.com/cvm/ip)** to enter the EIP management page.
2. Select the EIP whose bandwidth needs to be adjusted and click **Adjust network**
3. In the pop-up “Change bandwidth” window, configure the bandwidth value and click **OK** to complete the adjustment.

### Convert a public IP to an EIP
The public IP purchased along with the CVM instance is not elastic and cannot be mounted or unmounted. Tencent Cloud allows you to convert the public IP to an EIP by the following steps:
1. In the left sidebar, click **[Instances](https://console.cloud.tencent.com/cvm/index)** to enter the instance management page.
2. Select the instance whose public IP needs to be converted to an EIP and then click <img src="https://main.qcloudimg.com/raw/25e8c0e37b73c12da900301f03e57dbc.png" style="margin: 0;"></img>, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/dac8677bd2b48e99f6b99a5d351ec21e.png)
3. In the pop-up “Convert to EIP” window, click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/4f6a6e6b93afa784983a7d67de80ff67.png)

## Troubleshoot Exceptions
Network inaccessibility may occur with an EIP due to the following reasons: 
- The EIP is not bound to any cloud product. For more information about how to bind an EIP to the cloud product, please see [Bind EIPs to cloud products](#jump2).
- Security policy is invalid. Check if there is a valid security policy (security group or network ACL). If the bound cloud product has a security group policy, such as access to 8080 port is denied, the port 8080 of the EIP is also inaccessible.
