### What is the difference between SSH key login and password login?
An SSH key allows you to log in to a Linux server remotely. It uses the key generator to create a key pair (public and private). The public key is added to the server, and the client can use the private key to complete the authentication and login. Compared to password login, SSH key login is more secure and efficient.
Currently, Linux instance supports both password and SSH key login, while Windows instance only supports password login. For related documentation, see:
- [Logging in to Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436)
- [Logging in to Windows Instance](https://intl.cloud.tencent.com/document/product/213/5435)

### I cannot use the password to log in to a Linux instance that is associated with an SSH key.
After the CVM is associated with an SSH key, password login is **disabled by default**. See [Logging in to Linux Instance (SSH Key)](https://intl.cloud.tencent.com/document/product/213/32501). 

### Can I use SSH key together with the password login?
When you [log in to Linux instance via SSH key](https://intl.cloud.tencent.com/document/product/213/32501), password login is disabled by default to improve security.

### How do I create an SSH key and what if I lose it?
For more information on key creation, see [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).
If you lost the key, troubleshoot by the following methods:
 - Create a new key via [SSH Key](https://console.cloud.tencent.com/cvm/sshkey) on the console and bind it with the original instance.
  1. [Create an SSH key](https://intl.cloud.tencent.com/document/product/213/16691).
  2. After the key is successfully created, log in to the [CVM Console](https://console.cloud.tencent.com/cvm).
  3. Select the original instance with which you want to bind the key, click **More** -> **Password/key** -> **Load a key**. You can then use the new key to log in to the instance.
 - Reset your password through the CVM Console and log in to the instance with your new password. For more information, see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).

### How do I bind/unbind an SSH key to or from the server?

For more information, see the **Binding/Unbinding a key to or from a CVM** section in [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).

### How do I modify the SSH key name/description?

For more information, see the **Modifying the SSH key name and description** section in [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).

### How do I delete an SSH key?

For more information, see the **Deleting SSH keys** section in [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).

### What are the use limits on SSH keys?

For more information, see the **Use Limits** section in [SSH Keys](https://intl.cloud.tencent.com/document/product/213/6092).

### How to troubleshoot if I fail to log in to a Linux instance using an SSH key?

For more information, see [Unable to Log in to a Linux Instance via SSH](https://intl.cloud.tencent.com/document/product/213/32486).

### I can not download my key.
The key can only be downloaded once. If you lost the key, we recommend that you create a new key, download and save it.

### How can I query which key is used by the CVM instance?
You can log in to the CVM Console and go to the instance details page to view keys used by the CVM.
