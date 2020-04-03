## Prerequisites
1. You have activated the LVB service.
2. You have added your own domain name or leased a domain name.


## Viewing a Domain Name
On the Domain Management page, you can view the CNAME configuration status, type, current status, creation time, and expiration time of a leased domain name.
To view the domain name details, click the domain name or **Manage** on its right.

## Configuring a Domain Name
You can configure push/playback addresses for a domain name in the following ways:
#### Configuring a push domain name
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and select a push domain name in the domain name list or click **Manage** to enter its details page.
2. Select **Push Configuration**. You can customize the address expiration time and `StreamName` in the **Push Address Generator** and then click **Generate Push Address**.


>`StreamName` can contain only letters, digits, and symbols.

3. You can view the sample code for generating push addresses in PHP and Java in the **Push Address Sample Code** provided by Tencent Cloud. You can also use the sample code to calculate and generate **persistent push addresses**.

#### Configuring a playback domain name
- Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click **Manage** to the right of a playback domain name to enter its details page.
2. Select **Playback Configuration** to view the playback addresses for RTMP, FLV, and HLS formats prepared by Tencent Cloud.



## Disabling a Domain Name
To disable a domain name, click **Disable** on its right, confirm in the pop-up window, and click **OK**. When its status changes from "Enabled" to "Disabled", it is successfully disabled.
> Once disabled, the domain name cannot be accessed. It can be accessed again once enabled. The directions are the same for both playback and push domain names.

## Enabling a Domain Name
To enable a disabled domain name, click **Enable** on its right. When its status changes from "Disabled" to "Enabled", it is successfully disabled.

## Renewing a Leased Domain Name
To renew a leased domain name, click **More** > **Renew** on its right, confirm its new expiration time in the pop-up window, click **Buy Now** to enter the resource package purchase page, select the desired package quota, click **Buy Now**, and make the payment.


## Suspending a Leased Domain Name
To suspend a leased domain name, click **Suspend** on its right and confirm in the pop-up window. After it is suspended, its expiration time will be updated to 23:59:59 on the current day (i.e., the suspension will take effect the next day), and the remaining available days of the lease package cannot be refunded.
> 
>- After the suspension, you cannot add a new leased domain name before you delete the existing one.
>- Once suspended, the leased domain name will be retained for up to 3 months and will be terminated if not renewed by then.

## Deleting a Domain Name
To delete a domain name, click **More** > **Delete** on its right, confirm in the pop-up window, and click **OK**.
> 
>- If you delete a leased domain name, it will be suspended and deleted from the list.
>- After deleting a leased domain name, you can submit a domain name lease application again.
