For various types of Android apps, especially Android games, it is a common practice in business operations to customize versions for different channels and use different package names; however, this will lead to excessive workload for subsequent message pushes, as each package requires separate push, which is time-consuming and laborious and makes it difficult to achieve precise push and high efficiency.
The new "multi-package name push" feature of TPNS is a convenient solution to this problem. After this feature is enabled, you can easily add a multi-package name for different channels, and then one message push is enough to reach all channels.

## Use Cases
For operational promotions, a game vendor needs to publish an event announcement to all game players. The game is released in multiple app markets (such as CoolAPK, Anzhi, Wandoujia, and 360) with different package names. The multi-package name push feature can be used in this case. After it is enabled, when a push is sent, the event announcement can be received by all packages at the same time.

## Preparations
### Configuring in console
1. Log in to the TPNS Console and enter the [Product Management](https://console.cloud.tencent.com/tpns) page.
2. Select the application for which to configure multi-package name and click **Configuration Management**.
![](https://main.qcloudimg.com/raw/15f0ab0240137a1c7b02c6a73d1ef937.png)
3. If the application does not have a main package name, you need to enter one and then click **Add Package Name** to enter a package name.
![](https://main.qcloudimg.com/raw/687bc1a152d79e7347196c85c9d66c81.png)
4. If the application already has a main package name, click **Edit** to enter package name management, and click **Add** to enter a package name.
![](https://main.qcloudimg.com/raw/2949e98fcc0e9fd25490695a89ae770b.png)
>!Up to 50 package names can be configured.

### Configuring vendor channel for multi-package name
If your application has multiple package names, when you need to deliver messages to package names through vendor channels, you need to apply for a vendor key for each package name and configure it in the **[TPNS Console](https://console.cloud.tencent.com/tpns)** > **Configuration Management** > **Basic Configuration**.
Taking Huawei as an example, if the application has multiple package names configured, multiple key configurations will appear after the Huawei channel is enabled, and you need to complete the configuration for each package name; otherwise, messages to devices under a package name with incomplete configuration will be sent through the TPNS channel after multi-package name push is enabled.
![](https://main.qcloudimg.com/raw/5c454ec4e1c017ee2da11c6f8d1cb673.png)

### Integrating SDK
After configuring a package name, get the `AccessID` and `AccessKey`, and configure as instructed in [Android SDK Integration Guide](https://intl.cloud.tencent.com/document/product/1024/30713) or the **Quick Integration** process in the console.
![](https://main.qcloudimg.com/raw/86ced6140edd7012c8d1c7683f6e215a.png)

## Getting Started
### Console
After the above configuration is completed and confirmed, you can enable the multi-package name push feature in **Message Push** > **Create Push** > **Advanced Settings** in the **[TPNS Console](https://console.cloud.tencent.com/tpns)**.
![](https://main.qcloudimg.com/raw/cc1f1ec0ca401904438ac3a964cdefb1.png)
After enabling multi-package name push, a push will be delivered to devices that match the push target under all package names.
>?The multi-package name push feature is available only to Android. If the vendor channel corresponding to the package name is not configured, the message of the registered device under the package name is delivered through the TPNS channel.

### RESTful API
Set `multi_pkg` to `true` in the optional parameter of the Rest API to enable multi-package name push. For more information, please see [Push API Parameter Description](https://intl.cloud.tencent.com/document/product/1024/33764).
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
        "title": "Push title",
        "content": "Push content",
        "android": {
        	 "custom_content":"{\"key\":\"value\"}"
        }
    }
}
```
