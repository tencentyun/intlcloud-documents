The data statistics feature of TPNS can help product OPS personnel quickly view whether the push (operation) goal is achieved in order to fully understand the overall user conversion in push scenarios.
## Feature Description
Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and click **Data Overview** on the left sidebar.
The metrics on this page are described as follows:
**1. Yesterday's usage data: you can view application usage statistics on yesterday.**
![](https://main.qcloudimg.com/raw/b8e869d1f0acce432486942657bcb5c5.png)

- Messages Pushed Yesterday: total PV, which is the total number of actually delivered messages in all push tasks yesterday (actually delivered messages in cross-day tasks will be counted in daily actual pushes).
- Push Tasks Yesterday: total number of push tasks yesterday.
- Connected Devices Yesterday: number of deduplicated online devices connected to the SDK yesterday (the SDK will connect to the TPNS server when the application is on the foreground or its backend process is online).

**2. Application status monitoring: you can monitor the application's effective devices, notification bar enablement information, and uninstallation information.**
![](https://main.qcloudimg.com/raw/d415d3196b345f3f697ff53c52f106cf.png)

- Available Devices: number of devices where the application was still installed in the last 90 days (uninstalled devices include the devices whose invalid state was returned by the vendor or TPNS SDK when the vendor channel API is called).
- Unavailable Devices: number of inactive devices or devices whose invalid state was returned by the vendor or TPNS SDK in the last 90 days.
- Opt-In Devices: number of devices whose notification bar is enabled to receive push messages.
- Opt-Out Devices: number of devices whose notification bar is disabled to receive push messages.
- Opt-In Rate: number of devices with enabled notification bar/number of valid devices.
- Compare with App Industry: average enabled notification bar ratio of applications in the industry of your application (you can enter the product management page to view or modify the application's industry).
  ![](https://main.qcloudimg.com/raw/473fa76a291d90627292e254557a5fd1.png)
- Mobile device average: average enabled notification bar ratio of mobile applications.

**3. Application usage trend: trend in application push usage is displayed to help you analyze the push effect.**
![](https://main.qcloudimg.com/raw/0c19b7e3222f1f5506d039bdbcb98e6a.png)

- Delivered Messages (PV): daily total number of push messages (PV).
- Daily Connected Devices: daily number of deduplicated online devices connecting to the SDK (the SDK will connect to the TPNS server when the application is on the foreground or its backend process is online).
- New Devices: number of deduplicated devices with newly registered tokens today.

