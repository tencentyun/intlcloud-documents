## Overview

The reach rate and speed of app notification pushes are often compromised to various degrees due to factors such as **app processes not in the background**, **notifications disabled**, and **excessive vendor channels**.
If you have a type of push that requires high reach rate and speed (such as approval notifications and transaction notifications), you can use the supplementary SMS push feature provided by TPNS. This feature sends important information to users through SMS messages when they cannot receive app pushes, maximizing the reach rate and speed of messages.

## Use Cases

### System message pushes

Sends system-related messages to app users, including common notifications and SMS messages about upgrade/maintenance, service activation, price adjustment, order confirmation, logistics update, message confirmation, and payment.

### Promotional messages 

Sends messages to registered and potential users, including promotional information about sales campaign, business promotion, new product feature, and member care, to increase app exposure and user engagement.

## Directions

### Step 1. Bind mobile numbers

Before you use SMS push, you need to bind a mobile number for each user. The TPNS SDK provides an API for binding mobile numbers.
- For the SDK for Android, see [here](https://intl.cloud.tencent.com/document/product/1024/30715) to bind mobile numbers.
- For the SDK for iOS, see [here](https://intl.cloud.tencent.com/document/product/1024/30727) to bind mobile numbers.

### Step 2. Authorize access to the SMS platform

You need to save Tencent Cloud's API keys on the TPNS platform first, so that TPNS has the permission to send messages via the SMS platform. The configuration steps are as follows:
1. Log in to the [CAM console](https://console.cloud.tencent.com/).
2. On the left sidebar, click **Access Key** > [Manage API Key](https://console.cloud.tencent.com/cam/capi) to go the API key management page.
3. Click **Create Key** to create a key pair.
>? A key pair consists of a `SecretId` and `SecretKey`. Each user can have up to two key pairs.
>
4. Go to the [TPNS console](https://console.cloud.tencent.com/tpns).
5. On the left sidebar, click **Third-Party Service Authorization** to go to the third-party service authorization management page.
6. Click **Authorize Now**.
![](https://main.qcloudimg.com/raw/6089b5e64c2dfda9dc25b284a6caf14c.png)
7. In the pop-up dialog box, enter the `SecretId` and `SecretKey` and click **Confirm** to save.

### Step 3. Apply for SMS signatures and body templates

A complete SMS message consists of a **signature** and **body**. You can go to the [SMS console](https://console.cloud.tencent.com/smsv2) to create SMS signatures and body templates.
- To send SMS messages to users in Chinese mainland, please apply for a Chinese mainland SMS [signature](https://intl.cloud.tencent.com/document/product/382/35456) and [body template](https://intl.cloud.tencent.com/document/product/382/35457) first.
- To send SMS messages to users outside Chinese mainland, please apply for a Global SMS [signature](https://intl.cloud.tencent.com/document/product/382/35460) and [body template](https://intl.cloud.tencent.com/document/product/382/35461) first.

### Step 4. Start to use supplementary SMS push

Currently, TPNS supports using the supplementary SMS push feature via RESTful API calls only. You need to add the following fields to the message body when calling the push API:

| Parameter | Type | Required | Description |
| --------------- | ------ | -------- | -------------------------------------------- |
| resend_by_sms | bool | No       | Whether to enable supplementary SMS push. `true`: yes; `false`: no; default: `false` |
| sms_info | Object | No | Required for supplementary SMS push. The specific structure is as follows: [SmsInfo](#SmsInfo) |

<span id="SmsInfo"></span>
#### SmsInfo

| Parameter | Type | Required | Description |
| --------------- | ------ | -------- | -------------------------------------------- |
| delay_trigger_time | int | Yes | Time of trigger delay in seconds, that is, after you push normally, how long it will wait before performing the supplementary push if no trigger event is received. The minimum value is 300s. |
| trigger_condition | int | Yes | Event that triggers the supplementary SMS push.<li>`0`: send a supplementary SMS message to devices on which notifications are disabled.<li>`1`: sends a supplementary SMS message when no reach event is received within `delay_trigger_time`.<li>`2`: sends a supplementary SMS message when no click event is received within `delay_trigger_time`.</li> |
| sms_sign_name | String | No | SMS signature |
| sms_template_id | String| Yes | SMS template ID |
| sms_app_id | String | Yes | `appId` of the SMS platform |
|sms_template_params | Array of string | No | Parameters that must be carried in the template |

You can find the SMS signature, SMS template ID, and SMS platform’s `appId` in the [SMS console](https://console.cloud.tencent.com/smsv2). For more message parameters, see [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).

Below is a sample push:

```json
{
      "resend_by_sms": true,
      "sms_info": {
        "delay_trigger_time": 3600,
        "trigger_condition": 1,
        "sms_sign_name": "signe_name",
        "sms_template_id": "123",
        "sms_template_params": [
            "param1",
            "param2"
        ],
        "sms_app_id": "appId"
    },
    "audience_type": "token_list",
    "message": {
        "title": " test loop",
        "content": "test loop"
    },
    "token_list": ["025ae31e59b3**********a5866354b3","06dee08efed***********31ef23bba"],
    "message_type": "notify",
    "multi_pkg": true
}

```

After completing the push, you can view the SMS message records on the statistics page in the [SMS console](https://console.cloud.tencent.com/smsv2).


## FAQs

#### Do I need to pay extra fees for using supplementary SMS push when I have purchased the TPNS service?

Before you can use the **supplementary SMS push** feature, you need to purchase an SMS package. For more information, see [Billing Overview](https://intl.cloud.tencent.com/zh/document/product/382/18052).

#### Is there a limit on the delivery rate of supplementary SMS push?
The default delivery rate limit is as follows:
- SMS messages with the same content can be sent to a single mobile number only once within 30 seconds.
- A maximum of 10 messages can be sent to a single mobile number on a calender day.
Organizational users can log in to the [SMS console](https://console.cloud.tencent.com/smsv2) to set or modify the corresponding delivery rate limit policy. For detailed directions, please see [Setting Delivery Rate Limit](https://intl.cloud.tencent.com/document/product/382/35469).
Individual users have no permission to modify the delivery rate limit. To use this feature, change "Individual Identity" to "Organizational Identity". For more information on the rights of organizational users, please see [Differences in rights](https://intl.cloud.tencent.com/document/product/382/40653).


