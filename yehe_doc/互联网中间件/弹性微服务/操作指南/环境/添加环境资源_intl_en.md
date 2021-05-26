## Overview

This document describes how to add environment resources in the TEM console.

## Directions

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. On the **Environment** page, select a deployment region and click the target environment block to enter the environment information page.
3. In the resource details module, click **Add** to add storage, log, or registry resources.
   - Storage: select an existing storage resource. If there are no suitable CFS file systems, you can create [one](https://console.cloud.tencent.com/cfs/fs?rid=4).
	 ![](https://main.qcloudimg.com/raw/fe391a1fb69ed5d294079bdaaea19366.png)
   - Log: select an existing log resource. If there are no suitable logsets, you can create [one](https://console.cloud.tencent.com/cls/topic?region=ap-shanghai).
		![](https://main.qcloudimg.com/raw/418607848d7417f1329cf143c1d6d30d.png)
   - Registry: select an existing registry resource. If there are no suitable registry instances, you can create one in [TSE](https://console.cloud.tencent.com/tse/registry?rid=4). We recommend you select a registry in the same VPC to enable private network access between services.
		![](https://main.qcloudimg.com/raw/12337834fc470d100a99a4aed8c6f732.png)

     
