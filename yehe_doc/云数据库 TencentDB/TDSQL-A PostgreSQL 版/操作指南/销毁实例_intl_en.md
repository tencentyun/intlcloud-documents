
This document describes how to terminate a TDSQL-A for PostgreSQL instance in the console.

## Overview
You can terminate instances in the console as needed. After an instance is terminated, its status will become **Isolated**, and it will be completely eliminated after 7 days. Isolated instances cannot be restored.

>!
>- After an instance is terminated, its data cannot be recovered, and its backup files will also be terminated, so the data cannot be restored in the cloud either.
>- When the instance is terminated, its IP resources will be released simultaneously.

## Directions
1. Log in to the [TDSQL-A for PostgreSQL console](https://console.cloud.tencent.com/tdsqla/tdapg), select the target instance in the instance list, and click **More** > **Terminate** in the **Operation** column.
![](https://main.qcloudimg.com/raw/d8ca1740516008506008123a6417d5bb.png)
2. In the pop-up window, read and click "Yes, terminate it" and click **OK**.
![](https://main.qcloudimg.com/raw/66d137dc9e911514ad5840e7ae258390.png) 
3. After you confirm the termination, the instance status will change to **Isolated**.
![](https://main.qcloudimg.com/raw/2f287b50e385e975964b9a0ee84151e4.png)
4. Select the target instance in the instance list and click **More** > **Eliminate Now** in the **Operation** column.
>!The elimination operation will terminate the instance completely, and its data will not be recoverable. Please back up the data in advance.
>
![](https://main.qcloudimg.com/raw/2b6fecdad330bd298944adab300fdef7.png)
5. In the pop-up window, confirm that everything is correct and click **OK**.
6. After the instance is eliminated successfully, a prompt will pop up in the top-right corner of the instance list.
![](https://main.qcloudimg.com/raw/d46f542185efc4250e60852745ca71d0.png)

 
