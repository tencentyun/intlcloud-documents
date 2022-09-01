## Overview
This document describes common operations related to using SSH key pair to log in to an instance. For example, you can create, bind, unbind, modify, or delete an SSH key pair.


<dx-alert infotype="notice" title="">
An SSH key can only be bound to or unbound from a CVM instance that is shut down. For directions on how to shut down a CVM instance, see [Shutting Down Instances](https://intl.cloud.tencent.com/document/product/213/4929).
</dx-alert>



## Directions

### Creating an SSH key[](id:creatSSH)
1. Log in to the CVM console and select **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)** on the left sidebar.
2. On the **SSH Key** page, click **New**.
3. In the **Create an SSH key** pop-up window, configure the key.
![](https://main.qcloudimg.com/raw/a6675ade459e6bf236ff7301995a35f2.png)
 - **Creation Method**:
    - If you select **Create a key pair**, enter the key name.
    - If you select **Use an existing public key**, enter the key name and existing public key information.
    <dx-alert infotype="notice" title="">
    You need to use a public key without a password; otherwise, you cannot log in to the instance in the console.
    </dx-alert>
 - **Key Name**: Customize a name.
 - **Tag (Optional)**: You can add tags for a key as needed, which can be used to categorize, search for, and aggregate resources. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/651/13334).
4. Click **OK**.
<dx-alert infotype="notice" title="">
After clicking **OK**, the private key will be automatically downloaded. Tencent Cloud will not retain your private key. Be sure to keep it safe.
</dx-alert>




### Binding a key to an instance[](id:bindingSSH)
1. Log in to the CVM console and select **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)** on the left sidebar.
2. On the **SSH Key** page, click **Bind instance** in the row of the target key.
![](https://main.qcloudimg.com/raw/7419df720863aa9463e0dcf478580bbd.png)
3. In the pop-up window, select the **Region** and target CVM instance, and click **Bind**.


### Unbinding a key from an instance
1. Log in to the CVM console and select **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)** on the left sidebar.
2. On the **SSH Key** page, click **Unbind instance** in the row of the target key.
![](https://main.qcloudimg.com/raw/263f344c4bea3cdff4e422996821cb5d.png)
3. In the pop-up window, select the **Region** and target CVM instance, and click **Unbind**.


### Modifying the SSH key name or description
1. Log in to the CVM console and select **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)** on the left sidebar.
2. On the **SSH Key** page, select <img  style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/9db81482f9242417d94a04f314b42b19.png"/> on the right of the key name.
![](https://main.qcloudimg.com/raw/e4c46354bafa78daa7efa24064eafea9.png)
3. In the pop-up window, enter the new key name or description, and click **OK**.


### Deleting an SSH key

<dx-alert infotype="notice" title="">
An SSH key that is bound to a CVM instance or custom image cannot be deleted.
</dx-alert>


1. Log in to the CVM console and select **[SSH Key](https://console.cloud.tencent.com/cvm/sshkey)** on the left sidebar.
2. On the **SSH Key** page, delete one key or batch delete keys as needed.
   <dx-tabs>
   ::: Deleting one key
    1. Click **Delete** in the row of the target SSH key.
   ![](https://main.qcloudimg.com/raw/96d57d5beb3d73c0978cc1464bc73c7e.png)
    2. In the key deletion pop-up window, click **OK**.
   

:::
::: Batch deleting keys
    1. Select the target keys and click **Delete** at the top of the page.
        2. In the key deletion pop-up window, click **OK**.
        Only deletable ones of the selected key pairs will be deleted.
		![](https://main.qcloudimg.com/raw/bfcdfb401f8906834b02372d3e50dbe0.png)
		

:::
</dx-tabs>



## Related Operations


### Using an SSH key to log in to a Linux CVM

1. [Create an SSH key](#creatSSH).
2. [Bind an SSH key to a CVM instance](#bindingSSH).
3. [Log in to a Linux instance via SSH key](https://intl.cloud.tencent.com/document/product/213/32501).


### Editing a key tag

You can add, modify, or delete a tag for an SSH key in the following steps. For more information on tags, see [Overview](https://intl.cloud.tencent.com/document/product/651/13334). 

1. On the **SSH Key** page, click **Edit tags** on the right of the key.
2. In the **Edit tags** pop-up window, perform the desired operation.
3. Click **OK**.
