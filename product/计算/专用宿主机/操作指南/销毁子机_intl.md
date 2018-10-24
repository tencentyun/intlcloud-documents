Dedicated CVM instances can be terminated at any time when they are no longer needed. When terminating an instance, the local disk and inelastic cloud disks mounted on it will be terminated too and the data saved on these disks will be lost. However, the elastic cloud disk mounted on the instance will be retained and the data there will not be affected.

## Terminating an Instance in CDH Console
1. Log in to the [CDH Console](https://console.cloud.tencent.com/cvm/cdh).
2. Click a host ID/name to enter the host details page.
3. Click **CVM list** to enter the details page of the instances on the host.
4. Select the dedicated CVM instance to be terminated and click **Terminate** to terminate it.
![Details page for termination](https://main.qcloudimg.com/raw/1d42bf78f07ab5af287763162af1f3a6.png)

## Terminating an Instance in CVM Console
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm).
2. In the Operation column on the right, click **More** > **CVM status** > **Terminate** on the dedicated CVM instance to be terminated.
![List page for termination](https://main.qcloudimg.com/raw/27ce25d4b9a4d4d095a64eb856ab2871.png)

## Terminating an Instance Through API
For details on how to terminate instances through the TerminateInstances API, see [API for Returning Instance](https://cloud.tencent.com/document/api/213/15723).
