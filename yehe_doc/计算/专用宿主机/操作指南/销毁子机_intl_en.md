When you no longer need a dedicated CVM, you can terminate it at any time. After the dedicated CVM is terminated, both the local disks and non-elastic cloud disks mounted on the instance will be terminated as well, and the data stored on these storage media will be lost. However, the elastic cloud disks mounted on the instance will be retained, and the data stored on them will not be affected.



## Terminating a dedicated CVM through the CVM console
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm).
2. Locate the dedicated CVM to be terminated. In the **Operation** column, choose **More** > **Instance Status** > **Terminate/Return**.
![](https://main.qcloudimg.com/raw/d1a990819a14e974f68e9f9527787d44.jpg)

## Terminating a dedicated CVM through an API
Use the TerminateInstances API to terminate a dedicated CVM instance. For more information, see [TerminateInstances](https://intl.cloud.tencent.com/document/product/213/33234).
