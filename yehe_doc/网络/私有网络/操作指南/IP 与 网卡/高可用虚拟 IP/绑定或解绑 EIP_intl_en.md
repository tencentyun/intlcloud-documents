Similar to a private IP, HAVIP binding can also be configured in the console. Binding a HAVIP refers to EIP operations. You can skip this section if no public network connection is needed.

## Binding an EIP
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and select **IP and Interface** > **HAVIP** on the left sidebar. 
2. Select the target region on the HAVIP management page.
3. Select the HAVIP to be bound with EIP, and click **Bind** under the **Operation** column.
    ![](https://main.qcloudimg.com/raw/8ff34853fe60fa3ec2d9010df1bd3bbf.png)
4. In the pop-up dialog box, select an EIP to be bound.
    >!
    >+ An HAVIP can only be bound with one EIP.  If no EIP is available, you must first create an EIP in the console.
    >+ If the HAVIP is not bounded with a CVM instance, the corresponding EIP will be in idle status and will incur an idle fee. Please configure the HAVIP correctly and bind it to an instance by referring to the following cases:
    >  + [Building High Availability Primary/Secondary Cluster by Using HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) under Best Practice
    >  + [Creating a High-availability Database by Using HAVIP + Windows Server Failover Cluster](https://intl.cloud.tencent.com/document/product/215/31878) under Best Practice 
5. Click **OK**.
     ![](https://main.qcloudimg.com/raw/7b96dd411d694326603aac3035e75329.png)

## Unbinding an EIP
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and select **IP and Interface** > **HAVIP** on the left sidebar. 
2. Select the target region on the HAVIP management page.
3. Select the HAVIP from which EIP will be unbound, and click **Unbind** under the **Operation** column.
4. In the pop-up dialog box, read the notes, and click **OK** to unbind the EIP.
   >!
   >+ Your public network business may be affected after unbinding the EIP. Please get ready in advance.
   >+ After being unbound, the EIP will be idle and incur an idle fee. You can directly release unused EIPs to avoid costs.
   >
 <img src="https://main.qcloudimg.com/raw/dfaef505c93aa5c72e1b23e9516a9cec.png" width="50%" />
