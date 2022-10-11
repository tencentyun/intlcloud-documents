## Use Cases
When you want to access internet via an EIP, you can choose NAT mode or direct connection mode. The default mode is NAT mode.
- In NAT mode, EIP is invisible on the local machine.
- In direct connection mode, the EIP is visible on the local machine. You do not need to manually add an EIP address for each configuration, which can minimize development cost.
- NAT mode can meet most of the requirements. However, if you want to check the public IP on the CVM, you need to use EIP direct connection mode.

## Use Limits
- At present, EIP direct connection is under beta test and is only available to allowed users. It only supports devices in a VPC. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for this feature.
- An NAT gateway can be bound with EIPs that are enabled with direct connection, but direct connection cannot be implemented.
- On CVM, EIP direct connection cannot take effect at the same time as an NAT gateway. If the routing table associated with the subnet where your CVM resides is configured with a routing policy of accessing the public network through the NAT gateway, direct connection cannot be implemented through the EIP on the CVM. You can allow the CVM to access the public network through its EIP by [adjusting the priorities of NAT gateways and EIPs](https://intl.cloud.tencent.com/document/product/1015/32734). In this case, EIP direct connection can be implemented.

## Directions
To use EIP direct connection, you need to enable it in the console and add the IP to the ENI in the operating system. You also need to configure the routing in the operating system based on your application. Therefore, we provide a script for configuring the IP so that private network traffic goes through the private IP and public network traffic goes through the public IP.
>For other applications, configure the routing accordingly.
>
### Configuring EIP direct connection on Linux CVM
>
>- The script for Linux supports CentOS 6 and later, and Ubuntu.
>- The script for Linux supports only primary ENI (eth0) and does not support secondary ENI.
>- If the public IP that is bound to the primary ENI is not an EIP, you need to convert the public IP to an EIP. For more information, see [Converting public IP to EIP](https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip).

#### Scenario
The script for Linux is applicable to the following scenario: both the private IP and public IP are bound to the primary ENI (eth0), where the public network address is accessed through the public IP, and the private network address is accessed through the private IP.

#### Step 1: download the script for EIP direct connection
EIP direct connection may cause network interruption. Therefore, you need to download the script for EIP direct connection and upload it to CVM in advance. You can obtain the script by using one of the following methods:
- **Method 1: upload the script for EIP direct connection**
 (1) Download the configuration script for EIP direct connection from Download Script for Linux
 (2) After the script for Linux is downloaded onto the local machine, upload it to the CVM that requires EIP direct connection.
- **Method 2: directly use a command**
Log in to the CVM, and run the following command on the CVM to download the script:
```
wget https://network-data-1255486055.cos.ap-guangzhou.myqcloud.com/eip_direct.sh
```

#### Step 2: run the script for EIP direct connection
1. Log in to the CVM that requires EIP direct connection.
2. Run the script for EIP direct connection as follows:
 (1) Run the following command to add the execution permission:
```
chmod +x eip_direct.sh
```
 (2) Run the following command to run the script:
```
./eip_direct.sh install XX.XX.XX.XX
```
Here, XX.XX.XX.XX indicates the EIP address (optional). You may leave it blank and run `./eip_direct.sh install` directly.

#### Step 3: enable EIP direct connection
1. Log in to the [EIP Console](https://console.cloud.tencent.com/cvm/eip?rid=1).
2. Find the target EIP, and choose **More** -> **Direct connection** in the **Operation** column on the right.


### Configuring EIP direct connection on Windows CVM
>
>- To use EIP direct connection in Windows, you need one ENI for private IP and one ENI for public IP, and bind the public IP to the primary ENI and bind the private IP to the secondary ENI.
>- During configuration of EIP direct connection in Windows, your internet connection may be interrupted. Therefore, we recommend that you [log in to a Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
- If the public IP that is bound to the primary ENI is not an EIP, you need to convert the public IP to an EIP. For more information, see [Converting public IP to EIP](https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip).

#### Scenarios
The script for Windows is applicable to the following scenario: Public network traffic goes through the primary ENI, and private network traffic goes through the secondary ENI.

#### Step 1: download the script for EIP direct connection<span id="step1" />
During configuration of EIP direct connection, the internet connection will be interrupted. Therefore, you need to download the script for EIP direct connection and upload it to CVM in advance.
Open the following link in the browser of the CVM to download the script for EIP direct connection:
```
https://windows-1254277469.cos.ap-guangzhou.myqcloud.com/eip_windows_direct.bat
```

#### Step 2: configure the secondary ENI
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/overview).
2. On the **Instances** page, click the configured CVM ID to go to the **Basic Information** page.
3. Select the **ENI** tab and click **Bind ENI** to create an ENI that is in the same subnet as the primary ENI.
![](https://main.qcloudimg.com/raw/2da530f15e824ff99858f08397687cf6.png)
4. In the pop-up window, select **Create and Bind an ENI**, enter the information, select **Automatic Assignment** in **Assign IP** section and click **OK**.
![](https://main.qcloudimg.com/raw/cb6fe49d3bbefd792355ade6e62f29f3.png)

#### Step 3: configure EIP direct connection for the primary ENI
1. Log in to the [EIP Console](https://console.cloud.tencent.com/cvm/eip?rid=1).
2. Find the EIP that is bound to the primary ENI and choose **More** -> **Direct Connection** in the **Operation** column on the right.

#### Step 4: configure IP in CVM
1. Log in to the CVM. This operation may cause public network interruption. Therefore, you need to [Log in to a Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. On the operating system page, select <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;width:25px"> in the lower-left corner and click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: -3px 0px;"> to open the **Windows PowerShell** window. Enter `firewall.cpl` and press Enter to open the **Windows Firewall** page.
3. Click **Turn Windows Firewall on or off** to go to the **Customize Settings** page.
![](https://main.qcloudimg.com/raw/e6d6a44be911ec5f60a6205b6f47a2c7.png)
4. Select **Turn off Windows Firewall** both in the **Private network settings** pane and the **Public network settings** pane.
![](https://main.qcloudimg.com/raw/cdb7703dec781e98101f7f3fd7ecf71f.png)
5. Double-click to run the script downloaded in [Step 1](#step1). Enter the public IP address and press Enter twice.
6. Enter `ipconfig` in the **Windows PowerShell** window and press Enter. You can see that the IPv4 address on the primary ENI changes to the public network address.

>When the direct connection is enabled, you cannot assign a private IP to the primary ENI. Otherwise, the CVM cannot access the public network.
