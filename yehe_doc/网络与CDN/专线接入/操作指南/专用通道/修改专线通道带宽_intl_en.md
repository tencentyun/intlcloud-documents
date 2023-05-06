You can modify configurations including bandwidth of a connected dedicated tunnel in the Direct Connect console. This document describes how to modify the bandwidth of a 1.0 or 2.0 tunnel in the console.

> ?For a shared connection, only the connection owner can modify the bandwidth of a dedicated tunnel.

## Prerequisites
You have [owned a tunnel](https://www.tencentcloud.com/document/product/216/19250) before you modify it.

## **Dedicated Tunnel 1.0**
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/conn) and click **Exclusive virtual interface** in the left sidebar.
2. On the **Exclusive virtual interface** page, find the dedicated tunnel to be modified, and choose **More** > **Change tunnel** in the **Operation** column.
3. Modify the bandwidth cap in the **Change tunnel** pop-up window and click **OK**.
>?If the tunnel bandwidth is greater than 1 Gbps, you can increase the bandwidth value by an integer multiple of 1 Gbps, such as 2 Gbps and 3 Gbps.
>

## **Dedicated Tunnel 2.0**
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/conn) and click **Exclusive virtual interface** in the left sidebar.
2. Find the target exclusive dedicated tunnel, and click <img src="https://main.qcloudimg.com/raw/134ed671d2fa3ec1b82525985c0a6633.svg" style="zoom:6%;" /> in the **Bandwidth** column.
> ? You can modify the bandwidth only for a dedicated tunnel that is in the **Connected** state.
> 
3. Specify a new bandwidth value in the edit box and click **OK**.
> ? The tunnel bandwidth cap cannot exceed the maximum bandwidth of the associated connection. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the connection bandwidth.
> 
