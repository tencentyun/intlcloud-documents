### The custom dictionary doesn't take effect. What should I do?

You can troubleshoot the problem as follows:

- After creating the custom dictionary, you need to create a [custom policy](https://intl.cloud.tencent.com/document/product/1139/44942#step4) and bind the dictionary to the policy for the dictionary to take effect. After configuring the policy, enter the policy name as the `Biztype` input parameter during API call, and the policy will take effect.
- If you use the default policy for testing purposes, you need to add custom keywords to the non-compliant word dictionary on the [**Custom Library Management**](https://console.cloud.tencent.com/cms/audio/lib) > **Preset Dictionary** page for them to take effect.

If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### I have already activated the AMS service, but when I call the short audio API, the system prompts that I don't have access to the API. What should I do?

The short audio API has not been opened up, so it cannot be called.

### When I call the audio moderation task creation API of AMS, the system prompts that "can not access bucket tianyu-content-moderation-1305692660 at region ap-guangzhou – write to bucket error The specified bucket does not exist." What should I do?

After activating the service in the [CMS console](https://console.cloud.tencent.com/cms/audio/overview), you will be prompted to authorize a COS bucket. Specifically, a bucket will be created to store the segments generated during moderation.

The above error will occur if you delete the COS bucket by mistake. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) and provide the `RequestId` for assistance.