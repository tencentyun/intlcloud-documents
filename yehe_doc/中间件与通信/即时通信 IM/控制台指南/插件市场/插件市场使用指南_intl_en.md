>?The plugin marketplace integrates multiple cloud capabilities to enable more IM implementations. You can select a plugin as needed to quickly build a product with diversified features.

The plugin marketplace is currently in canary release. If there is no such switch, access it [here](https://console.cloud.tencent.com/im/plugin).

Currently available plugins include:

- Audio/Video call plugin
  - [tim_ui_kit_calling_plugin 0.3.3](https://pub.dev/packages/tim_ui_kit_calling_plugin)
- Vendor offline push plugin
  - [tim_ui_kit_push_plugin 0.3.3](https://pub.dev/packages/tim_ui_kit_push_plugin)

A plugin can be used in the following ways:

- In the [IM console](https://console.cloud.tencent.com/im/plugin), find the target plugin and click **Install**. Note that this operation will take effect in two minutes.

- In the client SDK, integrate the corresponding plugin SDK as instructed on the plugin details page.

### Billing

1. The audio/video call plugin and offline push plugin can be used for free after they are activated in the console.
2. IM and TRTC in the audio/video call plugin are charged.
3. For more information on the billing and call frequency of the offline push plugin, see the offline push integration documents of different vendors.

### Error codes
| Error Code | Description | Remarks |
|---------|---------|---------|
| 70130 | the configuration to use this plugin was not obtained | The application with the current `sdkappid` does not have permission to use the plugin, which needs to be enabled in the console. |
