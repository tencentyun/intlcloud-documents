This document describes how to bind an ENI to a CVM.
>?
>+ If your CVM is based on a CentOS 8.0, 7.8, 7.6, 7.5 or 7.4 image, you can directly refer to the “Method 1: tool-based configuration” section in the [Configuring an ENI on a Linux CVM](https://cloud.tencent.com/document/product/576/59353). Namely, you need to install the tool before binding an ENI. Then, the ENI information will be automatically configured in the ENI file, and the routing policy will be automatically distributed.
>+ If your CVM is based on another type of image, bind an ENI to the CVM as instructed below. And then, [configure it on a Linux CVM](https://cloud.tencent.com/document/product/576/59353) or [a Windows CVM](https://cloud.tencent.com/document/product/576/59354).

## Binding a CVM
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Locate the ENI you want to configure and bind to a CVM, and click **Bind CVM** in the **Operation** column.
![](https://main.qcloudimg.com/raw/bce45aabdb1e1b26df31d3ff40211bce.png)
>?
>- ENI can only be bound to CVMs in the same availability zone.
>- ENI cannot be bound to BM (Bare Metal) 2.0.
>
4. In the pop-up window, select the CVM to be bound with the ENI and click **OK**.
    ![](https://main.qcloudimg.com/raw/7bbcb3850eae4b56ccd6d2f918f04682.png)

