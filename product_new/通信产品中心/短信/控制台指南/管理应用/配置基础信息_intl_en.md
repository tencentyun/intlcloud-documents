On an application's **Basic Configuration** tab, you can view and manage the application information, excessive messaging reminder, event callback configuration, sending frequency limit, and frequency limit whitelist.



## Modifying Application Information
1. Log in to the [SMS Console](https://console.cloud.tencent.com/sms).
2. In the application list, click the name of the target application to enter the application details page which displays the **Basic Configuration** tab by default.
3. Click **Edit** in **Application Information** and you can modify the **Application Name** and **Application Overview**.
4. Click **OK** to save the changes.


## Setting an Excessive Messaging Reminder
1. Log in to the [SMS Console](https://console.cloud.tencent.com/sms).
2. In the application list, click the name of the target application to enter the application details page which displays the **Basic Configuration** tab by default.
3. Click **Set** in **Excessive Messaging Reminder**, select the reminder conditions for Chinese and international SMS messages as needed, and enter the corresponding reminder threshold.
4. Click **OK**.
    After successful configuration, when the number of messages sent by the current application on a calendar day reaches the threshold, the system will send a notification to the specified [alarm contact](https://cloud.tencent.com/document/product/382/36373).


## Configuring Event Callback
1. Log in to the [SMS Console](https://console.cloud.tencent.com/sms).
2. In the application list, click the name of the target application to enter the application details page which displays the **Basic Configuration** tab by default.
3. Click **Set** in **Event Callback Configuration**, select message status callback or message reply callback as needed, and enter the corresponding callback URL.
4. Click **OK**.
 After successful configuration, you will get a better grasp on SMS-related information and gain access to complete callback capabilities of the SMS service. For example, after you have configured the message receiving status callback address, Tencent Cloud will push the callback information received from the ISP to your specified callback address in a timely manner.

## Setting a Sending Frequency Limit
To ensure business and channel security and minimize potential financial losses caused by malicious calls of SMS APIs, the default frequency limit for sending SMS messages is as detailed below:
- For SMS messages with the same content, a maximum of one such message can be sent to the same mobile number within 30 seconds.
- A maximum of 10 messages can be sent to the same mobile number on a calender day.

>- Note: individual users have no permission to modify the frequency limit. To use this feature, change "Individual Identity" to "Organizational Identity".
>- This setting is only valid for SMS messages.

1. Log in to the [SMS Console](https://console.cloud.tencent.com/sms).
2. In the application list, click the name of the target application to enter the application details page which displays the **Basic Configuration** tab by default.
3. Click **Set** in **Sending Frequency Limit**, select the conditions as needed, and set the corresponding limit.
4. Click **OK**.
 ![](https://main.qcloudimg.com/raw/022ad62ddcdfb13be03a61973d1de770.png)

## Setting a Frequency Limit Whitelist
> Mobile numbers in the whitelist are not subject to the frequency limit policy. A whitelist can contain up to 300 mobile numbers. This setting is only valid for SMS messages.

1. Log in to the [SMS Console](https://console.cloud.tencent.com/sms).
2. In the application list, click the name of the target application to enter the application details page which displays the **Basic Configuration** tab by default.
3. Click **Frequency Limit Whitelist** and enter a number per row. A maximum of 300 numbers can be added to the whitelist.
4. Click **Confirm the Conditions** to save the configuration.


