To help operations personnel determine whether the push (operation) goals are achieved, TPNS introduces the data overview feature that allows them to fully view the overall user conversion results brought by the pushes.
## Features
Log in to the [TPNS console](https://console.cloud.tencent.com/tpns). In the left sidebar, click **Data Overview** > **Push Statistics**.
The metrics on this page are described as follows:
1. **Used Yesterday**: app usage yesterday
![](https://main.qcloudimg.com/raw/dd17dad647411bcbcacce185a27378af.png)

- Messages Pushed Yesterday: the number of messages (PV) pushed in all tasks yesterday (messages pushed in inter-day tasks are counted into the day they are pushed)
- Push Tasks Yesterday: the total number of push tasks yesterday
- Devices Reached Yesterday: the number of unique devices (UV) that the pushed messages in all tasks reached yesterday (messages pushed in inter-day tasks are counted into the day they are pushed)
- DAU Yesterday: the number of unique online devices connected to the TPNS server yesterday (the SDK will connect to the TPNS server when the application is running in the frontend or backend)

2. **Application Status Monitoring**: monitors the application’s available devices, notification bar enablement, and uninstallation.
![](https://main.qcloudimg.com/raw/1b138213a593d9892c571b6e2e7deba1.png)
- Available Devices: the number of devices on which the app is not uninstalled within 90 days as of 24:00 yesterday (uninstalled devices include those returned unavailable by vendor/TPNS SDK)
- Uninstalled/Unavailable Devices: the number of devices offline over 90 consecutive days or devices returned unavailable by vendor/TPNS SDK
- Opt-In Devices: the number of devices on which the notification bar is enabled
- Opt-Out Devices: the number of devices on which the notification bar is disabled
- Opt-In Rate: Opt-In devices/Available devices
- Compare with "Tool" the Mobile Industry: the average opt-in rate of the current app industry (you can enter the product management page to view or modify the app industry)
  ![](https://main.qcloudimg.com/raw/0f8a15da5768d61c0c71dc9a9da160c6.png)
- Compare with Mobile Industry: the average opt-in rate of the whole mobile app industry
- Connected Devices Yesterday: the number of unique online devices connected to the TPNS yesterday (the SDK will connect to the TPNS server when the application is running in the frontend or backend)

3. **App Usage Trend**: app push usage over time, helping you analyze the push effect
**Android**:
![](https://main.qcloudimg.com/raw/804ffa41de4d4ea18ffb35309e8af34b.png)
- Attempted: the number of available and opt-in devices connected to the Internet within 90 days that meet the target push conditions
- Sent to: the total number of messages (PV) pushed every day
- Messages Reached (PV): the number of devices (PV) that received the push messages
- Messages Clicked: the number of times the notification bar message was clicked. This feature requires Android SDK 1.2.0.1 or later. This deduplicated number is obtained from TPNS acquisition and vendor's data receipt.
- Messages Cleared: the number of times the notification bar message was dismissed
- Message Click Rate: Messages clicked/Messages reached (PV)
- DAU: the number of unique online devices connected to the TPNS server on a day (the SDK will connect to the TPNS server when the application is running in the frontend or backend)
- Opt-In Devices: the number of devices on which the notification bar is enabled
- Uninstalled/Unavailable devices: the total number of devices offline over 90 consecutive days or devices returned unavailable by vendor/TPNS SDK.
- New Devices: the number of unique devices that got newly registered Token on the day

**iOS**:
![](https://main.qcloudimg.com/raw/250a12d9381b0f502c7fbee3999661fe.png)
- Attempted: the number of available devices that meet the target push conditions
- Sent to: the total number of messages (PV) pushed every day
- Messages Reached (PV): the number of devices (PV) that received the push messages
- Messages Clicked: the number of times the notification bar message was clicked
- Message Click Rate: Messages clicked/Messages reached (PV)
- DAU: the number of unique online devices connected to the TPNS server on a day (the SDK will connect to the TPNS server when the application is running in the frontend or backend)
- Opt-In Devices: the number of devices on which the notification bar is enabled (the notification bar status will be checked every 10 seconds. The change will be reported when the application is online in the frontend).
- Uninstalled/Unavailable devices: the total number of devices offline over 90 consecutive days or devices returned unavailable by vendor/TPNS SDK.
- New Devices: the number of unique devices that got newly registered Token on the day


