## Overview

Tencent Cloud allows you to batch enable or disable the transfer prohibition lock for multiple domains.

>!
> You cannot transfer domains with the **transfer prohibition lock** enabled from Tencent Cloud to another registrar's platform until the **transfer prohibition lock** is disabled, which enhances the domain security.
> 


## Prerequisites
1. Log in to the [Domains console](https://console.cloud.tencent.com/domain/).    

2. Select **Bulk Operation** on the left sidebar and select **Transfer Prohibition Lock** to enter its management page.


## Directions

### Step 1. Enter a domain

Enter the domain for which to enable the **transfer prohibition lock** in either of the following ways.
- **Enter a domain**: Enter or paste up to 200 domains for which to enable the **transfer prohibition lock**.
  

   >? 
   > If you enter more than 200 domains, you will be unable to proceed.
   > 

- **Upload File**: Click **Upload** and select a local file to batch upload domains.

   >! 
   > - You can upload up to 4,000 domains at a time. If this number is exceeded, only the first 4,000 domains will be uploaded.
   > - You can upload only **.txt/.xls/.xlsx** files.
   > - You can upload a file of up to 2 MB.
   > - You can click **Download template** to view the template format.


### Step 2. Set the status

>! 
> - You will be unable to perform the following operations if the update prohibition lock is enabled for the domain.
> - After a task is submitted, the system will start executing it. The operations may fail for certain domains as they are in different statuses.

1. You can batch set the transfer prohibition lock to either of the following statuses.

- **Enable Transfer Prohibition Lock**: After the lock is enabled, the domain cannot be transferred out from Tencent Cloud for security purposes.

- **Disable Transfer Prohibition Lock**: After the lock is disabled, the domain can be transferred to another registrar's platform.

2. Click **Next** to enter the information confirmation page.

3. Click **Submit** to update the status of the **transfer prohibition lock**.


### Step 3. View operation logs
1. On the **Bulk Operation** management page, select the **Operation Log** tab.

2. Select **Task** > **Transfer prohibition lock** and click **View details** to view the settings of the transfer prohibition lock of your domain.
