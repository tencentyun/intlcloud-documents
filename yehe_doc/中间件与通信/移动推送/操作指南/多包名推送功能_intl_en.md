For various types of Android apps, especially Android games, it is a common practice in business operations to customize versions for different channels and use different package names; however, this will lead to excessive workload for subsequent message pushes, as each package requires separate push, which is time-consuming and laborious and makes it difficult to achieve precise push and high efficiency.
The Multi-Package Name Push feature of TPNS is a convenient solution to this problem. After this feature is enabled, you can easily add package names for different channels, and then one message push can reach all channels.

## Scenarios
For marketing promotions, a game vendor needs to publish an event announcement to all game players. The game is released in multiple app markets (such as CoolAPK, Anzhi, Wandoujia, and 360) with different package names. In this case, Multi-Package Name Push can be used to send the event announcement to all packages at a time.

## Preparations
### Configuring in console
1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns) and go to the **Product Management** page.
2. Select the application for which to configure multiple package names and click **Configuration Management**.
![](https://main.qcloudimg.com/raw/15f0ab0240137a1c7b02c6a73d1ef937.png)
3. If the application does not have a main package name, you need to enter one and then click **Add another package name** to enter a channel-specific package name.
![](https://main.qcloudimg.com/raw/687bc1a152d79e7347196c85c9d66c81.png)
4. If the application already has a main package name, click **Edit** to open the **Package Name Management** section, and click **click here to add** to configure a package name.
![](https://main.qcloudimg.com/raw/2949e98fcc0e9fd25490695a89ae770b.png)
>!Up to 50 package names can be configured.

### Configuring vendor channel for multi-package name
If your application has multiple package names, when you need to deliver messages to package names through vendor channels, you need to apply for a vendor key for each package name and configure it in the [TPNS console](https://console.cloud.tencent.com/tpns) > **Message Management** > **Basic Config**.
Taking Huawei as an example, if the application has multiple package names configured, multiple key configurations will appear after the Huawei channel is enabled, and you need to complete the configuration for each package name. Otherwise, messages to devices under a package name with incomplete configuration will be sent through the TPNS channel after Multi-Package Name Push is enabled.
![](https://main.qcloudimg.com/raw/5c454ec4e1c017ee2da11c6f8d1cb673.png)

### Integrating the SDK
After configuring a package name, get the `AccessID` and `AccessKey`, and configure as instructed in [Android SDK Integration Guide](https://intl.cloud.tencent.com/document/product/1024/30713) or the **Quick Integration** process in the console.
![](https://main.qcloudimg.com/raw/86ced6140edd7012c8d1c7683f6e215a.png)

## Getting Started
### Using the console
After the above configuration is completed and confirmed, you can enable Multi-Package Name Push in the [TPNS console](https://console.cloud.tencent.com/tpns) > **Message Management** > **Task List** > **Create Push** > **Advanced Settings**, as shown below:
![](https://main.qcloudimg.com/raw/cc1f1ec0ca401904438ac3a964cdefb1.png)
After enabling Multi-Package Name Push, a push will be delivered to devices that match the push target under all package names.
>?Multi-Package Name Push is available only to Android. If a vendor channel corresponding to a package name is not configured, messages to devices registered under the package name will be delivered through the TPNS channel.

### Using RESTful APIs
Set the RESTful API's optional parameter `multi_pkg` to `true` to enable Multi-Package Name Push. For more information, please see the parameter description in [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).
Below is a sample push:
```
{
    "audience_type": "token",
    "token_list": [
        "05da87c0ae5973******9e08d884aada5bb2"
    ],
    "message_type": "notify",
    "multi_pkg":true,
    "message": {
        "Title": "Push title",
        "content": "Push content",
        "android": {
        	 "custom_content":"{\"key\":\"value\"}"
        }
    }
}
```
