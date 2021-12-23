## Overview

This document describes how to establish or cancel a binding between an exchange and a queue in the TDMQ console.

## Prerequisites

- You have [created an exchange](https://intl.cloud.tencent.com/document/product/1112/43074).
- You have [created a queue](https://intl.cloud.tencent.com/document/product/1112/43075).

## Directions

### Creating binding

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), select the region, and click the ID of the target cluster to enter the cluster's basic information page.
2. Click the **Binding** tab at the top, select a vhost, and click **Create** to enter the **Create Binding** page.
3. On the **Create Binding** page, select the source exchange, binding target type, and binding target.
   ![](https://main.qcloudimg.com/raw/27dca8450a4f059179488062738be0ed.png)
4. Click **Submit**.

### Unbinding

>!After a binding is deleted, it will no longer provide services and cannot be recovered.

1. In the binding list, click **Unbind** in the **Operation** column of the target binding.
2. In the pop-up window, click **Delete**.
