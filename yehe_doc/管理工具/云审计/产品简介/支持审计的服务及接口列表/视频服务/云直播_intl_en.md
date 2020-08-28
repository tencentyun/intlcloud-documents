Relying on Tencent's powerful technical platforms, Tencent Cloud Live Video Broadcasting (LVB) opens up the underlying capabilities of core Tencent businesses such as Tencent Video to users, providing professional, stable, and fast live streaming access and distribution services that feature advantages such as low latency, high security, high performance, easy connection, multi-device compatibility, and support for multiple bitrates. It fully meets the audio/video requirements for ultra-low latency and ultra-high concurrence and provides Tencent's proprietary push and player SDKs, enabling you to customize your own push and playback applications.

LVB operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|---------------|------|-----------------------------|
| Delaying playback          | live | AddDelayLiveStream          |
| Adding domain name          | live | AddLiveDomain               |
| Adding watermark          | live | AddLiveWatermark            |
| Binding certificate to domain name        | live | BindLiveDomainCert          |
| Disabling real-time logging        | live | CloseRealTimeLogAnalysis    |
| Adding top speed codec configuration      | live | CreateLiveAiTranscodeConf   |
| Creating live streaming IM information      | live | CreateLiveAvcInfo           |
| Creating callback rule        | live | CreateLiveCallbackRule      |
| Creating callback template        | live | CreateLiveCallbackTemplate  |
| Adding certificate          | live | CreateLiveCert              |
| Adding domain name policy        | live | CreateLiveDomainStrategy    |
| Creating instance recording task      | live | CreateLiveInstantRecord     |
| Creating instant screencapturing task      | live | CreateLiveInstantSnapshot   |
| Creating recording task        | live | CreateLiveRecord            |
| Creating recording rule        | live | CreateLiveRecordRule        |
| Creating recording template        | live | CreateLiveRecordTemplate    |
| Creating screencapturing rule        | live | CreateLiveSnapshotRule      |
| Creating screencapturing template        | live | CreateLiveSnapshotTemplate  |
| Creating transcoding rule        | live | CreateLiveTranscodeRule     |
| Creating transcoding template        | live | CreateLiveTranscodeTemplate |
| Creating watermarking rule        | live | CreateLiveWatermarkRule     |
| Creating log topic        | live | CreateLogAnalysisTheme      |
| Adding pull configuration        | live | CreatePullStreamConfig      |
| Deleting callback rule        | live | DeleteLiveCallbackRule      |
| Deleting log topic        | live | DeleteLogAnalysisTheme      |
| Querying director list       | live | DescribeCasterList          |
| LVB Console homepage       | live | DescribeLiveQcloudCom       |
| Disconnecting live stream         | live | DropLiveStream              |
| Modifying room information of application     | live | ModifyLiveAvcAccountInfo    |
| Modifying or creating license | live | ModifyLiveLicense           |
| Modifying log topic        | live | ModifyLogAnalysisTheme      |
| Enabling real-time logging        | live | OpenRealTimeLogAnalysis     |
| Switching from old AVC application to new one     | live | UpDowngradeAvcInfo          |
