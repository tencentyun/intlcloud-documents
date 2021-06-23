## Overview

This document describes how to add environment resources in the TEM console.

## Directions

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. On the **Environment** page, select a deployment region and click the target environment block to enter the environment information page.
3. In the resource details module, click **Add** to add storage, log, or registry resources.
   - Storage: select an existing storage resource. If there are no suitable CFS file systems, you can create [one](https://console.cloud.tencent.com/cfs/fs?rid=4).
	 ![](https://main.qcloudimg.com/raw/940243e7479d02e8745d5a1d99180050.png)
   - Log: select an existing log resource. If there are no suitable logsets, you can create [one](https://console.cloud.tencent.com/cls/topic?region=ap-shanghai).
		![](https://main.qcloudimg.com/raw/60bff2ccdc80c0f0fa1cd5c60f2298a8.png)
   - Registry: select an existing registry resource. If there are no suitable registry instances, you can create one in [TSE](https://console.cloud.tencent.com/tse/registry?rid=4). We recommend you select a registry in the same VPC to enable private network access between services.
		![](https://main.qcloudimg.com/raw/6edf197b3eb3c2db85d1ccb4ed3cfff4.png)

     
