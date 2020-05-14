The data statistics feature of TPNS can help product OPS personnel quickly view whether the push (operation) goal is achieved in order to fully understand the overall user conversion in push scenarios.
## Feature Description
Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and click **Data Overview** on the left sidebar.
The metrics on this page are described as follows:
**1. Yesterday's usage data: you can view application usage statistics on yesterday.**

- Yesterday's push messages: total PV, which is the total number of actually delivered messages in all push tasks yesterday (actually delivered messages in cross-day tasks will be counted in daily actual pushes).
- Yesterday's push tasks: total number of push tasks yesterday.
- Yesterday's online devices: number of deduplicated online devices connected to the SDK yesterday (the SDK will connect to the TPNS server when the application is on the foreground or its backend process is online).

**2. Application status monitoring: you can monitor the application's effective devices, notification panel enablement information, and uninstallation information.**

- Valid devices: number of devices where the application was still installed in the last 90 days (uninstalled devices include the devices whose invalid state was returned by the vendor or TPNS SDK when the vendor channel API is called).
- Uninstalled devices: number of inactive devices or devices whose invalid state was returned by the vendor or TPNS SDK in the last 90 days.
- Devices with enabled notification panel: number of devices whose notification panel is enabled to receive push messages.
- Devices with disabled notification panel: number of devices whose notification panel is disabled to receive push messages.
- Enabled notification panel ratio: number of devices with enabled notification panel/number of valid devices.
- Industry average: average enabled notification panel ratio of applications in the industry of your application (you can enter the product management page to view or modify the application's industry).
  
- Mobile device average: average enabled notification panel ratio of mobile applications.

**3. Application usage trend: trend in application push usage is displayed to help you analyze the push effect.**

- Delivered messages (PV): daily total number of push messages (PV).
- Daily online devices: daily number of deduplicated online devices connecting to the SDK (the SDK will connect to the TPNS server when the application is on the foreground or its backend process is online).
- New devices: number of deduplicated devices with newly registered tokens today.

