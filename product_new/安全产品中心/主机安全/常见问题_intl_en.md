### What are the harms of server intrusion?
- Business interruption: the databases and files are tampered with or deleted, end users cannot access your services, and your system crashes.
- Data theft: hackers steal your data and sell it publicly. Your users' private data is leaked, damaging your enterprise brand image and bringing customer churning.
- File encryption by ransomware: hackers intrude your server and implant irreversible encrypted ransomware to encrypt your data for ransom.
- Unstable service: hackers run cryptomining malware or DDoS trojan programs on your server, consuming a large amount of system resources and making the server unable to provide normal service.

### How to automatically back up data using snapshot?
Snapshot is a data backup method provided by Tencent Cloud. It can create a fully-available duplicate of the specified cloud disk, whose lifecycle is independent of the lifecycle of the original cloud disk. You can create snapshots regularly to quickly recover data in case of accidental data loss.
You can create a snapshot in the console as instructed below:
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/overview).
2. Click **Cloud Block Storage** on the left sidebar.
3. Find the row of the desired instance and click **Create Snapshot**.
4. Wait until the snapshot is created.

For more information, please see [Snapshot Overview](https://cloud.tencent.com/document/product/362/5754).

### What to do if the system prompts that a password has been successfully cracked by brute force attacks?
If the password is cracked, the server may be hacked by a backdoor program embedded into it.
- Check the security status of the server to see whether there are other unknown accounts and trojan files, and if yes, delete them immediately and change the server login password.
- If necessary, you are recommended to reset the server and then set up a complex password containing at least 15 letters, number, and special characters.

### What to do if suspicious logins are detected?
CWP judges whether a login attempt is normal according to the list the common login locations. Please check the login log carefully. If a login was not intended, the password may have been compromised. In this case, you need to perform a detailed security check on the server.

### Why does CWP agent go offline? And how to solve the issue? 
The CWP agent may go offline because of the following reasons:
- The agent is blocked by the firewall policies of the server. Please configure the firewall policy of this server to allow CWP backend access address.
- The agent is corrupted by a third-party malware on the server. In this case, please re-install the agent.

### What to do if my server has trojan files?
To learn more about how to deal with trojan files detected, please see [Dealing with Trojan Files](https://cloud.tencent.com/document/product/296/13008).

### What to do if trojans are not successfully detected (false negative)?
If undetected trojan files are found, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=635&source=0&data_title=%E4%B8%BB%E6%9C%BA%E5%AE%89%E5%85%A8(%E4%BA%91%E9%95%9C)&step=1) to contact the Tencent Cloud security team for fast identification.

### How to uninstall the CWP agent?
- Log in to the [CWP Console](https://console.cloud.tencent.com/yunjing), select **Asset Management** > **Server List** on the left sidebar, find the server from which you want to uninstall CWP, and click **Uninstall**. Or, open the installation directory and use the uninstaller there to uninstall it.

### What to do if there is a problem in identity verification of my Tencent Cloud account?
If you have encountered a problem related to the Tencent Cloud account when using CWP, please see the [account documentation](https://cloud.tencent.com/document/product/378).
