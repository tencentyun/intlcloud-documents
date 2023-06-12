## Overview

Tencent Cloud allows you to modify DNS servers for multiple domains.

>！
> 
> - Modifying DNS servers for a domain changes the DNS servers used to resolve the domain. Incorrect modifications may affect the normal resolution of the domain. Please proceed with caution.
> - After a task is submitted, the system will start executing it. The modification may fail for certain domains as they are in different statuses. Check the execution result do determine whether the modification is successful.
> - After you successfully modify the DNS server addresses, **the modification may take 24 to 48 hours to take effect globally**, depending on the DNS caching mechanisms of DNS service providers in different regions.


## Directions (Method 1)
1. Log in to the [Domains console](https://console.cloud.tencent.com/domain/).    

2. On the left sidebar, click **Bulk Operation** > **DNS Change** to enter the DNS change management page.


### Step 1. Enter domains

Enter the domains for which you want to modify DNS servers in either of the following ways:

- **Enter a domain**: Enter or paste up to 200 domains.
  

   >？
   > If you enter more than 200 domains, you will be unable to proceed.


- **Upload File**: Click **Upload** and select a local file to bulk upload domains.
  

   >！
   >   - You can upload up to 4,000 domains at a time. If this number is exceeded, only the first 4,000 domains will be uploaded.
   >   - You can upload only **.txt/.xls/.xlsx** files.
   >   - You can upload a file of up to 2 MB.
   >   - You can click **Download template** to view the template format.


### Step 2. Select DNS servers
1. Modify DNS servers in either of the following ways:

- **Use DNSPod (Recommended)**: The DNS addresses of the DNSPod servers will be automatically matched for the domains.
  

   >？
   > If you choose to use DNSPod, the DNS addresses for the current DNS plan will be matched.
   > 

- **Custom DNS**: Enter the DNS server addresses you want to set for the domains.
  

   >？
   >- The domain of a custom DNS server cannot be a private domain but must be an authoritative DNS server domain of a DNS service provider.


2. Click **Next** to enter the information confirmation page.

3. Click **Submit**.


### Step 3. View operation logs
1. On the **Bulk Operation** management page, select the **Operation Log** tab.

2. Select **Task** > **DNS Change** and click **View details** to view the DNS server modification result of your domains.


## Directions (Method 2)
1. Log in to the [Domains console](https://console.cloud.tencent.com/domain/).   

2. On the **My Domains** management page, select the target domains and click **More Operations** > **Modify DNS Server**.

3. In the **Identity Verification** pop-up window, obtain the verification code. The verification code email will be sent to the email address associated with your account. After entering the correct verification code, you can proceed.

4. In the **Modify DNS Server** pop-up window, select a modification method:

- **Use DNSPod**: The DNS addresses of the DNSPod servers will be automatically matched for the domains.

- **Custom DNS**: Enter the DNS server addresses you want to set for the domains.
  

>？
>- The domain of a custom DNS server cannot be a private domain but must be an authoritative DNS server domain of a DNS service provider.

