### What should I do if a user does not receive an SMS message?
Log in to the [SMS Console](https://console.cloud.tencent.com/sms), click the name of the target application to enter the application details page, and select **Mainland China SMS** (or **Global SMS**) > **Statistical Analysis** > **Message Records** to view the **Sending Status** and **Remarks** for the mobile number.
- If the **Sending Status** is "failed", you can troubleshoot the issue based on the cause as described in **Remarks**. The cause may be that the request has hit the frequency control policy, the SMS message format is incorrect, or the mobile number has been blocked due to unsubscription.
If the **Sending Status** is "successful", but an error code is displayed in **Remarks**, please troubleshoot the issue based on the specific [error code](https://intl.cloud.tencent.com/document/product/382/3771).
- If the **Sending Status** is "successful" and the **Remarks** display that "The user has successfully received the message", but the user actually has not received the message, you can troubleshoot the issue by following the steps below:
 - The mobile phone has been powered off or the mobile number has run out of credit or is out of service: check the status of the mobile phone/number, such as by dialing the number.
 - The mobile number is blocked: check whether the user has complained to the carrier or unsubscribed from the service.
 - The mobile phone cannot receive SMS messages because it has not been powered off for a long period of time: try restarting the mobile phone.
 - The mobile phone cannot receive SMS messages due to poor reception: check the reception and try restarting the mobile phone if necessary.
 - The mobile phone's SMS inbox is full: try deleting unwanted messages.
 - The mobile phone cannot receive SMS messages due to a settings or hardware issue: try changing the settings or removing the SIM card and inserting it into another mobile phone for testing (if the mobile phone is a dual SIM phone, try removing the SIM card and inserting it into the other card slot for testing).
 - The message has been blocked by the system/software in the mobile phone: check the blocklist.

If the issue persists, please consult [SMS Helper](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/382/3773).

<span id="jump"></span>
### What should I do if it takes a long time to call an API?
If you find that it takes a long time to call a Tencent Cloud SMS API, you can troubleshoot the issue in the following steps:
1. Run the `dig yun.tim.qq.com` command to check whether a private DNS is used, and if so, select a nearby Tencent Cloud SMS IP from the same carrier to configure the host and check whether the issue is fixed.
  - If the issue persists, the cause may be that the DNS resolution is stuck or there is a latency caused by cross-region or cross-carrier access. You are recommended to use a DNS proxy or set up a public DNS server.
  - If the issue persists, please follow [step 2](#Q2step2).
<span id="Q2step2"></span> 
2. Check which connection mode is used and whether a connection pool is used.
 - If a single persistent connection is used, according to the HTTP request/response model, if a request gets stuck, subsequent requests on the connection will be affected. The "persistent connection + connection pool" model is recommended.
 - If a non-persistent connection is used, run `netstat` to check whether the number of local connections has reached the upper limit, and if so, the "persistent connection + connection pool" model is recommended.
 - Run `netstat` to check or run `tcpdump` to capture packets to check whether there is a heap of connected Recv-Q and Send-Q, and if so, the "persistent connection + connection pool" model is recommended.
 - If no requests are sent over a connection for a long period of time (90 seconds), in order to prevent the intermediate network device from repossessing the connection, the requester is recommended to close the connection and establish a connection again when initiating a new request and there are not enough connections in the connection pool.

### Why does it take a long time for a user to receive an SMS message?

1. View the request sent time recorded in the local system and the SMS message sent time recorded in the console and calculate the difference between them.
 - If the difference is large (such as approximately or even more than 10 minutes), the cause may be that there is a delay in the API call. Please fix the issue by referring to [What should I do if it takes a long time to call an API?](#jump).
 - If the difference is small, please follow [step 2](#Q3step2).
<span id="Q3step2"></span> 
2. Check the **Sent Time** and **Status Reported Time** for the SMS message and calculate the difference between them.
 - If the difference is large (such as more than 10 seconds for general SMS or more than 5 minutes for marketing SMS), the cause may be that the SMS message is under review as it contains sensitive words, the mobile phone reception is poor, or the mobile number is in an exceptional state (for example, it has run out of credit or is out of service).
 - If the difference is small, the cause may be that the mobile phone reception is poor or the mobile phone is in an exceptional state (for example, it has been powered off).
3. If the issue persists, please consult [SMS Helper](https://intl.cloud.tencent.com/document/product/382/3773).

### What is a mobile number blocklist?

Currently, there are blocklists in the following types:
- Unsubscribed user list. After an user replies "T", "N", "TD", "Unsubscribe", "QX", or "0000" (case-insensitive) to unsubscribe, the system will put the user's mobile number on the blocklist after receipt of the reply. When an SMS message is sent again, "Failed to send" will be returned, with remarks "1015 The mobile number is blocked", and the user will be unable to receive the message.
 You can log in to the [SMS Console](https://console.cloud.tencent.com/sms), click the name of the target application to enter the application details page, select **Application Configuration** > **Unsubscribed User Management**, and submit an application for cancellation of the unsubscription, which will take effect upon approval.
- Carrier's blocklist. This type of users is blocked by the carrier for different reasons. When an SMS message is sent, "Sent successfully" will be returned, but the message may not be received by the user because it is blocked by the carrier's gateway or for other reasons.

### What should I do if error 1004 is returned?
When you call a Tencent Cloud SMS API to send an SMS message, if the response packet returns error 1004, you can troubleshoot the issue in the following steps:
1. Check whether the sent request is in standard JSON format. You are recommended to search for a JSON format checker on the internet to identify the issue; for example, single quotation marks are used as double quotation marks by mistake, but double quotation marks should be used for standard JSON format.
2. Check whether the parameter names are correct.
3. Check whether the field types of the request are the same as those as described in the [API documentation](https://intl.cloud.tencent.com/document/product/382/34689). For example, JSON strings and JSON integers are incorrectly used (e.g., `{"Name":"Tom", "Age":23}`, where "Name" should be a JSON string, while "Age" a JSON integer).
4. Check whether the field values of the request are within the value ranges as described in the API documentation. For example, the `international` field can only take a value of 0 or 1.
5. Check whether the API call is initiated as described in the API documentation. For example, when you call the API for sending bulk messages, you should not use the packet for sending a message to a single recipient.
6. If the issue persists, please consult [SMS Helper](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/382/3773).

### What should I do if error 1014 is returned?
When you call a Tencent Cloud SMS API to send an SMS message, if the response packet returns error 1014, you can troubleshoot the issue in the following steps:
1. Check whether the content template applied for is correctly formatted. For example, the "{}" in the content template should be English brackets, and the numbers in the brackets should start from 1, i.e., {1}, {2}, and so on.
2. Check whether the corresponding template has been approved.
3. Check whether the value of the `type` parameter in the request packet is the same as the type of the content template applied for (0 indicates general SMS, while 1 indicates marketing SMS).
4. Check whether the request content is in the same format as the content template applied for. For example, **a mismatch may occur due to invisible characters such as spaces.**
5. If the content contains Chinese characters, please make sure that they need to be encoded in UTF-8.
6. A Mainland China SMS template can only be used for sending messages to mobile numbers in Mainland China, while a Global SMS template can only be used for sending messages to mobile numbers outside Mainland China.
7. If the issue persists, please consult [SMS Helper](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/382/3773).

### What should I do if error 1016 is returned?
When you call a Tencent Cloud SMS API to send an SMS message, if the response packet returns error 1016, you can troubleshoot the issue in the following steps:
1. Check whether the `AppID` and `AppKey` are correct.
2. Check whether the mobile number is in the correct format. **A correct mobile number should not contain spaces.**
3. Check whether the field names are correct.


### What should I do if error 60008 is returned?
When you call a Tencent Cloud SMS API to send an SMS message, if the response packet returns error 60008, you can troubleshoot the issue in the following steps:
1. If error code 60008 is returned within 1 second in response to the request, please check whether the request is in standard HTTP format.
2. Check whether the URL and body format of the request match the API.
3. Check whether the `Content-Type` of the request is the same as that of the packet (`Content-Type: application/json;charset=utf-8` for SMS).
4. Check the DNS configuration to ensure that a public DNS server is used.
5. An HTTP persistent connection and a connection pool are recommended to improve network quality.
6. If the issue persists, please consult [SMS Helper](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/382/3773).

### What should I do if error 1001 (sig verification failed) is returned?
When you call a Tencent Cloud SMS API to send an SMS message, if the response packet returns error 1001, you can troubleshoot the issue in the following steps:
1. Check whether the random number generated by `sig` is the same as that in the URL.
2. Check whether the SDK `AppID` (starting with 1400) and `App Key` in the code are correct.
3. Check whether the code used is the same as the sample code and the `sig` pseudo-code generated from the parameters is consistent.

### Can the recipient reply to a Tencent Cloud SMS message? Is there a time limit for doing so?
The recipient must reply within 72 hours, and the reply can be viewed.

### What is the number used to send SMS messages after I activate Tencent Cloud SMS?
- For Mainland China SMS: the number contains 13–20 digits starting with 1069 and ending with a random number assigned by the carrier.
- For Global SMS: no numbers but only Qsms or Qcloud will be displayed.

### Can I send different SMS messages to different mobiles numbers at the same time?
You can send different SMS messages to different mobile numbers by calling the API for sending a message to a single recipient in multiple processes.

### What should I do if I cannot troubleshoot the issue that occurs while sending an SMS message?
You can consult [SMS Helper](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/382/3773).

### The application has been approved, but an SMS message fails to be sent, and the record indicates that it contains sensitive words. Why?
The vocabulary of sensitive words is provided by the carrier. You can contact [SMS Helper](https://intl.cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/382/3773) and provide the mobile number to which the message fails to be sent. A customer service agent will communicate with the carrier to fix the issue.

### Can I send marketing SMS messages if I am an individual user?
Individual users cannot send marketing SMS messages. For more information, please see [Instructions for Use](https://intl.cloud.tencent.com/document/product/382/13444?from_cn_redirect=1).


### Will each SMS message be reviewed after the SMS signature and body have been approved?
Individual users must obtain approval first before using the console to send SMS messages and are recommended to verify organizational identities.


### Can I send SMS messages offering loans?
No, you cannot send SMS messages offering loans.

### Can I send SMS messages about job interviews?
No, you cannot send SMS messages about job interviews or recruitment.


### Can I send SMS messages demanding payments?
You cannot send SMS messages offering loans or demanding payments.

### Can I send SMS messages offering home decor services?
Carriers do not allow you to send SMS messages offering home decor services.

### Can I send SMS messages that invite recipients to WeChat groups?
No, you cannot send SMS messages that ask recipients to follow WeChat/QQ accounts or invite them to groups.


### Can I send marketing SMS messages involving educational services (such as enrollment)?
Carriers do not allow you to send marketing SMS messages involving educational services.

### Can I send SMS messages that contain links to loan apps?
No, you cannot send SMS messages that offer loans; otherwise, you account will be banned.

### Can I send website links?
You can send text that contains an URL, but the URL must be entered in the body template and can be opened for review.


### Can I send SMS messages that contain information about rebates or VIP membership?
No, you cannot send SMS messages that contain information about rebates.


### I sent an SMS message to a mobile number, but the message was not received, and the mobile number cannot be found in the console. What should I do?
- If the message was sent through the console, you are recommended to check whether the mobile number in the sent file contains any extra characters, and if so, delete them.
- If the message was sent through the API, you are recommended to check whether the request has been properly sent to Tencent Cloud and whether any response has been returned.


### Can I use a server outside Mainland China to send SMS messages?
A server outside Mainland China can be used to call an API to send SMS messages, and the domain name can be resolved nearby. You can use the `curl` API for testing first.

### Can I send bulk SMS?
Yes, you can send an SMS message to up to 200 mobile numbers at a time by calling the [API](https://intl.cloud.tencent.com/document/product/382/5977) or up to 100,000 mobile numbers through the console.

### Can I receive SMS replies from users?
Yes, and no additional fees will be incurred by SMS replies. Replies can be viewed in the "Reply Records" section in the console or obtained by setting the callback address.


### Who can send marketing SMS messages?
Only organizational users can send marketing SMS messages, and they can only send membership marketing SMS messages. For more information on the review standards, please see [Instructions for Use](https://intl.cloud.tencent.com/document/product/382/13444?from_cn_redirect=1).


### What is the difference between marketing SMS and notification SMS?
Whether an SMS message is a marketing or general one depends on the nature of the message. For more information, please see [Common Concepts](https://intl.cloud.tencent.com/document/product/382/13299).


### My application for marketing SMS message is rejected as it contains text designed to acquire new customers. What does "acquire new customers" mean?
It refers to sending marketing SMS messages to users who have not purchased a product and have not signed up for membership. Due to a lot of complaints, SMS messages designed to acquire new customers cannot be sent.


### Why does the number contain asterisks when I preview an SMS message? For example, `Dear customer, your top-up payment of 1**2 USD has been credited to your account. Please check it in the system!`.
The console will encrypt numbers for storage, so numbers will contain asterisks when being previewed, but SMS messages received by users will be fully displayed.


### Does the Tencent Cloud SMS service support sending MMS?
No.
