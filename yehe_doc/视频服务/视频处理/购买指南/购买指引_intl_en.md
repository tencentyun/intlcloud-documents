## Signing up
You need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) before using MPS.

## Authorizing
### Step 1. Log in

Log in to the console and go to **All Products** > **Video Services** > [**Media Processing Service**](https://console.cloud.tencent.com/mps).

### Step 2. Grant access to COS
MPS needs read and write access to COS in order to download and transcode videos in COS buckets as well as upload files to buckets. Therefore, you need to create a service role and grant the role access to COS.

Go to the [MPS console](https://console.cloud.tencent.com/mps), and click **Go to CAM** to enter the authorization page to grant the access.
![](https://qcloudimg.tencent-cloud.cn/raw/e001187c224f239c596ccc4343e03be7.png)
>!You cannot perform further operations in the MPS console before granting the access.


## Using MPS
After authorization, you can start using MPS in the console via **All products** >**Video Services** > [**Media Processing Service**](https://console.cloud.tencent.com/mps).

## Billing
MPS supports two billing modes: **daily pay-as-you-go** and **monthly pay-as-you-go**. For details, see [Billing Mode](https://intl.cloud.tencent.com/document/product/1041/33478).

- **Daily pay-as-you-go**: You need to [top up](https://console.cloud.tencent.com/expense/recharge) your account in order to use this mode. On a daily basis, the system calculates your usage in the previous day, sends you a bill, and deducts the fee from your account.
- **Monthly pay-as-you-go**: You need to [top up](https://console.cloud.tencent.com/expense/recharge) your account in order to use this mode. On the first day of each month, the system calculates your usage in the previous month, generates a bill, and deducts the fee.
