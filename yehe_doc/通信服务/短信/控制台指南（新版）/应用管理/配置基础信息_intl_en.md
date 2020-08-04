On an application's details page, you can view and modify application information. On its **Basic Configuration** page, you can set excessive messaging reminder, configure event callback, and manage alarm contacts.

## Modifying Application Information
1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. Select **Application Management** > **Application List** on the left sidebar and click the card of the target application to enter its details page.
3. Click **Modify Application** or click **Set** in **Application Information** to modify the **Application Name** and **Application Overview**.
4. Click **Modify** to save the changes.


## Setting Excessive Messaging Reminder
1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. You can enter the **Basic Configuration** tab in the following ways:
 - Select **Application Management** > **Application List** on the left sidebar and click the card of the target application to enter its details page. Then, click **Basic Configuration**.
 - Select **Application Management** > **Basic Configuration** on the left sidebar.
3. Select the **current application** as the target application to be manipulated.
3. Click **Set** in **Excessive Messaging Reminder**, select the reminder conditions for Mainland China or Global SMS as needed, and enter the corresponding reminder threshold.
4. Click **Set** to save.
    After successful configuration, when the number of messages sent by the current application on a calendar day reaches the threshold, the system will send a notification to the specified [alarm contact](https://intl.cloud.tencent.com/document/product/382/35470).


## Configuring Event Callback
1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. You can enter the **Basic Configuration** tab in the following ways:
 - Select **Application Management** > **Application List** on the left sidebar and click the card of the target application to enter its details page. Then, click **Basic Configuration**.
 - Select **Application Management** > **Basic Configuration** on the left sidebar.
3. Select the **current application** as the target application to be manipulated.
4. Click **Set** in **Event Callback Configuration**, select message status callback as needed, and enter the corresponding callback URL.
5. Click **Set** to save.
 After successful configuration, you will get a better grasp on the information related to SMS sending status. For example, after you configure the message receiving status callback address, Tencent Cloud will push the callback information received from the ISP to your specified callback address in a timely manner. Then, you can write appropriate code to receive, parse, and further use the callback information pushed by Tencent Cloud SMS.

## Setting Sending Frequency Limit
To ensure business and channel security and minimize potential financial losses caused by malicious calls of SMS APIs, the default frequency limit for sending SMS messages is as detailed below:
- For SMS messages with the same content, a maximum of one such message can be sent to the same mobile number within 30 seconds.
- A maximum of 10 messages can be sent to the same mobile number on a calendar day.

>Note: individual users have no permission to modify the frequency limit. To use this feature, change "Individual Identity" to "Organizational Identity".

1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. You can enter the **Basic Configuration** tab in the following ways:
 - Select **Application Management** > **Application List** on the left sidebar and click the card of the target application to enter its details page. Then, click **Basic Configuration**.
 - Select **Application Management** > **Basic Configuration** on the left sidebar.
3. Select the **current application** as the target application to be manipulated.
4. Click **Set** in **Sending Frequency Limit**, select the conditions as needed, and set the corresponding limit.
5. Click **Set** to save.

## Setting Frequency Limit Allowlist
> Mobile numbers in the allowlist are not subject to the frequency limit policy. An allowlist can contain up to 300 mobile numbers.

### Adding a mobile number to the allowlist
1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. You can enter the **Basic Configuration** tab in the following ways:
 - Select **Application Management** > **Application List** on the left sidebar and click the card of the target application to enter its details page. Then, click **Basic Configuration**.
 - Select **Application Management** > **Basic Configuration** on the left sidebar.
3. Select the **current application** as the target application to be manipulated.
4. Click **Set** in **Frequency Limit Allowlist** and enter a number per row. A maximum of 300 numbers can be added to the allowlist.
5. Click **Set** to save the settings.

### Removing a mobile number from the allowlist
1. Log in to the [SMS Console](https://console.cloud.tencent.com/smsv2).
2. You can enter the **Basic Configuration** tab in the following ways:
 - Select **Application Management** > **Application List** on the left sidebar and click the card of the target application to enter its details page. Then, click **Basic Configuration**.
 - Select **Application Management** > **Basic Configuration** on the left sidebar.
3. Select the **current application** as the target application to be manipulated.
4. Click **Delete** in the row of the target mobile number in **Frequency Limit Allowlist**.
5. Click **Delete**.
