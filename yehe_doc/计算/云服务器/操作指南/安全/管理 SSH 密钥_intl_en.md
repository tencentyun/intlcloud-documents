## Scenario
The password is a unique login credential for each CVM instance. To ensure the security of an instance, Tencent Cloud provides the following two login methods:
- [Password Login](https://intl.cloud.tencent.com/document/product/213/6093)
- SSH key pair login

This document describes common operations related to using SSH key pair to log in to an instance.

## Directions

<span id="creatSSH"></span>
### Creating SSH keys
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, click **Create a key**.
 4. In the **Create an SSH key** window that pops up, select how you will create the key, enter the related information, and click **OK**.
  - If you select **Create a new key pair**, enter the key name.
  - If you select **Use an existing public key**, enter the key name and the original public key information.
 5. In the prompt box that pops up, click **Download** to download the private key.
 > Tencent Cloud does not save your private key information. Download and obtain the private key within 10 minutes.
 > 

<span id="bindingSSH"></span>
### Binding/Unbinding a key to or from a CVM
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, select the SSH key of the CVM to be bound or unbound, and click **Bind/unbind Instance**.
 4. In the **Bind/unbind Instance** window that pops up, select the region and the CVM to be bound or unbound, and click **OK**.


### Modifying the SSH key name and description
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, select the key to be modified, and click **Modify**.
 4. In the **Modify a key** window that pops up, enter the new key name and description, and click **OK**.

### Deleting SSH keys
> If the SSH key is associated with a CVM or a custom image, it cannot be deleted.
>
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, select all SSH keys to be deleted, and click **Delete**.
 4. In the **Delete key** window that pops up, click **OK**.

### Using an SSH key to log in to a Linux CVM

1. [Create an SSH key](#creatSSH).
2. [Bind an SSH key to a CVM](#bindingSSH).
3. [Log in to a Linux instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501).
