You can modify configurations including bandwidth of a connected dedicated tunnel in the Direct Connect console. This document describes how to modify the bandwidth of a 1.0 or 2.0 tunnel in the console.

> ?For a shared connection, only the connection owner can modify the bandwidth of a dedicated tunnel.

## Preparation
You have [owned a tunnel](https://intl.cloud.tencent.com/document/product/216/19250) before you modify it.

## **Dedicated Tunnel 1.0**
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/conn) and click **Dedicated Tunnels** on the left sidebar to access the **Dedicated Tunnels** page.
2. Locate the dedicated tunnel to be modified, and click **More** > **Change tunnel** under the **Operation** column.
![]()
3. Adjust the bandwidth cap in the **Change tunnel** dialog and click **OK**.
![]()

## **Dedicated Tunnel 2.0**
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/conn) and click **Dedicated Tunnels** on the left sidebar to access the **Dedicated Tunnels** page.
2. Locate the target dedicated tunnel, and click <img src="https://main.qcloudimg.com/raw/134ed671d2fa3ec1b82525985c0a6633.svg" style="zoom:6%;" /> under the **Bandwidth** column.
> ? Only a **Connected** dedicated tunnel supports modifying the bandwidth.
> 
![]()
3. Specify a new bandwidth value in the edit box and click **OK**.
![]()
> ? The tunnel bandwidth cap cannot exceed the maximum bandwidth of the associated connection. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the connection bandwidth.
> 

