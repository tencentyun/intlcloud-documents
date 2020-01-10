## Operation Scenarios
CFS supports transfer encryption and storage encryption. You can enable storage encryption when creating a file system and transfer encryption when mounting a file system. To try out the file storage encryption feature, please fill in the [CFS Encryption Feature Application Form](https://cloud.tencent.com/apply/p/alop3uh2szt) for application. This document describes how to use these two encryption features.

<table>
   <tr>
      <th>Item</th>
      <th>Limits</th>
      <th>Remarks</th>
   </tr>
   <tr>
      <td>Applicable region</td>
      <td>Hong Kong (China)</td>
      <td>Currently, transfer encryption and static storage encryption are supported only in Hong Kong (China)</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Transfer encryption - file access protocol</td>
      <td>Only NFS v4.0 is supported currently</td>
      <td>To enable transfer encryption, you need to mount the file system with NFS v4.0. Other versions of NFS and other protocols are not supported currently</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Transfer encryption - client limits</td>
      <td>Currently, transfer encryption can only be configured on operating systems with Linux or Unix kernel</td>
      <td>Transfer encryption is not supported on Windows clients currently</td>
   </tr>
</table>



## Prerequisites
- The [CFS](https://cloud.tencent.com/product/cfs) service has been activated, and the application for using the [CFS encryption feature](https://cloud.tencent.com/apply/p/alop3uh2szt) has been approved.
- The [KMS](https://cloud.tencent.com/document/product/573/34388) service has been activated.



## Directions
### Encrypting data in transfer
Due to the characteristics of the NFS protocol, communicated information in the file system that is accessed with NFS is transferred in plaintext. In some special scenarios, the information that the client communicates with the file system should be encrypted as required by the business. To meet this requirement, CFS supports enabling Transport Layer Security (TLS) when a file system is mounted to implement data encryption.

This example uses Stunnel, an open-source multipurpose proxy, to enable transfer encryption on CentOS. You can also use other applications that support TLS/SSL to configure transfer encryption on your own. You can enable transfer encryption in the following steps:

1. Download and install Stunnel.
```bash
yum install -y stunnel
```
If there is any exception when Stunnel is enabled in the public image of your CVM instance, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
2. Modify Stunnel permissions, create a directory named `stunnel` in the `/var/run/` directory, grant all users permissions to execute commands, and run the following command:
```bash
chmod 777 stunnel
```
3. Create the `stunnel.conf` file in the `/etc/stunnel` directory and copy the following content to the file.
```
root = /var/run/stunnel/
pid = /stunnel.pid
client = yes
[nfs]
accept = 2049
connect = cfs_ip:22049
```
4. Replace `cfs_ip` above with the IP address of the CFS instance you want to mount, as shown below.
```bash
connect = 10.0.0.1:22049
```
5. Start the Stunnel service.
```bash
/usr/bin/stunnel /etc/stunnel/stunnel.conf
```
6. Mount the file system and implement transfer encryption.
```
// In the following command, `localhost` is the localhost of the CVM instance, and `localfolder` is the target mount path.
mount -t nfs -o vers=4.0,rw,sync  localhost:/ /localfolder
```

### Encrypting static data

In addition to encryption in transfer, encryption of stored data is required too in some business scenarios. CFS features static data encryption to ensure data privacy.
CFS uses the key provided by [KMS](https://cloud.tencent.com/document/product/573) and the AES-256 algorithm for static data encryption. Once the file system encryption feature is enabled, you don't have to care about the encryption and decryption procedures, as the storage encryption process is completely imperceptible to your business systems.

When creating a file system, you can choose whether to encrypt it or not.
1. Log in to the [CFS Console](https://console.cloud.tencent.com/cfs).
2. Click **Create** and the "Create File System" window will pop up.
3. Select Hong Kong (China), enter other parameters, and click **Next**.
4. Check **Enable Data Encryption**. If you are using it for the first time, you need to authorize the CFS service to access KMS. During authorization, the system will generate a unique key for the CFS service for each user, which will be used for encrypting your newly created file system by default.
5. After the authorization is completed, return to the CFS Console and click **OK** to create an encrypted file system.
>Data stored in CFS can only be encrypted with the default key currently.
5. Then, you can mount and use the encrypted file system just like any other file systems. For more information on how to mount, please see [Using CFS File Systems on Linux Clients](https://intl.cloud.tencent.com/document/product/582/11523).
>Once you set encryption options when creating a file system, you will not be able to change the file system encryption attributes (including the encryption status and the key used).
