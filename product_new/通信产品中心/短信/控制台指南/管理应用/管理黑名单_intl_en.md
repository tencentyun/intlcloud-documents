The blacklist feature offers a proactive way to block spam SMS messages. You can add mobile numbers to the blacklist, and the blacklisted numbers cannot receive messages sent with the corresponding signature. Up to 1,000 numbers can be configured for all signatures under one application.

## Blacklisting a Mobile Number
1. Log in to the [SMS Console](https://console.cloud.tencent.com/sms).
2. In the application list, click the name of the target application to enter the application details page.
3. Select the **Blacklist Management** tab and click **Add a Mobile Number**.
4. Select a signature and SMS message type and enter a mobile number.
 >If you need to add multiple numbers, separate them by pressing Enter (one number per row). A maximum of 1,000 numbers can be added under one application.
 >
 ![](https://main.qcloudimg.com/raw/47cce8dd803655b5ee5a536abe65a026.png)
5. Click **OK**.
 After the addition succeed, the operation will take about 5 minutes to take effect. When the status of the number becomes **effective**, it will be unable to receive SMS messages sent with the corresponding signature.

## Querying a Blacklisted Number
1. Log in to the [SMS Console](https://console.cloud.tencent.com/sms).
2. In the application list, click the name of the target application to enter the application details page.
3. Select the **Blacklist Management** tab.
4. Enter a mobile number and select a signature at the top of the blacklist and click **Query** to check whether the number is in the current blacklist.
 ![](https://main.qcloudimg.com/raw/c0263291a6018aac1a4ee1d68c8f5b2c.png)

## Removing a Mobile Number from the Blacklist
>Removing a mobile number from the blacklist is **irreversible**, and the number can receive SMS messages sent with the corresponding signature normally.

1. Log in to the [SMS Console](https://console.cloud.tencent.com/sms).
2. In the application list, click the name of the target application to enter the application details page.
3. Select the **Blacklist Management** tab.
4. You can choose the removal operation as needed:
 - Single removal: click **Remove** in the row of the target mobile number.
 - Batch removal: select the numbers to be removed and click **Batch Remove** at the top of the blacklist.
5. In the pop-up window, click **OK**.

