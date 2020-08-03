On an application's **Basic Configuration** Tab, you can view and manage the application information, excessive messaging reminder, event callback configuration, sending frequency limit, and frequency limit allowlist.

## Modifying Application Information

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) .
2. In the application list, click the name of the target application to enter the application details page which displays the **Basic Configuration** Tab by default.
3. Click **Edit** In **Application Information** And you can modify the **Application Name** And **Application Overview** .
4. Click **OK** To save the changes.

## Setting an Excessive Messaging Reminder

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) .
2. In the application list, click the name of the target application to enter the application details page which displays the **Basic Configuration** Tab by default.
3. Click **Set** In **Excessive Messaging Reminder** , select the reminder conditions for Chinese and international SMS messages as needed, and enter the corresponding reminder threshold.
4. Click **OK** To save the configuration.
    After successful configuration, when the number of messages sent by the current application on a calendar day reaches the threshold, the system will send a notification to the specified [Alarm contact](https://intl.cloud.tencent.com/document/product/382/32356) .

## Configuring Event Callback

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) .
2. In the application list, click the name of the target application to enter the application details page which displays the **Basic Configuration** Tab by default.
3. Click **Set** In **Event Callback Configuration** , select message status callback or message reply callback as needed, and enter the corresponding callback URL.
4. Click **OK** To save the configuration.
    After the setting is successful, you can have a more detailed understanding of the information related to the sending of SMS messages. For example, if you configure an SMS reception status callback address, Tencent Cloud will push the callback message to the callback address you specified after receiving the ISP callback message, and then you can develop the relevant code by yourself. receive, parse and apply the callback message pushed by Tencent Cloud SMS.

## Setting a Sending Frequency Limit

To ensure business and channel security and minimize financial loss caused by malicious call of SMS API, the default frequency limit for sending SMS messages is set as follows:

- For SMS messages with the same content, a maximum of one such message can be sent to the same phone number within 30 seconds;
- A maximum of 10 messages can be sent to the same mobile number on a calender day.

> - Note: individual users have no permission to modify the frequency limit. To use this feature, change "Individual Identity" to "Organizational Identity".
> - This setting is only valid for SMS messages.

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) .
2. In the application list, click the name of the target application to enter the application details page which displays the **Basic Configuration** Tab by default.
3. Click **Set** In **Sending Frequency Limit** , select the conditions as needed, and set the corresponding limit.
4. Click **OK** To save the configuration.

## Setting a Frequency Limit Allowlist

> Mobile numbers in the allowlist are not subject to the frequency limit policy. An allowlist can contain up to 300 mobile numbers. This setting is only valid for SMS messages.

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) .
2. In the application list, click the name of the target application to enter the application details page which displays the **Basic Configuration** Tab by default.
3. Click **Frequency Limit Allowlist** And enter a number per row. A maximum of 300 numbers can be added to the allowlist.
4. Click **Confirm the Conditions** To save the configuration.
