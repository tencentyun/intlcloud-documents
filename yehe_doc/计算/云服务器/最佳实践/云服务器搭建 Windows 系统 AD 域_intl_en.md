## Overview
This document introduces how to set up an Active Directory (AD) domain based on a Windows server 2012 R2 data center version 64-bit operating system. Active Directory (AD) is a core component of Microsoft services. AD can achieve efficient management through batch management of users, deploying applications and updating patches. An AD domain is required for many Microsoft components (such as Exchange) and failover clusters. 

## Prerequisites

- You have created two Windows-based CVM instances, which are used as a domain controller (DC) and a client.
- Requirements for the instances:
	- Use NTFS partition;
	- Support DNS service;
	- Support TCP/IP protocol.

## Instance Network Environment
- Networking: The instances are in VPC, and the private IP range of the switch is `10.0.0.0/16`.
- Domain name: For example, `example.com`. The IP address of the CVM instance used as the DC is `10.0.5.102`, while the IP address of another instance is `10.0.5.97`.
<dx-alert infotype="notice" title="">
After setting up the AD domain, keep the IP address of the CVM instances unchanged. 
</dx-alert>



## Concepts
The main concepts of AD are listed below:
- **DC**: Domain controller.
- **DN**: Distinguished name.
- **OU**: Organization unit.
- **CN**: Canonical name.
- **SID**: Security identifier.


## Directions

<dx-alert infotype="explain" title="">
It's not recommended to create an instance with an image whose source instance is already deployed with a domain controller. If you do need to use this image, please be sure that the host name of new instance is the same as the host name of source instance of the image. Otherwise, an error **The security database on the server is not trusted** can be reported. You can also change the new instance name to the same hostname after the instance creation to solve this problem.
</dx-alert>



### Deploying AD domain controller[](id:Step1)
1. Log in to the CVM instance used as a DC.
2. In the OS interface, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin:-3px 0px"> to open **Server Manager**.
3. Click **Add Roles and Features**, and the **Add Roles and Features Wizard** window pops up.
4. In the **Select Installation Type** page, select **Role-based or feature-based installation** and click **Next** twice.
5. In the **Select Server role** page, tick **AD Domain Service" and "DNS Server** , and click **Add features** and **Next** in the pop-up window.
This example deploys the AD domain service and DNS service on the same instance.
6. Keep the default configuration for the next four steps till you reach the confirmation page.
7. On the confirmation page, click **Install**.
After the installation is complete, close the **Add Roles and Features** dialog.
8. In the OS interface, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin:-3px 0px"> to open **Server Manager**.
9. Click <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin:-3px 0px">, and select **Promote this server to a domain controller**.
10. In the **AD Domain Service Configuration Guide** window, set "Select deployment operation" to **Add a new forest**, and enter the root domain name (for example, "example.com"). Then, click **Next**.
11. Set the Directory Services Restore Mode (DSRM) password and click **Next**.
12. Keep the default configuration for the next four steps till you reach the **Prerequisite Check** page.
13. In the **Prerequisite Check**, click **Install**.
After the installation of AD domain server, you can reconnect to the instance and view the installation result in **Control Panel** > **System and Security** > **System**.

### Modifying the client SID
Modify the SID of the instance used as the client. For details, see [Modifying SID](https://intl.cloud.tencent.com/document/product/213/4829).


### Joining the client to AD domain
1. Log in to the CVM instance used as the client.
2. Modify the DNS server address.
    i. Open **Control Panel** > **Network and Internet** > **Network and Sharing Center**, and click **Ethernet**, .
      ii. In the **Ethernet Status** window, click **Properties**.
    iii. Select **Internet Protocol Version 4 (TCP/IPv4)** in the "Ethernet Properties" window and click **Properties**.
    iv. In the **Internet Protocol Version 4 (TCP/IPv4) Properties** window, select **Use the following DNS server address** and set the preferred DNS server address (`10.0.5.102` in this example) as the IP address of the instance.
  In the step of [Deploying AD domain controller](#Step1), AD domain service and DNS service are deployed on the same CVM instance (IP: `10.0.5.102`), so the address of the DNS server specified here is `10.0.5.102`.
     v. Click **Ok**.
3. In the cmd window, execute the following `ping` command to check whether the IP address is connected.
```
ping example.com
```
4. Open **Control Panel** > **System and Security** > **System**, and click **Change Settings** in the "System" window.
5. In the pop-up **System Properties** window, click **Change**.
6. In the pop-up **Computer Name/Domain Change** window, modify the computer name as required, and set `example.com` as the domain.
7. Click **OK**.
8. In the pop-up **Windows Security**, enter the username and login password of the instance, and click **OK**.
The client successfully joins the domain when the following window pops up.
9. Click **Ok**, and restart the instance for the configuration to take effect.
<dx-alert infotype="explain" title="">
If the CVM instance that works as the client has joined a domain, don’t use it to create the custom image, which can cause the error **The security database on the server is not trusted**. If you do need to create an image for this instance, remove the instance from the domain first.
</dx-alert>

