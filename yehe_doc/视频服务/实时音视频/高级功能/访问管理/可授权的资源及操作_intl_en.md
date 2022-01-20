>!This document describes the management of access to **TRTC**. For access management of other Tencent Cloud services, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

In essence, CAM enables you to **allow or forbid specified accounts to access certain resources**. TRTC access management supports [resource-level authorization](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B). The granularity of manageable resources is [TRTC applications](https://intl.cloud.tencent.com/document/product/647/37714), and the granularity of authorizable actions is [TencentCloud APIs](https://intl.cloud.tencent.com/product/api), including [server APIs](https://intl.cloud.tencent.com/document/product/647/34260) and APIs that may be needed to access the TRTC console.

If you need to manage access to TRTC, please log in to the console with a Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/34899) and use a [preset policy](https://intl.cloud.tencent.com/document/product/647/39550) or a [custom policy](https://intl.cloud.tencent.com/document/product/647/39551) to grant permissions.


## Type of Manageable Resources
- TRTC access management allows you to control access to [applications](https://intl.cloud.tencent.com/document/product/647/37714).


## APIs Supporting Resource-Level Authorization[](id:Support)
Barring a [few exceptions](#n_Support), all API actions listed in this section support resource-level authorization. Authorization policies related to these API actions use the same [**syntax conventions**](https://intl.cloud.tencent.com/document/product/647/39551#grammar). See below for details.
- Authorizing access to all applications: `qcs::trtc::uin/${uin}:sdkappid/*`
- Authorizing access to single applications: `qcs::trtc::uin/${uin}:sdkappid/${SdkAppId}`.

#### Server API actions
| API                                                     | Category     | Description               |
| ------------------------------------------------------------ | ------------ | ---------------------- |
| [DismissRoom](https://intl.cloud.tencent.com/document/product/647/39631) | Room management     | Closes a room.               |
| [RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) | Room management     | Removes a user.               |
|[RemoveUserByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39630)	| Room management	| Removes a user (string room ID). |
|[DismissRoomByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39631)	| Room management	| Closes a room (string room ID). |
| [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) | Stream mixing and transcoding     | Starts On-Cloud MixTranscoding.           |
| [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) | Stream mixing and transcoding     | Stops On-Cloud MixTranscoding.       |
| [StartMCUMixTranscodeByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39637) | Stream mixing and transcoding | Starts On-Cloud MixTranscoding (string room ID). |
| [StopMCUMixTranscodeByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39636) | Stream mixing and transcoding | Stops On-Cloud MixTranscoding (string room ID). |
| [CreateTroubleInfo](https://intl.cloud.tencent.com/document/product/647/37764) | Call quality monitoring | Generates information about exceptional conditions.           |
| [DescribeAbnormalEvent](https://intl.cloud.tencent.com/document/product/647/37763) | Call quality monitoring | Queries abnormal events.       |
| [DescribeCallDetail](https://intl.cloud.tencent.com/document/product/647/36759) | Call quality monitoring | Queries user list and call metrics. |
| [DescribeHistoryScale](https://intl.cloud.tencent.com/document/product/647/36758) | Call quality monitoring | Queries room and user numbers in the past.   |
| DescribeRealtimeNetwork | Call quality monitoring | Queries network conditions in real time.       |
| DescribeRealtimeQuality | Call quality monitoring | Queries quality data in real time.       |
| DescribeRealtimeScale | Call quality monitoring | Queries room and user numbers in real time.           |
| [DescribeRoomInformation](https://intl.cloud.tencent.com/document/product/647/36754) | Call quality monitoring | Queries room list.           |
| [DescribeUserInformation](https://intl.cloud.tencent.com/document/product/647/39096) | Call quality monitoring | Queries the list of historical users. |




### Console API actions
<table>
<thead><tr><th >API</th><th>Console</th><th width="38%">Description</th></tr></thead>
<tbody><tr>
<td>DescribeAppStatList</td>
<td>TRTC console:<ul style="margin:0">
<li> <a href="https://console.cloud.tencent.com/trtc">Overview</a> 
<li><a href="https://console.cloud.tencent.com/trtc/statistics">Usage Statistics</a>
<li><a href="https://console.cloud.tencent.com/trtc/monitor">Monitoring Dashboard</a>
<li><a href="https://console.cloud.tencent.com/trtc/usersigtool">Development Assistance &gt; UserSig Generation &amp; Verification</a> 
<li><a href="https://console.cloud.tencent.com/trtc/app">Application Management</a>
</ul></td>
<td>Gets application list.</td>
</tr><tr>
<td>DescribeSdkAppInfo</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Application Info</a></td>
<td>Gets application information.</td>
</tr><tr>
<td>ModifyAppInfo</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Application Info</a></td>
<td>Modifies application information.</td>
</tr><tr>
<td>ChangeSecretKeyFlag</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Application Info</a></td>
<td>Enables/Disables encryption keys.</td>
</tr><tr>
<td>CreateWatermark</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Material Management</a></td>
<td>Uploads an image.</td>
</tr><tr>
<td>DeleteWatermark</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Material Management</a></td>
<td>Deletes an image.</td>
</tr><tr>
<td>ModifyWatermark</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Material Management</a></td>
<td>Edits an image.</td>
</tr><tr>
<td>DescribeWatermark</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Material Management</a></td>
<td>Searches an image.</td>
</tr><tr>
<td>CreateSecret</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Quick Start</a></td>
<td>Generates a symmetric encryption key.</td>
</tr><tr>
<td>ToggleSecretVersion</td>
<td>TRTC console:<a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Quick Start</a></td>
<td>Switches between asymmetric keys (private and public keys) and symmetric keys.</td>
</tr><tr>
<td>DescribeSecret</td>
<td>TRTC console:<ul style="margin:0">
<li><a href="https://console.cloud.tencent.com/trtc/quickstart">Development Assistance &gt; Demo Quick Run</a>
<li><a href="https://console.cloud.tencent.com/trtc/usersigtool">Development Assistance &gt; UserSig Generation &amp; Verification</a>
<li><a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Quick Start</a>
</ul></td>
<td>Gets a symmetric encryption key.</td>
</tr><tr>
<td>DescribeTrtcAppAndAccountInfo</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/usersigtool">Development Assistance &gt; UserSig Generation &amp; Verification</a></td>
<td>Gets application and account information to obtain a pair of public and private keys.</td>
</tr><tr>
<td>CreateSecretUserSig</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/usersigtool">Development Assistance &gt; UserSig Generation &amp; Verification</a></td>
<td>Uses a symmetric encryption key to generate a UserSig.</td>
</tr><tr>
<td>DescribeSig</td>
<td>TRTC console:<ul style="margin:0">
<li><a href="https://console.cloud.tencent.com/trtc/usersigtool">Development Assistance &gt; UserSig Generation &amp; Verification</a>
<li> <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Quick Start</a>
</ul></td>
<td>Gets a UserSig generated using a pair of public and private keys.</td>
</tr><tr>
<td>VerifySecretUserSig</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/usersigtool">Development Assistance &gt; UserSig Generation &amp; Verification</a></td>
<td>Verifies a UserSig generated using a symmetric encryption key.</td>
</tr><tr>
<td>VerifySig</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/usersigtool">Development Assistance &gt; UserSig Generation &amp; Verification</a></td>
<td>Verifies a UserSig generated using a pair of public and private keys.</td>
</tr>
<tr>
<td>CreateSpearConf</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Image Settings</a></td>
<td>Adds an image setting. This module is available only in iLiveSDK 1.9.6 and earlier versions. For TRTC SDK 6.0 and later versions, see <a href="https://intl.cloud.tencent.com/document/product/647/35153">Setting Image Quality</a></td>
</tr>
<tr>
<td>DeleteSpearConf</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Image Settings</a></td>
<td>Deletes an image setting. This module is available only in iLiveSDK 1.9.6 and earlier versions. For TRTC SDK 6.0 and later versions, see <a href="https://intl.cloud.tencent.com/document/product/647/35153">Setting Image Quality</a></td>
</tr>
<tr>
<td>ModifySpearConf</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Image Settings</a></td>
<td>Modifies image settings. This module is available only in iLiveSDK 1.9.6 and earlier versions. For TRTC SDK 6.0 and later versions, see <a href="https://intl.cloud.tencent.com/document/product/647/35153">Setting Image Quality</a></td>
</tr>
<tr>
<td>DescribeSpearConf</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Image Settings</a></td>
<td>Gets image settings. This module is available only in iLiveSDK 1.9.6 and earlier versions. For TRTC SDK 6.0 and later versions, see <a href="https://intl.cloud.tencent.com/document/product/647/35153">Setting Image Quality</a></td>
</tr>
<tr>
<td>ToggleSpearScheme</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Image Settings</a></td>
<td>Switches image setting scenarios. This module is available only in iLiveSDK 1.9.6 and earlier versions. For TRTC SDK 6.0 and later versions, see <a href="https://intl.cloud.tencent.com/document/product/647/35153">Setting Image Quality</a></td>
</tr>
</tbody></table>


## APIs Not Supporting Resource-Level Authorization[](id:n_Support)
Due to special restrictions, the following APIs do not support resource-level authorization.

#### Server API actions
|API|Category|Description|Restriction|
|---|---|---|---|
|[DescribeDetailEvent](https://intl.cloud.tencent.com/document/product/647/37762)|Call quality monitoring|Queries specific events.|The parameters entered do not include `SDKAppID`, making resource-level authorization impossible.|
| [DescribeRecordStatistic](https://intl.cloud.tencent.com/document/product/647/42972) | Other APIs | Queries the billing period of on-cloud recording. | For business reasons, resource-level authorization is not supported currently. |
| [DescribeTrtcInteractiveTime](https://intl.cloud.tencent.com/document/product/647/42971) | Other APIs | Queries the billing period for audio/video interactive features. | For business reasons, resource-level authorization is not supported currently. |
| [DescribeTrtcMcuTranscodeTime](https://intl.cloud.tencent.com/document/product/647/42970) | Other APIs | Queries the billing period of relayed transcoding. | For business reasons, resource-level authorization is not supported currently. |

### Console API actions
<table>
<thead><tr><th>API</th><th width="20%">Console</th><th width="15%">Description</th><th>Restriction</th></tr></thead>
<tbody><tr>
<td>DescribeTrtcStatistic</td>
<td>TRTC console:<ul style="margin:0">
<li><a href="https://console.cloud.tencent.com/trtc">Overview</a> 
<li><a href="https://console.cloud.tencent.com/trtc/statistics">Usage Statistics</a>
</ul></td>
<td>Gets usage statistics.</td>
<td>This API returns the statistics of all `SDKAppIDs`. Limiting a query to specific `SDKAppIDs` will lead to an error. You can use `DescribeAppStatList` to specify a list of applications to query.</td>
</tr>
<tr>
<td>DescribeDurationPackages</td>
<td>TRTC console:<ul style="margin:0">
<li> <a href="https://console.cloud.tencent.com/trtc">Overview</a>
<li><a href="https://console.cloud.tencent.com/trtc/package">Package Management</a>
</ul></td>
<td>Gets the list of prepaid packages.</td>
<td>A prepaid package is shared by all TRTC applications under the same Tencent Cloud account. There is no `SDKAppID` parameter in the package information, so resource-level authorization cannot be performed.</td>
</tr>
<tr>
<td>GetUserList</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/monitor">Monitoring Dashboard</a></td>
<td>Gets user list.</td>
<td>The parameters entered do not include `SDKAppID`, making resource-level authorization impossible. You can use `DescribeAppStatList` to specify a list of applications to query.</td>
</tr>
<tr>
<td>GetUserInfo</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/monitor">Monitoring Dashboard</a></td>
<td>Gets user information.</td>
<td>The parameters entered do not include `SDKAppID`, making resource-level authorization impossible. You can use `DescribeAppStatList` to specify a list of applications to query.</td>
</tr>
<tr>
<td>GetCommState</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/monitor">Monitoring Dashboard</a></td>
<td>Gets call status.</td>
<td>The parameters entered do not include `SDKAppID`, making resource-level authorization impossible. You can use `DescribeAppStatList` to specify a list of applications to query.</td>
</tr>
<tr>
<td>GetElasticSearchData</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/monitor">Monitoring Dashboard</a></td>
<td>Queries Elasticsearch data.</td>
<td>The parameters entered do not include `SDKAppID`, making resource-level authorization impossible. You can use `DescribeAppStatList` to specify a list of applications to query.</td>
</tr>
<tr>
<td>CreateTrtcApp</td>
<td>TRTC console: <ul>
<li><a href="https://console.cloud.tencent.com/trtc/quickstart">Development Assistance &gt; Demo Quick Run</a> 
<li><a href="https://console.cloud.tencent.com/trtc/app">Application Management</a>
</ul></td>
<td>Creates a TRTC application.</td>
<td>The parameters entered do not include `SDKAppID`, making resource-level authorization impossible. `SDKAppID` is the unique ID of a TRTC application and is generated after application creation. </td>
</tr>
<tr>
<td>HardDescribeMixConf</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Function Configuration</a></td>
<td>Queries relayed push status.</td>
<td>The parameters entered do not include `SDKAppID`, making resource-level authorization impossible. You can use `DescribeAppStatList` to specify a list of applications to query.</td>
</tr>
<tr>
<td>ModifyMixConf</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/app">Application Management &gt; Function Configuration</a></td>
<td>Enables/Disables relayed push.</td>
<td>The parameters entered do not include `SDKAppID`, making resource-level authorization impossible. You can use `DescribeAppStatList` to specify a list of applications to query.</td>
</tr>
<tr>
<td>RemindBalance</td>
<td>TRTC console: <a href="https://console.cloud.tencent.com/trtc/package">Package Management</a></td>
<td>Gets the balance alarm information of a prepaid package.</td>
<td>A prepaid package is shared by all TRTC applications under the same Tencent Cloud account. There is no `SDKAppID` parameter in the package information, so resource-level authorization cannot be performed.</td>
</tr>
</tbody></table>

>!You can use a [custom policy](https://intl.cloud.tencent.com/document/product/647/39551) to control access to an API that does not support resource-level authorization. In the policy statement, set the resource element to `*`.
