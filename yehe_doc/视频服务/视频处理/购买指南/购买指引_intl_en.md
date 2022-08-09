## Signing Up
Before using MPS, you need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Authorizing
### Step 1. Log in
Log in to the [MPS console](https://console.cloud.tencent.com/mps).

### Step 2. Grant access to COS
MPS needs read and write access to COS in order to download videos from COS buckets and upload files to COS buckets after transcoding. Therefore, you need to create a service role to grant MPS access to COS.
In the [MPS console](https://console.cloud.tencent.com/mps), click **Go to CAM** to grant the access.
![](https://qcloudimg.tencent-cloud.cn/raw/b5cf2f61dfd652dbd4af57abe13b06d3.png)

>! You cannot perform further operations in the MPS console before granting the permissions.

## Using MPS
After authorization, you can start using media processing services in the [MPS console](https://console.cloud.tencent.com/mps).

## Billing
Currently, MPS supports two billing modes: [pay-as-you-go](https://intl.cloud.tencent.com/document/product/1041/33478) and [prepaid resource packs](https://intl.cloud.tencent.com/document/product/1041/48810).
- **Daily pay-as-you-go**: Each day, the system calculates your usage in the previous day, sends you a bill, and deducts the fee from your account balance. In this mode, you need to [top up](https://console.cloud.tencent.com/expense/recharge) your account accordingly.
- **Monthly pay-as-you-go**: On the first day of each month, the system calculates your usage in the previous month, generates a bill, and deducts the fee from your account balance. In this mode, you need to [top up](https://console.cloud.tencent.com/expense/recharge) your account accordingly.
- **Prepaid resource packs**: With resource packs, MPS resources are sold in packages. You [buy resource packs](https://buy.cloud.tencent.com/mps) before using MPS, and your usage each day will be deducted from resource packs first. After your resource packages are used up, the remaining usage (if any) is billed at daily pay-as-you-go rates. For details, see [Resource Packs](https://intl.cloud.tencent.com/document/product/1041/48810).
