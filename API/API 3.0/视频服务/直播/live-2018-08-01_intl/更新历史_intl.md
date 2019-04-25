## Update 10

Release time: March 8, 2019 17:38:22

This release includes:

Improvements on existing documentation.

Modified APIs:

* [CreateLiveCallbackTemplate](/document/api/267/32637)
	* New input parameters: CallbackKey
* [ModifyLiveCallbackTemplate](/document/api/267/32631)
	* New input parameters: CallbackKey
	
Modified data structure:

* [CallBackTemplateInfo](/document/api/267/20474#CallBackTemplateInfo)
	* New members: CallbackKey

## Update 9

Release time: February 22, 2019 14:53:43

This release includes:

Improvements on existing documentation.

Newly added APIs:

* [DescribeLiveForbidStreamList](/document/api/267/33187)
* [DescribeLiveStreamEventList](/document/api/267/33186)

Newly added data structures:

* [ForbidStreamInfo](/document/api/267/20474#ForbidStreamInfo)
* [StreamEventInfo](/document/api/267/20474#StreamEventInfo)

## Update 8

Release time: January 18, 2019 19:51:10

This release includes:

Improvements on existing documentation.

New APIs:

* [BindLiveDomainCert](/document/api/267/32657)
* [CreateLiveCallbackRule](/document/api/267/32638)
* [CreateLiveCallbackTemplate](/document/api/267/32637)
* [CreateLiveCert](/document/api/267/32656)
* [CreateLiveRecordRule](/document/api/267/32615)
* [CreateLiveRecordTemplate](/document/api/267/32614)
* [CreateLiveSnapshotRule](/document/api/267/32625)
* [CreateLiveSnapshotTemplate](/document/api/267/32624)
* [CreateLiveTranscodeRule](/document/api/267/32647)
* [CreateLiveTranscodeTemplate](/document/api/267/32646)
* [CreateLiveWatermarkRule](/document/api/267/32629)
* [DeleteLiveCallbackRule](/document/api/267/32636)
* [DeleteLiveCallbackTemplate](/document/api/267/32635)
* [DeleteLiveCert](/document/api/267/32655)
* [DeleteLiveRecordRule](/document/api/267/32613)
* [DeleteLiveRecordTemplate](/document/api/267/32612)
* [DeleteLiveSnapshotRule](/document/api/267/32623)
* [DeleteLiveSnapshotTemplate](/document/api/267/32622)
* [DeleteLiveTranscodeRule](/document/api/267/32645)
* [DeleteLiveTranscodeTemplate](/document/api/267/32644)
* [DeleteLiveWatermarkRule](/document/api/267/32628)
* [DescribeLiveCallbackRules](/document/api/267/32634)
* [DescribeLiveCallbackTemplate](/document/api/267/32633)
* [DescribeLiveCallbackTemplates](/document/api/267/32632)
* [DescribeLiveCert](/document/api/267/32654)
* [DescribeLiveCerts](/document/api/267/32653)
* [DescribeLiveDomainCert](/document/api/267/32652)
* [DescribeLiveRecordRules](/document/api/267/32611)
* [DescribeLiveRecordTemplate](/document/api/267/32610)
* [DescribeLiveRecordTemplates](/document/api/267/32609)
* [DescribeLiveSnapshotRules](/document/api/267/32621)
* [DescribeLiveSnapshotTemplate](/document/api/267/32620)
* [DescribeLiveSnapshotTemplates](/document/api/267/32619)
* [DescribeLiveTranscodeRules](/document/api/267/32643)
* [DescribeLiveTranscodeTemplate](/document/api/267/32642)
* [DescribeLiveTranscodeTemplates](/document/api/267/32641)
* [DescribeLiveWatermark](/document/api/267/32627)
* [DescribeLiveWatermarkRules](/document/api/267/32626)
* [ModifyLiveCallbackTemplate](/document/api/267/32631)
* [ModifyLiveCert](/document/api/267/32651)
* [ModifyLiveDomainCert](/document/api/267/32650)
* [ModifyLiveRecordTemplate](/document/api/267/32608)
* [ModifyLiveSnapshotTemplate](/document/api/267/32618)
* [ModifyLiveTranscodeTemplate](/document/api/267/32640)
* [UnBindLiveDomainCert](/document/api/267/32649)

Modified APIs:

* [DescribeLiveStreamOnlineList](/document/api/267/20472)
	* New input parameters: StreamName
	* **Modified members:** DomainName
	
Newly added data structures:

* [CallBackRuleInfo](/document/api/267/20474#CallBackRuleInfo)
* [CallBackTemplateInfo](/document/api/267/20474#CallBackTemplateInfo)
* [CertInfo](/document/api/267/20474#CertInfo)
* [DomainCertInfo](/document/api/267/20474#DomainCertInfo)
* [RecordParam](/document/api/267/20474#RecordParam)
* [RecordTemplateInfo](/document/api/267/20474#RecordTemplateInfo)
* [RuleInfo](/document/api/267/20474#RuleInfo)
* [SnapshotTemplateInfo](/document/api/267/20474#SnapshotTemplateInfo)
* [TemplateInfo](/document/api/267/20474#TemplateInfo)

## Update 7

Release time: January 17, 2019 20:40:05

This release contains:

Improvements on existing documentation.

Modified data structure:

* [StreamOnlineInfo](/document/api/267/20474#StreamOnlineInfo)
	* New members: DomainName

## Update 6

Release time: January 10, 2019 20:11:53

This release includes:

Improvements on existing documentation.

Modified APIs:

* [CreatePullStreamConfig](/document/api/267/30159)
	* **Modified input parameters:** StartTime, EndTime
* [ModifyPullStreamConfig](/document/api/267/30157)
	* **Modified input parameters:** StartTime, EndTime
	
Modified data structure:

* [PullStreamConfig](/document/api/267/20474#PullStreamConfig)
	* **Modified members:** StartTime, EndTime
* [StreamOnlineInfo](/document/api/267/20474#StreamOnlineInfo)
	* New members: AppName

## Update 5

Release time: December 27, 2018 20:38:48

This release includes:

Improvements on existing documentation.

Modified APIs:

* [AddDelayLiveStream](/document/api/267/20465)
	* New input parameters: ExpireTime

## Update 4

Release time: December 6, 2018 19:05:52

This release includes:

Improvements on existing documentation.

Newly added APIs:

* [DeletePullStreamConfig](/document/api/267/31311)

Modified APIs:

* [ModifyLivePlayAuthKey](/document/api/267/30424)
	* New input parameters: AuthBackKey
	
Modified data structure:

* [PlayAuthKeyInfo](/document/api/267/20474#PlayAuthKeyInfo)
	* New members: AuthBackKey

## Update 3

Release time: November 15, 2018 15:42:56

This release includes:

Improvements on existing documentation.

Newly added APIs:

* [DescribeLivePlayAuthKey](/document/api/267/30426)
* [DescribeLivePushAuthKey](/document/api/267/30425)
* [ModifyLivePlayAuthKey](/document/api/267/30424)
* [ModifyLivePushAuthKey](/document/api/267/30423)

Newly added data structures:

* [PlayAuthKeyInfo](/document/api/267/20474#PlayAuthKeyInfo)
* [UpstreamAuthKeyInfo](/document/api/267/20474#UpstreamAuthKeyInfo)

## Update 2

Release time: October 26, 2018  14:29:15

This release includes:

Improvements on existing documentation.

Newly added APIs:

* [AddLiveWatermark](/document/api/267/30154)
* [CreateLiveRecord](/document/api/267/30148)
* [CreatePullStreamConfig](/document/api/267/30159)
* [DeleteLiveRecord](/document/api/267/30147)
* [DeleteLiveWatermark](/document/api/267/30153)
* [DescribeLiveWatermarks](/document/api/267/30152)
* [DescribePullStreamConfigs](/document/api/267/30158)
* [ModifyPullStreamConfig](/document/api/267/30157)
* [ModifyPullStreamStatus](/document/api/267/30156)
* [SetLiveWatermarkStatus](/document/api/267/30151)
* [StopLiveRecord](/document/api/267/30146)
* [UpdateLiveWatermark](/document/api/267/30150)

Newly added data structures:

* [PullStreamConfig](/document/api/267/20474#PullStreamConfig)
* [WatermarkInfo](/document/api/267/20474#WatermarkInfo)

## Update 1

Release time: October 11, 2018 19:44:12

This release includes:

Improvements on existing documentation.

Newly added APIs:

* [AddDelayLiveStream](/document/api/267/20465)
* [DescribeLiveStreamOnlineInfo](/document/api/267/20473)
* [DescribeLiveStreamOnlineList](/document/api/267/20472)
* [DescribeLiveStreamPublishedList](/document/api/267/20471)
* [DescribeLiveStreamState](/document/api/267/20470)
* [DropLiveStream](/document/api/267/20469)
* [ForbidLiveStream](/document/api/267/20468)
* [ResumeDelayLiveStream](/document/api/267/20464)
* [ResumeLiveStream](/document/api/267/20467)

Newly added data structures:

* [PublishTime](/document/api/267/20474#PublishTime)
* [StreamInfo](/document/api/267/20474#StreamInfo)
* [StreamName](/document/api/267/20474#StreamName)
* [StreamOnlineInfo](/document/api/267/20474#StreamOnlineInfo)

