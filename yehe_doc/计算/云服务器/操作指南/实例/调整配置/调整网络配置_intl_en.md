## Changing the Billing Method
Tencent Cloud provides multiple network billing methods. You can switch the billing method between Bill-by-bandwidth and Bill-by-traffic in the console. For each CVM instance, however, you can switch between both billing methods twice at most.
For more information on billing, see [Public Network Billing Methods](https://intl.cloud.tencent.com/document/product/213/10578). 

## Changing the Public Network Type
Tencent Cloud provides two types of network configurations: dedicated public network and shared public network. The shared public network service is billed by bandwidth. To activate this service, you need to submit a ticket. For more information on billing methods, see [Billing of Shared Public Network](https://intl.cloud.tencent.com/document/product/684/15255). This document describes the billing methods of a single CVM instance. For more information, see [Public Network Billing Methods](https://intl.cloud.tencent.com/document/product/213/10578).

#### Bill-by-bandwidth for pay-as-you-go CVM instances
This billing method supports adjustment (increase or decrease) of the network bandwidth at any time. If you have changed the network bandwidth more than once within an hour, you are billed based on the maximum bandwidth.

#### Bill-by-traffic
This billing method supports the adjustment (increase or decrease) of the bandwidth cap at any time, and the change takes effect immediately.
> The Bill-by-traffic billing method is also applicable to pay-as-you-go CVM instances.

#### Bandwidth cap
The bandwidth cap varies with the billing methods and CVM configurations. For more information, see [Public Network Bandwidth Cap](https://intl.cloud.tencent.com/document/product/213/12523).

## Directions
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the instance list, select the target instance, and choose **More** > **Resource Adjustment** > **Adjust Network**.
3. In the **Adjust Network** window that appears, set the target bandwidth cap or change the billing method, and then click **OK**.
