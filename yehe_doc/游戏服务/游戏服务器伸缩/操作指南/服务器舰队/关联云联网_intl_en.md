
## Overview

This document describes how to associate CCN to enable multi-point private interconnection, implementing multi-point interconnection in all regions on and off the cloud.

## Directions

### Associating with a CCN instance during the creation of the server fleet

1. Log in to the [GSE console](https://console.cloud.tencent.com/gse/asset) and click **Fleet** on the left sidebar to enter the server fleet page.
2. Click **Create** to create a server fleet.
![](https://camo.githubusercontent.com/02155cd8e3264bae81e2936d80c5a421bbde29c0340f690a24b1f859f8bedaf0/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f35393464663837326437393431626663656462633237383939376139343866322e706e67)
3. Select **Associate CCN Instance** on the **Create Fleet** page.
![](https://camo.githubusercontent.com/d01cc445038fa547acb626b29ca43a9766629b00e284397111976373e7ab4395/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f36633937363661323636363332363932326438333238383966356361646431382e706e67)
4. Enter the **Account ID** and **CCN Instance ID** for association.<br>
<img src="https://camo.githubusercontent.com/a30c3ed1cf7dda51ec46c1ee93a558a328e0773aa4d48e685964551063f52e53/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f39313966636633626661313934643032616236663137376262343063373464302e706e67" style="width: 75%;"/>

>?
 1. If you choose to associate with a CCN instance during the creation of the server fleet, the CCN instance owner needs to accept the association request in 20 minutes. Otherwise, the creation of the server fleet fails.
 2. The network interconnection fees arising from adding instance to CCN are borne by the CCN instance account.  
 3. Please note that the region where this CCN instance resides does not support cross-region interconnection (across all Tencent Cloud regions). If needed, contact your sales rep. 
>




### Associating with a CCN instance after the creation of the server fleet

1. Log in to the [GSE console](https://console.cloud.tencent.com/gse/asset) and click **Fleet** on the left sidebar to enter the server fleet page.
2. [Created a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675).
3. Click the **ID** of the server fleet that needs to associate with a CCN instance to go to its details page.
![](https://camo.githubusercontent.com/3bc6a3b373b8dab13e24bb09a8d80b5a0e7579a6dcd56e3c2d346364b17b1351/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f36333433313438373761663863626633323162626231663762643635626437332e706e67)
4. On the details page, click **Associate** in the **Associate CCN Instance** section.
![](https://camo.githubusercontent.com/cd203d79081eeb9400dfa0420edfafbe3850f776d8d3671e9f793d8a8bd67783/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f36333634363064396435376536613034336131373531393763343632323662312e706e67)
5. Enter the **Account ID** and **CCN Instance ID** for association.<br>
<img src="https://camo.githubusercontent.com/d71628bf784f991f4d683f53951fd34dd0eaf5aa31e886e0dab1971c4353121d/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f61346137376234616666366234333366643733373564613463306536373639372e706e67" style="width: 70%;"/>

> ? 
> 1. If you choose to associate with a CCN instance after the creation of the server fleet, the CCN instance owner needs to accept the association request in 7 days, after which it will expire.  
> 2. The network interconnection fees arising from adding instance to CCN are borne by the CCN instance account.  
> 3. Please note that the region where this CCN instance resides does not support cross-region interconnection (across all Tencent Cloud regions). If needed, contact your sales rep.  
