
## Overview

TPNS supports adding custom parameters to the push text. After you bind custom parameters to the device and create a push, the device will display the message with custom parameters.

## Use Cases

This feature allows you to add custom parameters to the push task and display messages with different user attributes on devices, which is more appealing than the stereotyped push. For example, the account name “Pokonyan” shown in the following figure is customized.
<img src="https://main.qcloudimg.com/raw/7e49d269531e0714996b7fda40f8ba1f.jpg" width="60%"></img>


## Prerequisites

### Creating and managing user attributes

1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns).
2. Select **Toolbox** > **User Attribute Management** and click **New**.
3. In the dialog box, enter the attribute name and description, and click **OK**. Then you can view the created time, attribute name, attribute description and number of devices on the **User Attribute Management** page. You can edit or delete an attribute at anytime.
![](https://main.qcloudimg.com/raw/5fd62fb7e0026a292040a26f3d6cc16a.png)

### Binding user attributes

Before pushing a custom message, you need to bind the user attributes to devices using either of the following methods:

#### Method 1: using client APIs:

- For more information on iOS SDK, see [User Attribute Feature] (https://intl.cloud.tencent.com/document/product/1024/30727#.E7.94.A8.E6.88.B7.E5.B1.9E.E6.80.A7.E5.8A.9F.E8.83.BD).
- For more information on Android SDK, see [User Attribute Feature](https://intl.cloud.tencent.com/document/product/1024/38542).

#### Method 2: using RESTful APIs

For more information, see [Custom Push API](https://intl.cloud.tencent.com/document/product/1024/38542).

## Getting Started

### Using the console

1. Select **Message Management** > **Task List** and click **Create Push**.
![](https://main.qcloudimg.com/raw/a97f47ae0bc61d5ca67a8c235942f8cc.png)
2. Insert the user attributes on the right of the **Notification Title** or **Notification Content** field.
> ?One push supports adding up to 5 attributes at a time.
> ![](https://main.qcloudimg.com/raw/fcae716dba0f098efb91a72e8e2a466a.png)
3. Set to deliver the default notification or content if no user attribute is matched.
![](https://main.qcloudimg.com/raw/93833c98f826b90743debf8066da0a0e.png)
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
    "platform": "android",
    "ntf_wt_attrs":true
}
```
