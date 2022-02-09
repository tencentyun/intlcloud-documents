This document describes how to use the offline log feature.

## Prerequisites
You have [connected your application](https://intl.cloud.tencent.com/document/product/1131/44496).

## Directions
1. Enable offline log when initializing the SDK.
<dx-codeblock>
:::  javascript
new Aegis({
	id: 'xxxxx',
	uin: '123456',
	offlineLog: true, // Enable offline log (disabled by default)
})
:::
</dx-codeblock>
The offline log feature stores the user data in `localstorage` and therefore may slightly compromise the user business performance. You can enable it based on your actual conditions.
2. Log in to the [RUM console](https://console.cloud.tencent.com/rum).
3. On the left sidebar, click **Offline Log** to enter the offline log page.
4. You need to listen on the user, so that when the user enters the page next time, the locally stored offline logs will be reported to the server in batches.
![](https://main.qcloudimg.com/raw/0d773e49207787745012bba1239204c6.png)
5. After getting the user's reported data, you can search for relevant logs.
![](https://main.qcloudimg.com/raw/c4b86e82c2d2c15daa00c494209b8a9e.png)


### Field
You can select the fields to be displayed in the offline log list.
![](https://main.qcloudimg.com/raw/e62d2d41bfe72a289e8c2c5b20df340a.png)

### Advanced search
- You can filter logs by project, log type, and time.
- You can filter logs by UIN, `sessionid`, `aid`, keyword, and blocked keyword.
- You can set offline listening, so that the system will automatically pull the offline logs under the specified `uin`/`aid` after offline log is configured.

### Log list
Long log collapsing: if collapsing is disabled, all information of a log will be displayed on one line. After it is enabled, up to 8 lines of information of a long log will be displayed.
