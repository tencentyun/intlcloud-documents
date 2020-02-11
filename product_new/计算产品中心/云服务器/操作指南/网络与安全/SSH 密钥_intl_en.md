## Scenario
The password is an exclusive login credential for every CVM. To ensure the reliability and security of an instance, Tencent Cloud provides the following two login methods:
- [Password Login](https://intl.cloud.tencent.com/document/product/213/6093)
- SSH key pair login

This document describes common operations in using SSH key pair to log in to an instance.

## Steps

<span id="creatSSH"></span>
### Creating SSH keys
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, click **Create a key**.
 4. In the pop-up **Create SSH key** window, select the method for creating a key, enter the information, and click **OK**.
  - If you select **Create a new key pair**, enter the key name.
  - If you select **Use an existing public key**, enter the key name and the original public key information.
 5. In the prompt box that pops up, click **Download** to download the private key.
 > Tencent Cloud does not save your private key information. Download and obtain the private key within 10 minutes.
 > 

<span id="bindingSSH"></span>
### Binding/unbinding a key to or from a CVM
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, select the SSH key of the CVM to be bound or unbound and click **Bind/Unbind Instance**.
 4. In the **Bind/unbind Instance** window that pops up, select the region and the CVM to be bound or unbound, and click **OK**.


### Modifying the SSH key name and description
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, select the key to be modified, and click **Modify**.
 4. In the **Modify a key** window that pops up, enter the new key name and key description, and click **OK**.

### Deleting SSH keys
> If the SSH key is associated with a CVM or a custom image, it cannot be deleted.
>
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, select all SSH keys that need to be deleted, and click **Delete**.
 4. In the **Delete Key** window that pops up, click **OK**.

### Using an SSH key to log in to a Linux CVM

1. [Create an SSH key](#creatSSH).
2. [Bind an SSH key to a CVM](#bindingSSH).
3. [Logging into Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501).
