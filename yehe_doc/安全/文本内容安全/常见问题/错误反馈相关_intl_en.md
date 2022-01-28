### Why do I receive the error "Unauthorized operation. Check the CAM policy." when I call the `TextModeration` API?

A sub-user doesn't have the permission to call the service, and it needs to be authorized by the root account by associating it with the `QcloudTMSFullAccess` CAM policy as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

### The content is obviously pornographic, but the score returned by TMS is 0. What should I do?

If you encounter this problem, [submit a ticket](https://console.cloud.tencent.com/workorder/category) and provide the `RequestId` for assistance.

### The custom dictionary in TMS doesn't take effect. What should I do?

You can troubleshoot the problem as follows:

- When using a custom dictionary, you need to configure a custom policy and bind the dictionary to the policy as instructed in [Configure a custom policy](https://intl.cloud.tencent.com/document/product/1121/43753#step4) for the dictionary to take effect in about 5–10 minutes.
- If you use the default policy for testing purposes, you need to add custom keywords to the non-compliant word dictionary on the [**Custom Library Management**](https://console.cloud.tencent.com/cms/text/lib) > **Preset Dictionary** page for them to take effect.

If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Why are the configured keywords not blocked?

You can troubleshoot the problem as follows:

- When using a custom dictionary, you need to configure a custom policy and bind the dictionary to the policy as instructed in [Configure a custom policy](https://intl.cloud.tencent.com/document/product/1121/43753#step4) for the dictionary to take effect in about 5–10 minutes.
- If you use the default policy for testing purposes, you need to add keywords to the non-compliant word dictionary on the [**Custom Library Management**](https://console.cloud.tencent.com/cms/text/lib) > **Preset Dictionary** page for them to take effect.

If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Sensitive words are allowed in the keyword dictionary in TMS, but they are still blocked. What should I do?

Check the following:

1. Check whether the account that added sensitive words and the account that called the APIs are the same.
2. As the added sensitive words will take effect in 10 minutes, we recommend you wait for a while before you call APIs for testing purposes.
3. The system also detects and blocks variants of keywords. To avoid this problem, you can select **Exact Match** when configuring the dictionary.

If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.