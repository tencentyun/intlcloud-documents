## Scenario
The password is the exclusive login credential for every CVM. In order to ensure the reliable security of an instance, Tencent Cloud provides the following two login methods:
- [Password login](https://intl.cloud.tencent.com/document/product/213/6093)
- SSH key pair login

This document introduces the common operations related to using SSH key pair to log in to an instance.

## Steps

<span id="creatSSH"></span>
### Creating SSH Keys
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, click **Create Key**.
 4. In the pop-up **Create SSH Key** window, select the method for creating a key, enter the related information, and click **Confirm**.
  - If you selected **Create a new key pair**, enter the key name.
  - If you selected **Use an existing public key**, enter the key name and the original public key information.
 4. In the prompt box that pops up, click **Download** to download the private key.
 >! Tencent Cloud does not save your private key information. Download and obtain the private key within 10 minutes.
 > 

<span id="bindingSSH"></span>
### Binding/Unbinding a Key to or from a CVM
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, select the SSH key of the CVM to be bound or unbound and click **Bind/Unbind Instance**.
 4. In the **Bind/Unbind Instance** window that pops up, select the region and the CVM to be bound or unbound, and click **Confirm**.


### Modifying the SSH Key Name and Description
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, select the key to be modified, and click **Modify**.
 4. In the **Modify Key** window that pops up, enter the new key name and key description, and click **Confirm**.

### Deleting SSH Keys
> If the SSH key is associated with a CVM or a custom image, it cannot be deleted.
>
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[SSH key](https://console.cloud.tencent.com/cvm/sshkey)**.
 3. In the SSH key management page, select all the SSH keys that need to be deleted, and click **Delete**.
 4. In the **Delete Key** window that pops up, click **OK**.

### Using an SSH Key to Log in to a Linux CVM

1. [Create an SSH Key](#creatSSH).
2. [Bind an SSH Key to a CVM](#bindingSSH).
3. [Use SSH to Log in to a Linux Instance](https://intl.cloud.tencent.com/document/product/213/32501).
