The Aegis SDK uses flog to manage offline logs. You can use the offline log feature with simple configuration.


1. Enable the offline log parameter in the SDK.
<dx-codeblock>
:::  js
new Aegis({
  id: '', // Reporting key that you applied for on the TAM platform
  uin: 'xxxx', // `uin` must be set to report offline logs. If it cannot be obtained in the beginning, you can use `setConfig` to set it later
  offlineLog: true, // Enable offline log
})
:::
</dx-codeblock>
After offline log is enabled, user logs will be collected to IndexedDB of the browser but won't be reported in real time. To report them, you need to listen on the user UIN.
2. Log in to the [RUM console](https://console.cloud.tencent.com/rum), go to the **Offline Log** page, click **Set Offline Listening**, and enter the target user UIN for listening.
![](https://main.qcloudimg.com/raw/12e4608aee8a33e681132f4677fdc727.png)
3. The next time the user opens a page or `setConfig` is executed in the code, a log will be reported to the RUM server, and two APIs will be called on the user side:
	-  `aegis.qq.com/collect/offlineAuto`: determines whether to send an offline log and returns the encryption token.
	-   `aegis.qq.com/collect/offlineLog`: reports the offline logs stored in IndexedDB.
4. Click the drop-down list, select the target offline log, and click **Search** to view it.
![](https://main.qcloudimg.com/raw/7b103d2881ba0e6f8521ec9800ebbc76.png)
