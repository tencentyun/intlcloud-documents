
## Overview

TPNS supports adding custom parameters to the push text. After you bind custom parameters to the device and create a push, the device will display the message with custom parameters. This makes the push more attractive, so users are more likely to click on it.

## Use Cases

### Ecommerce

To increase the payment rate for items in cart, you can use the following template:

```
Hi, @{{nickname}}, there are only {{productnum}} left in stock for the {{productname}} in your cart.
Wanna buy it now?
```

**The push message Tommy receives is as follows**:

```plaintext
Hi, @Tommy, there are only 6 left in stock for the penguin doll in your cart. Wanna buy it now?
```

### Gaming

To reactivate inactive gamers through push, you can use the following template:

```
Hi, @{{nickname}}, you have not logged in to the game for {{offline_days}} days. We have prepared {{gift_num}} gift packages for you.
Come claim them. >>>
```

**The push message Tommy (who has been inactive for 3 consecutive days) receives is as follows**:

```plaintext
Hi, @Tommy, you have not logged in to the game for 3 days. We have prepared 6 gift packages for you. Come claim them. >>>
```


### Social networking

To reactivate users who have not opened the application for 3 consecutive days through push, you can use the following template:

```
Hi, @{{nickname}}, {{friend_num}} friends of yours posted {{story_num}} updates while you were away.
Come check them out. >>>
```

**The push message Tommy receives is as follows**:

```plaintext
Hi, @Tommy, 8 friends of yours posted 20 updates while you were away. Come check them out. >>>
```

## Prerequisites

### Creating and managing user attributes

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. Go to **Message Management** > **Attributes Management** and click **Add User Attribute**.
3. In the dialog box, enter the attribute name and description, and click **OK**. Then you can view the created time, attribute name, attribute description and number of devices on the **User Attribute Management** page. You can edit or delete an attribute at anytime.
![](https://main.qcloudimg.com/raw/c7693a0b6775c79cc8922cc5240d84d4.png)

### Binding user attributes

Before pushing a custom message, you need to bind the user attributes to devices using either of the following methods:

#### Method 1: using client APIs:

For the iOS SDK, see [here](https://intl.cloud.tencent.com/document/product/1024/30727).
For the Android SDK, see [here](https://intl.cloud.tencent.com/document/product/1024/30715).

#### Method 2: using the RESTful API

To bind user attributes via the RESTful API, see [here](https://intl.cloud.tencent.com/document/product/1024/38571).

## Getting Started

### Console

1. Go to **Message Management** > **Task List** and click **Create Push**.
2. Insert the user attributes on the right of the **Notification Title** or **Notification Content** field.
> ?One push supports adding up to 5 attributes at a time.
> ![](https://main.qcloudimg.com/raw/1b0c19bb25cf7075fc2fb0e4528737c2.png)
3. Set to deliver the default notification or content if no user attribute is matched.
![](https://main.qcloudimg.com/raw/cf33ae6b1b0ce97df310c04b28361f2a.png)
4. Click **Preview**, double check the information, and click **Confirm**.

### Using RESTful APIs

To enable the custom notification via the API, set `ntf_wt_attrs` to `true` and add the following fields to `message`.

| Parameter Name | Type | Required | Description |
| --------------- | ------ | -------- | -------------------------------------------- |
| default_content | string | Yes       | The default message content will be sent to devices if no user attribute is matched. |
| default_title | string | “Yes” for Android, and “No” for iOS | The default message title will be sent to devices if no user attribute is matched. |
| default_subtitle | string| No | The default message subtitle will be sent to devices if no user attribute is matched. |

For more information about other message fields, see the “message: message body” section in [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).

Below is a sample push:

```json
{
    "audience_type": "token",
    "expire_time": 3600,
    "message_type": "notify",
    "environment": "dev",
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
    "ntf_wt_attrs":true
}
```
