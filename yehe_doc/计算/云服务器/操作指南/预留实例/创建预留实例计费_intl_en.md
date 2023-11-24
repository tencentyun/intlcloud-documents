## Overview

Reserved Instance (RI) provides a discount for pay-as-you-go instances. This document describes how to create RI via the console.

## Prerequisites
Currently, RIs are only offered to beta users. To use it, go to the RI beta application page and [submit an application](https://intl.cloud.tencent.com/apply/p/bvrqmrrp5ns) to be a beta user.

## Directions
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. Click **Reserved Instance** on the left sidebar to enter the management page.
3. Click **Create Reserve Instance** to purchase RIs.

![image-20200909172355330](https://main.qcloudimg.com/raw/f604c27f8faeded74797d78d66ada9c2.png)

4. Configure the following information as prompted by the page:

| Parameter        | Required/Optional | Description                               |
| ------------------ | --------- | ------------------------------------------------------------ |
| Region/Availability Zone  | Required      | The region and availability zone where the matched pay-as-you-go instances reside.           |
| Operating System    | Required      | Linux OS,Windows.                                    |
| Validity         | Required      | RI term: 1 year.                    |
| Instance         | Required     | The type of pay-as-you-go instances that you want to match the RI.</br>These pay-as-you-go instances must exactly match RI attributes to benefit from the billing discount during the RI term.  |
| RI Name | Optional      | User-defined. <li> The RI name defaults to “unnamed” if this parameter is left empty.</li>  <li> You can enter any name within 60 characters.</li> |
| Billing Mode     | Required      | Select a billing option as needed:</br> <ul><li>**All Upfront**: you pay for the entire RI term with one upfront payment. This option provides you with the largest discount compared to the other two options below.</li><li>**Partial Upfront**: you make a low upfront payment and then pay for instance fees at a monthly rate or discounted hourly rate during the RI term. </li> </ul> |
| Quantity         | Required      | Number of RIs you want to purchase                             |


5. Click **Purchase Now** and complete the payment. Then you can visit the [Reserved Instance](https://console.cloud.tencent.com/cvm/reservedinstances/) console to query, search and manage your RIs. On this page, you can click **Create Instance** to create CVM instances, or click **View Bill** to see RI discount details.

   ![image-20200909173059650](https://main.qcloudimg.com/raw/86912bb5b8ceabbb071fbb6cfa06cadf.png)
