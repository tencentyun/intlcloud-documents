The blocklist feature offers a proactive way to block spam SMS messages. You can add mobile numbers to the blocklist, and the blocked numbers cannot receive messages sent with the corresponding signature. Up to 1,000 numbers can be blocked for all signatures.

## Prerequisites
Before using the blocklist feature, you need to apply for an SMS signature and get it approved.

## Blocking a Mobile Number
1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. Select **General Management** > **Blocklist Management** on the left sidebar.
3. Click **Add Number**.
4. Select a signature and SMS message type and enter a mobile number.
 >If you need to add multiple numbers, separate them by pressing Enter (one number per row). Up to 1,000 numbers can be blocked for all signatures.
 >
 >Click **OK**.
 >After successful addition, the configuration will take about 5 minutes to take effect. When the status of the number becomes **effective**, it will be unable to receive SMS messages sent with the corresponding signature.
## Querying a Blocked Mobile Number
1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. Select **General Management** > **Blocklist Management** on the left sidebar.
3. Enter a mobile number and select the target signature at the top of the blocklist and click **Query** to check whether the number is in the current blocklist.
 


## Removing a Mobile Number from the blocklist
>Removing a mobile number from the blocklist is **irreversible**, and the number can receive SMS messages sent with the corresponding signature normally.

1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. Select **General Management** > **Blocklist Management** on the left sidebar.
3. You can choose the removal operation as needed:
 - Single removal: click **Remove** in the row of the target mobile number.
 - Batch removal: select the numbers to be removed and click **Batch Remove** at the top of the blocklist.
4. In the pop-up window, click **OK**.
