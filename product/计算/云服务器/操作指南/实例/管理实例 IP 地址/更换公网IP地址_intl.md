## Scenario

This guide introduces how to change public IP. There are two different ways:
- Change public IP directly
- First change to Elastic Public IP, and then unbind Elastic Public IP

> **Note:**
If you change IP directly:
- No more than 3 times/day per account per region.
- One instance can only change IP once.
- The previous IP will be released.

If you first change to Elastic Public IP and then unbind it:
- When Elastic IP is bound with an instance, the current public IP will be released.
- Elastic Public IP quota per account per region is 20.
- Release the unbound EIP as soon as possible if you no longer use it. Otherwise, you will be billed for the idle EIP. The released EIP cannot be retrieved. 

## Directions
### Change public IP directly
1. For an instance, click **More** > **IP/ENI** > **Change Public IP**.
2. Click **Confirm**

### First change to Elastic Public IP, and then unbind Elastic Public IP
#### Binding an EIP
1. Log in to Tencent Cloud, enter the CVM [management page](https://console.cloud.tencent.com/cvm/index) of the CVM console, and click **More** -> **IP/ENI** -> **Bind EIP**.
![](https://main.qcloudimg.com/raw/9f6b1d1bcb3019e156ca0fc8fb4fde5b.png)
2. After confirming the information in the pop-up box, click **Confirm**.
![](https://main.qcloudimg.com/raw/24b34243fa471ef3e0cab6e40ea3e578.png)
3. The EIP converted successfully is shown as below:
![](https://main.qcloudimg.com/raw/e1d0d72e2b7eff6d1fab88042a3f6bf5.png)

> **Note:**
> It is recommended to bind the applied EIP with the CVM immediately. Otherwise, you will be billed for the idle EIP.

#### Unbinding EIP
1. To convert the EIP back to public network IP, click **More** -> **IP/ENI** -> **Unbind EIP**.
![](https://main.qcloudimg.com/raw/15575487bdf6dbb15e9b5c0ff9daa22a.png)
2. In the pop-up box, select **A free public IP will be assigned after unbinding**, and click **OK** to unbind the EIP.
![](https://main.qcloudimg.com/raw/c36e36a4ebe4a26449e131b48019e410.png)

#### Releasing EIP
1. Click **Elastic Public IP** on the navigation bar on the left side to go to the Elastic Public IP Management page. Select the target EIP, and click **Release** in the Action column.
![](https://main.qcloudimg.com/raw/310d3c5afd4c2eb74a7c3b0da38720e2.png)
2. Confirm the information in the pop-up box, and click **OK** to release the EIP.
![](https://main.qcloudimg.com/raw/1c62aa1e8ac3aeb561dee393a97ae093.png)
