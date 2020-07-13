The data statistics feature of TPNS can help product OPS personnel quickly view whether the push (operation) goal is achieved in order to fully understand the overall user conversion in push scenarios.
## Feature Description
Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and click **Data Overview** on the left sidebar.
The metrics on this page are described as follows:
**1. Yesterday's usage data: you can view app usage statistics on yesterday.**
![](https://main.qcloudimg.com/raw/995c59fb99aff4dddaaf4e644a58ff13.png)
- Messages Pushed Yesterday: the total number of messages pushed by all push tasks (subject to the actual sent amount and not affected by the creation date of push tasks).
- Push Tasks Yesterday: the total number of push tasks yesterday.
- Connected Devices Yesterday: the number of unique devices of which SDK connected to TPNS server yesterday (SDK will be connected to TPNS server when app frontend or backend process is online).

**2. App status monitoring: you can monitor the app's effective devices, notification bar enablement information, and uninstallation information.**
![](https://main.qcloudimg.com/raw/29045d8efabc6ebdf56038742222014a.png)
- Available Devices: the number of devices on which the app is not uninstalled within 90 days as of 23:59 yesterday (the uninstalled indicates that vendor/TPNS SDK returns unavailable for that device).
- Uninstalled/Unavailable Devices: the number of offline devices over 90 days or devices that vendor/TPNS SDK returned unavailable.
- Opt-In Devices: the number of devices on which the notification bar is enabled.
- Opt-Out Devices: the number of devices on which the notification bar is disabled.
- Opt-In Rate: the current number of devices with notification bar enabled/the current number of available devices.
- Compare with App Industry: the opt-in rate of the current app industry (you can enter the product management page to view or modify the app industry).
  ![](https://main.qcloudimg.com/raw/cdcc47b7b7f02b84bc7eb727f229d74d.png)
- Compare with Mobile Industry: the opt-in rate of notification bar in the whole mobile app market.

**3. App usage trend: trend in app push usage is displayed to help you analyze the push effect.**
Android:
![](https://main.qcloudimg.com/raw/61ce80ed653cc2ec131de743a7ada613.png)
- Attempted: available devices in the push target devices
- Messages Sent (PV): the total number of messages pushed everyday
- Reached (PV): unique devices that received push messages
- Clicked: the number of times the notification was clicked
- Cleared: the number of times the notification was dismissed
- Daily Connected Devices: the number of daily unique devices of which the SDK connected to Internet (SDK connects to TPNS server when frontend is online or backend process is online)
- New Devices: the number of unique devices that got newly registered token on the day

iOS:
![](https://main.qcloudimg.com/raw/cd97cbbd3a31cec3639befb211b1886e.png)
- Attempted: available devices in the push target devices
- Messages Sent (PV): the total number of messages pushed everyday
- Reached (PV): unique devices that received push messages
- Clicked: the number of times the notification was clicked
- Daily Connected Devices: the number of daily unique devices of which the SDK connected to Internet (SDK connects to TPNS server when frontend is online or backend process is online)
- New Devices: the number of unique devices that got newly registered token on the day

