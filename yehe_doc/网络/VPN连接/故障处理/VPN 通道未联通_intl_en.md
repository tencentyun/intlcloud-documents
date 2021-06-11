

## Error description
A VPN connection is used to connect VPC to IDC, but the status of VPN tunnel is **Unconnected** after the configuration.
![](https://main.qcloudimg.com/raw/d37bb0a17e5b7ab17db816872ff5dfa5.png)

## Possible causes
An exception in tunnel status usually results from the following factors:
+ No traffic to activate the tunnel
+ The VPN gateway public IP is not connected
+ The security policy is not correctly configured
+ Inconsistent negotiation parameters and modes

## Solutions
1. Log in to a CVM in the VPC and activate the tunnel by using the ping command to test the network connectivity of the private IP of the server on the customer IDC side.
>?To log in to the CVM in the VPC, please see [Logging in to Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436) or [Logging in to a Windows Instance](https://intl.cloud.tencent.com/document/product/213/5435).
>
    - A successful ping indicates that the tunnel is activated. Check if the status of the VPN tunnel is “Connected”. If so, the problem is solved.
    - In case of a ping failure, please directly go to [Step 2](#step2).
2. <span id="step2"></span>Log in to the VPN device on the IDC side and use the ping command to test the network connectivity of the VPN gateway public IP on the Tencent Cloud side (suppose the VPN gateway public IP is 139.186.120.129) to see if the ping is successful or not.
    - If it is, please go to [Step 4](##step4).
    - If not, please go to [Step 3](#step3).
		![](https://main.qcloudimg.com/raw/8202c85bf541bcd3df296b72ce177a3a.png)
3. <span id="step3"></span>Check the connection status of the public network on the IDC side and see whether it can be connected to the Internet.
    - If it is, please go to [Step 4](#step4).
    -. If not, please check whether the VPN tunnel is connected after repairing the local network. If it is connected, the problem is solved. If not, please go to [Step 4](#step4).
4. <span id="step4"></span>Check the security policy of the VPN device on the IDC side, and whether the public IP address of the VPN gateway on the Tencent Cloud side and the private IP address are open to Internet.
```plaintext
display current-configuration configuration security-policy      //Take Huawei Firewall as an example here
```
  - If it is, please go to [Step 5](#step5).
  - If not, please modify the security policy and make the VPN gateway IP on the Tencent Cloud side and the corresponding SPD policy open to Internet. Then, check whether the VPN tunnel is connected. If so, the problem is solved. If not, please go to [Step 5](#step5).
5. <span id="step5"></span>Check whether the negotiation parameters (including IKE and IPsec configurations) and negotiation modes (main/aggressive mode) of the VPN gateway on the Tencent Cloud side and the VPN device in the customer IDC are consistent.
>!
>- Inconsistency in any parameter can cause the failure to create a VPN tunnel.
>- The default VPN configuration varies by devices and public cloud service providers.
>
 Go to the [VPN tunnel console](https://console.cloud.tencent.com/vpc/vpnConn?rid=17). Click the instance ID to enter the details page, and check the consistency on the “Advanced Configuration” tab.
   ![](https://main.qcloudimg.com/raw/003f674d04966acebd7b713a64743609.png)
	 Device configuration parameters on the IDC side can be obtained through the following command. Take Huawei Firewall as an example here.
	  ```plaintext
display current-configuration configuration ike profile
display current-configuration configuration ipsec  policy
    ```
   - If they are consistent, please go to [Step 6](#step6).
   - If not, please modify corresponding parameters on both sides to ensure the consistency. Then, check whether the VPN tunnel is connected. If so, the problem is solved. If not, please go to [Step 6](#step6).
6. <span id="step6"></span>Collect the troubleshooting information above and [submit a ticket](https://console.cloud.tencent.com/workorder/category) or ask the device manufacturer for help.

