
This document describes how to terminate a TDSQL-A for PostgreSQL instance in the console.

## Overview
You can terminate instances in the console as needed. After an instance is terminated, its status will become **Isolated**, and it will be completely eliminated after 7 days. Isolated instances cannot be restored.

>!
>- After an instance is terminated, its data cannot be recovered, and its backup files will also be terminated, so the data cannot be restored in the cloud either.
>- When the instance is terminated, its IP resources will be released simultaneously.

## Directions
1. Log in to the [TDSQL-A for PostgreSQL console](https://console.cloud.tencent.com/tdsqla/tdapg), select the target instance in the instance list, and click **More** > **Terminate** in the **Operation** column.
![](https://main.qcloudimg.com/raw/3ee36e69b705740ef35a509c74c5dc0b.png)
2. In the pop-up window, read and click "Yes, terminate it" and click **OK**.
![](https://main.qcloudimg.com/raw/a2151f6eacfcaab380f0a00c8ff4eaae.png) 
3. After you confirm the termination, the instance status will change to **Isolated**.
![](https://main.qcloudimg.com/raw/b32ca16b8211b2b39c645e1cab386fbb.png)
4. Select the target instance in the instance list and click **More** > **Eliminate Now** in the **Operation** column.
>!The elimination operation will terminate the instance completely, and its data will not be recoverable. Please back up the data in advance.
>
![](https://main.qcloudimg.com/raw/c5be91618049e1d48683df416d4dfb11.png)
5. In the pop-up window, confirm that everything is correct and click **OK**.
6. After the instance is eliminated successfully, a prompt will pop up in the top-right corner of the instance list.
![](https://main.qcloudimg.com/raw/b7869d46781925c69b0ab86b98c5935a.png)

 
