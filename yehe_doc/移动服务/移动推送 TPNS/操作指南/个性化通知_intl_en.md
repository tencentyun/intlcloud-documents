
## Overview

TPNS supports adding custom parameters to the push text. After you bind custom parameters to the device and create a push, the device will display the message with custom parameters, which can increase the willingness of users to click the message compared to stereotype pushes.

## Use Cases

### Ecommerce

To increase the payment rate for items in cart, you can use the following template:

```
Hi, @{{nickname}}. There are only {{productnum}} left in stock for the {{productname}} in your cart.
Wanna buy it now?
```

**The push message Tommy receives is as follows:**

```plaintext
Hi, @Tommy. There are only 6 left in stock for the penguin doll in your cart. Wanna buy it now?
```

### Gaming

To reactivate inactive gamers through push, you can use the following template:

```
Hi, @{{nickname}}, you have not logged in to the game for {{offline_days}} days. We have prepared {{gift_num}} gift packages for you.
Come claim them >>>
```

**The push message Tommy (who has been inactive for 3 consecutive days) receives is as follows:**

```plaintext
Hi, @Tommy, you have not logged in to the game for 3 days. We have prepared 6 gift packages for you. Come claim them >>>
```


### Social networking

To reactivate users who have not opened the application for 3 consecutive days through push, you can use the following template:

```
Hi, @{{nickname}}. {{friend_num}} friends of yours posted {{story_num}} updates while you were away.
Come check them out >>>
```

**The push message Tommy receives is as follows:**

```plaintext
Hi, @Tommy. 8 friends of yours posted 20 updates while you were away. Come check them out >>>
```

## Prerequisites

### Creating and managing user attribute

1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns)
2. Go to **Configuration Management** > **User Attribute Management** and click **Add User Attribute**.
3. In the dialog box, enter the attribute name and description, and click **OK**. Then you can view the created time, attribute name, attribute description, and number of devices on the "User Attribute Management" page. You can edit or delete an attribute at anytime.
![](https://main.qcloudimg.com/raw/c7693a0b6775c79cc8922cc5240d84d4.png)

### Binding user attribute

Before pushing a custom message, you need to bind the user attributes to devices in either of the following ways:

#### Method 1. Use client APIs

- For more information on how to configure user attributes in the SDK for iOS, please see [User Attribute Feature](https://intl.cloud.tencent.com/document/product/1024/30727#.E7.94.A8.E6.88.B7.E5.B1.9E.E6.80.A7.E5.8A.9F.E8.83.BD).
- For more information on how to configure user attributes in the SDK for Android, please see [User Attribute Feature](https://intl.cloud.tencent.com/document/product/1024/30715).

#### Method 2. Use RESTful APIs

For more information on how to bind through APIs, please see [User Attribute APIs](https://intl.cloud.tencent.com/document/product/1024/38571).

## Getting Started

### Console

1. Go to **Push Management** > **Task List** and click **Create Push**.
![](https://main.qcloudimg.com/raw/f6a351c7a33b8cbd10b785660dda61c9.png)
2. Insert the user attributes on the right of the "Notification Title" or "Notification Content" field.
> ?One push message can contain up to 5 attributes.
> ![](https://main.qcloudimg.com/raw/1b0c19bb25cf7075fc2fb0e4528737c2.png)
3. Set to deliver the default notification title or content if no user attribute is matched.
![](https://main.qcloudimg.com/raw/cf33ae6b1b0ce97df310c04b28361f2a.png)
4. Click **Preview**, confirm that everything is correct, and click **Confirm**.

### RESTful API

To enable custom notification through the API, set `ntf_wt_attrs` to `true` and add the following fields to `message`.

| Parameter Name | Type | Required | Description |
| --------------- | ------ | -------- | -------------------------------------------- |
| default_content | string | Yes       | The default message content will be sent to devices if no user attribute is matched. |
| default_title | string | Yes for Android, and no for iOS | The default message title will be sent to devices if no user attribute is matched.
| default_subtitle | string| No | The default message subtitle will be sent to devices if no user attribute is matched. |

For more information on other message fields, please see the "message: message body" section in [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).

Below is a sample push:

```json
{
    "audience_type": "token",
    "expire_time": 3600,
    "message_type": "notify",
    "environment":"dev",
    "message": {
        "title": "Hi, {{name}}",
        "content":"You have earned {{score}} points",
        "default_content": "Default content",
        "default_title": "Default title",
        "default_subtitle": "Default subtitle"
    },
    "token_list": [
        "086f959c7aefc3****add2ccf0cd539c1edd"
    ],
    "platform": "android",
    "ntf_wt_attrs":true
}
```
