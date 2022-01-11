## Overview
This document describes common operations related to using SSH key pair to log in to an instance. For example, you can create, bind, unbind, modify, or delete a SSH key pair.
>!To bind an SSH key to or unbind it from an instance, please shut down the instance first. See [Shutdown Instances](https://intl.cloud.tencent.com/document/product/213/4929).
>

## Directions

<span id="creatSSH"></span>
### Creating a SSH key
 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
 2. Click **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)** on the left sidebar.
 3. Click **New** on the **SSH Key**page.
 >! After clicking **OK**, the private key will be automatically downloaded. Tencent Cloud will not retain your private key. Be sure to keep it safe.
 > 
![](https://main.qcloudimg.com/raw/a6675ade459e6bf236ff7301995a35f2.png)
  - If you select **Create a new key pair**, enter the key name.
  - If you select **Use an existing public key**, enter the key name and the original public key information.


<span id="bindingSSH"></span>
### Binding a key to instance
 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
 2. Click **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)** on the left sidebar.
 3. On the SSH key management page, select the target SSH key, and click **Bind with instances**.
![](https://main.qcloudimg.com/raw/7419df720863aa9463e0dcf478580bbd.png)
 4. In the pop-up window, select the target region and instances, and click **Bind**.


### Unbinding a key from instance
 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
 2. Click **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)** on the left sidebar.
 3. On the SSH key management page, select the target SSH key, and click **Unbind from instances**.
![](https://main.qcloudimg.com/raw/263f344c4bea3cdff4e422996821cb5d.png)
 4. In the pop-up window, select the region and instances to unbind from the key, and click **Unbind**.


### Modifying the SSH key name or description
 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
 2. Click **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)** on the left sidebar.
 3. On the SSH key management page, select the key to be modified and click <img  style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/9db81482f9242417d94a04f314b42b19.png"/> next to the key name, as shown below.
![](https://main.qcloudimg.com/raw/e4c46354bafa78daa7efa24064eafea9.png)
 4. In the pop-up window, enter the new key name or description, and click **OK**.

### Deleting SSH keys
>! An SSH key cannot be deleted when it is bound with CVM instances or custom images,  cannot be deleted.
>
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. Click **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)** on the left sidebar. You can delete a single or multiple SSH keys as needed.
 - **Deleting a single key**
    1. On the SSH key management page, select the SSH key to be deleted, and click **Delete** under the **Operation** column, as shown below.
![](https://main.qcloudimg.com/raw/96d57d5beb3d73c0978cc1464bc73c7e.png)
    2. In the pop-up window, click **OK**.
 - **Batch deleting keys**
    1. On the SSH key management page, select SSH keys to be deleted, and click **Delete** above the list to batch delete them.
    2. In the pop-up window, click **OK**, as shown below.
    Only deletable ones of the selected key pairs will be deleted.
		![](https://main.qcloudimg.com/raw/bfcdfb401f8906834b02372d3e50dbe0.png)


### Using a SSH key to log in to a Linux CVM

1. [Create a SSH key](#creatSSH).
2. [Bind a SSH key to a CVM instance](#bindingSSH).
3. [Log in to a Linux instance via SSH key](https://intl.cloud.tencent.com/document/product/213/32501).
