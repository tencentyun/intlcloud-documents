### What is the difference between SSH key login and password login?
An SSH key allows you to log into Linux server remotely. It uses the key generator to create a key pair (public and private). The public key is added to the server, and then the user can use the private key to complete the authentication and login. This method focuses on data security and is more convenient than the manual input of the traditional password login method.
Currently, Linux instance supports both password and SSH key login, while Windows instance supports only password login. For related documentation, see:
- [Log in to Linux Instance](https://intl.cloud.tencent.com/document/product/213/16515)
- [Log in to Windows Instance](https://intl.cloud.tencent.com/document/product/213/35697)

### Can I use SSH key and password logins at the same time?
When you [log into Linux instance via SSH key](https://intl.cloud.tencent.com/document/product/213/32501), password login is disabled by default to improve security.

### What should I do if I forget my password?
You can reset the password. For details, see [Reset Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).

### How do I create an SSH key and what if I lose it?
For more formation on key creation, please see [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).
If you lose the key, resolve by the following two methods:
 - Create a new key through [SSH Key](https://console.cloud.tencent.com/cvm/sshkey) on the console and bind it with the original instance.
  1. [Create an SSH key](https://intl.cloud.tencent.com/document/product/213/16691).
  2. After the key is successfully created, log in to the [CVM Console](https://console.cloud.tencent.com/cvm).
  3. Select the original instance with which you want to bind the key, click **More** > **Password/key** **Load a key**. Then you can use the new key to log into the instance.
 - Reset your password through the CVM console and log into the instance with your new password. For details, see [Reset Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).

### How do I bind/unbind an SSH key to or from the server?

Please see the **Binding/Unbinding a key to or from a CVM** section in [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).

### How do I modify the SSH key name/description?

Please see the **Modifying the SSH key name and description** section in [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).

### How do I delete an SSH key?

Please see the **Deleting SSH keys** section in the [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).

### What are the use limits on SSH keys?

Please see the **Use Limits** section in [SSH Key](https://intl.cloud.tencent.com/document/product/213/6092).

### How to troubleshoot if I fail to log into a Linux instance using an SSH key?

Please see [Unable to Log into a Linux Instance via SSH](https://intl.cloud.tencent.com/document/product/213/32486).
