### Can I customize a dictionary in TMS?

Yes. You can configure and apply a custom dictionary as follows:

1. On the [**Custom Library Management**](https://console.cloud.tencent.com/cms/text/lib) > **Custom Dictionary** page, create a custom dictionary and add non-compliant words as instructed in [Configure a custom dictionary](https://intl.cloud.tencent.com/document/product/1121/43753#step5).
2. After creating the custom dictionary, you need to create a [custom moderation policy](https://intl.cloud.tencent.com/document/product/1121/43753#step4) and bind the dictionary to the policy for the dictionary to take effect.

### Does custom library management support API calls?

No.

### Can I add custom banned words? Is there an API for this?

- Yes. Go to **Custom Library Management** > **Preset Dictionary** in the [TMS console](https://console.cloud.tencent.com/cms/text/lib), select a preset non-compliant word dictionary, and click **Manage** > **Add Sample** in the **Operation** column.
- Currently, there is no API for adding custom banned words.

### Can I group custom banned words?

You can create multiple custom dictionaries for grouping purposes. A custom dictionary needs to be associated with a policy for it to take effect. You can enter different `Biztype` values to associate different custom dictionaries. When calling APIs, you need to enter the name of the created policy as `Biztype` for the policy to take effect.

### Can I batch import words into a custom dictionary?

Yes. You can request configuration on the backend by [submitting a ticket](https://console.cloud.tencent.com/workorder/category). Before configuration, you need to categorize keywords (such as by "violence", "terrorism", and "porn") and separate them by line breaks.

### Which dictionary does the policy I create use?

● If you don't associate a custom dictionary when creating a custom policy, the preset dictionary will be used by default.
● You can add custom keywords to the preset dictionary. To allow keywords, go to **Custom Library Management** > **Preset Dictionary** in the [TMS console](https://console.cloud.tencent.com/cms/text/lib) and add them to the allowlist (preset).

### Does TMS provide any service to filter sensitive words on forums or in live rooms? Can I customize keywords?

- Yes. TMS offers large keyword dictionaries and machine learning models. It also features noise filtering with strong resistance to interference as well as text restoration from interference, making it very effective in recognizing different variants of non-compliant text.
- You can customize sensitive word dictionaries. Go to **Custom Library Management** > **Custom Dictionary** in the [TMS console](https://console.cloud.tencent.com/cms/text/lib), configure a custom dictionary, and add custom non-compliant words as instructed in [Configure a custom dictionary](https://intl.cloud.tencent.com/document/product/1121/43753#step5). After creating the custom dictionary, you need to create a [custom moderation policy](https://intl.cloud.tencent.com/document/product/1121/43753#step4) and bind the dictionary to the policy for the dictionary to take effect.