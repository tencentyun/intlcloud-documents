## Operation Scenarios
This document describes how to create a cluster in the TcaplusDB Console.

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629) successfully.

## Directions
1. Log in to the [TcaplusDB Console](https://console.cloud.tencent.com/tcaplusdb/app), select **Cluster List** on the left sidebar, and click **Create Cluster**.
2. In the "Create Cluster" dialog box that pops up, configure the cluster information.
 - **Network Type**: select a VPC and a subnet. You can select the VPC and subnet only when creating the cluster, which cannot be modified after creation.
 - **Connection Protocol**: select a connection protocol (data description protocol) for your TcaplusDB cluster.
 - **Cluster Name**: set the cluster name, which must be unique under the account and can contain 1–32 characters. You can rename the cluster at any time.
 - **Access Password**: set the cluster access password, which must meet the following requirements:
	 - 8–64 bits in length. The password of 12 or more bits is recommended.
	 - Cannot start with a slash (/)
	 - At least contain three types:
	  - Lowercase letters (a-z)
	  - Uppercase letters (A-Z)
	  - Digits (0-9)
	  - Special symbols (\~!@#$%^&*_-+=\|(){}[]:;'<>,.?/ )
 - **Table Group Name and Table Group ID**: create a default table group for the cluster and name it. The table group ID can be automatically generated or customized.
![](https://main.qcloudimg.com/raw/403156d42bf01dec755e6b169c77b160.png)
3. Click **Create Cluster** and the system will prompt that the creation succeeded.
You can return to the cluster list to view the created cluster and table group. Each cluster will be assigned a unique cluster ID.
![](https://main.qcloudimg.com/raw/7612056a6d9420ffb5697c0243c0e7d4.png)
