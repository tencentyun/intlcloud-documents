
Starting from December 7, 2020, 21:30 (UTC +8), only **bill-by-hourly-traffic** is available for new CDN users. The CDN billing mode cannot be changed after service activation. Additionally, changing the ECDN billing mode is not allowed.

If you have activated CDN before that time, you can change the billing mode as instructed in [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949).

>?If you are a Tencent Cloud VIP customer with a monthly billing plan, you can contact your Tencent Cloud sales rep to change your billing mode.

## Notes:
The billing mode used to calculate the generated consumption on the current day will be also used for settlement on the following day.
+ If you switch from bill-by-bandwidth to bill-by-traffic when consumption has yet to occur, you will be charged with bill-by-traffic on the following day unless you switch the billing mode again.
+ If consumption has already occurred when you switch, you will be charged with bill-by-bandwidth on the following day. You will be charged with bill-by-traffic on the third day when calculating the consumption on the second day, unless you switch the billing mode again.

## How to Change Billing Mode
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Overview** on the left sidebar to find the **Billing Mode** section and click **Change**.
<img src="https://main.qcloudimg.com/raw/11ba290746b4ed66736119d94175e367.png" width=100%> 
2. Change the billing mode from **Bill by Traffic** to **Bill by Bandwidth** and click **Confirm**.
<img src="https://main.qcloudimg.com/raw/f611bf8653bce37ace29e99ebbb75f7b.png" width=70%> 
3. Your traffic packs can only be used when the billing mode is **bill-by-traffic**.
4. You can repeat the previous steps to cancel the switch.

