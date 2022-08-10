## Region
A region is the geographical area where a physical data center is located. In Tencent Cloud Short Message Service (SMS), regions are fully isolated from each other, which means data cannot be stored across regions but in the local region. We suggest you select a region according to the data storage requirements in different regions.
The features and prices of SMS services in different region are the same, but the data is not interconnected. Only the approved signatures and templates can be copied across regions.
Click [here](https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list) to view the region list.

## SMS Message Format
An SMS message consists of a signature and a body. Before sending an SMS message, you need to apply for a signature and a body template.
For example, if the SMS signature is `Tencent Technology` and the SMS body is `The login verification code for your account is 1234 and valid for 5 minutes.`, then the complete SMS message will be:
```
[Tencent Technology] The login verification code for your account is 1234 and valid for 5 minutes.
```
To send the above sample SMS message, perform the following steps:
1. Apply for an SMS signature whose **Signature Content** is `Tencent Technology`.
2. Apply for an SMS body template whose **SMS Content** is `The login verification code for your account is {1} and valid for {2} minutes.`, where {1} and {2} are customizable parameters when an SMS message is sent.
>!The signature is optional for Global SMS.

## SMS Signature
An SMS signature is the signature enclosed in [] before an SMS body, which is used to identify a company or business. To apply for an SMS signature, an enterprise user needs to upload a qualification certificate, while an individual user needs to upload an identity certificate. An SMS signature can be used only after it is approved.
**Sample SMS signature:**
Shenzhen Tencent Computer Systems Company Limited can apply for a signature associated with its company name, such as `[Tencent Technology]`, or one associated with the name of any product provided, such as `[Tencent Cloud]`.

>!You do not need to enter "[]" when applying for an SMS signature in the console. For example, if you want to use `[Tencent Technology]` as a signature, you simply need to enter `Tencent Technology` as the **Signature Content**.

## SMS Template
An SMS template is the SMS body content. SMS templates divide into verification code templates, notification templates, and marketing SMS templates. SMS content can be customized through template parameters.
>!You cannot apply for marketing SMS templates or send marketing SMS messages if you are an individual user.

Before applying for an SMS template, you need to apply for an SMS signature first. An SMS template can be used only after it is approved.
**Sample SMS template:**
If Tencent Technology wants to send an SMS verification code: `[Tencent Technology] The login verification code for your  account is 1234 and valid for 2 minutes.`, where the verification code (1234 in the sample) and validity period (2 minutes in the sample) can be changed in specific circumstances, then:
You can apply for a signature and a template as below:
- SMS signature: `Tencent Technology`
- SMS template: `The login verification code for your account is {1} and valid for {2} minutes.`
 {1} and {2} are variables that are arranged in order, and their values can be customized by setting the values of the template parameters when you send the SMS message.

## Regular SMS
Regular SMS messages include verification code SMS and notification SMS.
- **Verification code SMS**: Verification code messages for signup or login verification, payment confirmation, identity verification, etc.
 Sample:
 ```
Your login verification code is 1234. It will expire in 2 minutes. If the login was not performed by you, please ignore this message.
```
- **Notification SMS**: System notification messages such as delivery notifications, payment receipts, and status notifications.
 Sample:
 ```
The documents submitted for the ICP filing order 201700001234 have been approved. Please submit additional supporting documents as soon as possible. If you have already submitted them, Tencent Cloud will review them as soon as possible.
```

## Marketing SMS
Marketing SMS typically refers to SMS messages sent to registered members of websites or companies for marketing purposes during promotion campaigns or member events. The content of marketing SMS messages is usually about customer care or the notifications of new product launches or events.

Sample 1:
```
Great news! You can now apply to improve your store's ranking on the official website. A large number of free resources will help you raise your brand recognition. Try it right now! Unsubscribe by replying T.
```
Sample 2:
```
Another wave of new year promotions is on the way! Hairstyle goods are discounted by up to 30%. The flash sale will begin at 9:00 a.m. on February 17. Tap xxx for details. Unsubscribe by replying T.
```
