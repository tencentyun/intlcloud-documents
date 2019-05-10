## CallBackRuleInfo

Rule information

Referenced by: DescribeLiveCallbackRules.

| Name | Type | Description |
|------|------|-------|
| CreateTime | String | Rule creation time. |
| UpdateTime | String | Rule update time. |
| TemplateId | Integer | Template ID. |
| DomainName | String | Upstream domain name. |
| AppName | String | Upstream path. |

## CallBackTemplateInfo

Callback template information

Referenced by: DescribeLiveCallbackTemplate, DescribeLiveCallbackTemplates.

| Name | Type | Description |
|------|------|-------|
| TemplateId | Integer | Template ID. |
| TemplateName | String | Template name. |
| Description | String | Description information. |
| StreamBeginNotifyUrl | String | Stream starting callback URL. |
| StreamEndNotifyUrl | String | Stream ending callback URL. |
| StreamMixNotifyUrl | String | Stream mixing callback URL. |
| RecordNotifyUrl | String | Recording callback URL. |
| SnapshotNotifyUrl | String | Screencapture callback URL. |
| PornCensorshipNotifyUrl | String | Porn detection callback URL. |
| CallbackKey | String | Callback authentication key |

## CertInfo

Certificate information

Referenced by: DescribeLiveCert, DescribeLiveCerts.

| Name | Type | Description |
|------|------|-------|
| CertId | Integer | Certificate ID. |
| CertName | String | Certificate name. |
| Description | String | Description information. |
| CreateTime | String | Creation time in UTC format. |
| HttpsCrt | String | Certificate content. |
| CertType | Integer | Certificate type. <br/>0: Tencent Cloud-hosted certificate. <br/>1: User-added certificate. |
| CertExpireTime | String | Certificate expiration time in UTC format. |
| DomainList | Array of String | List of domain names that use this certificate. |

## DomainCertInfo

Domain name certificate information

Referenced by: DescribeLiveDomainCert.

| Name | Type | Description |
|------|------|-------|
| CertId | Integer | Certificate ID. |
| CertName | String | Certificate name. |
| Description | String | Description information. |
| CreateTime | String | Creation time in UTC format. |
| HttpsCrt | String | Certificate content. |
| CertType | Integer | Certificate type. <br/>0: Tencent Cloud-hosted certificate. <br/>1: User-added certificate. |
| CertExpireTime | String | Certificate expiration time in UTC format. |
| DomainName | String | Name of the domain name that uses this certificate. |
| Status | Integer | Certificate status |

## ForbidStreamInfo

Forbidden stream list

Referenced by: DescribeLiveForbidStreamList.

| Name | Type | Description |
|------|------|-------|
| StreamName | String | Stream name. |
| CreateTime | String | Creation time. |
| ExpireTime | String | Forbidding expiration time. |

## PlayAuthKeyInfo

Playback authentication key information

Referenced by: DescribeLivePlayAuthKey.

| Name | Type | Description |
|------|------|-------|
| DomainName | String | Domain name. |
| Enable | Integer | Whether to enable; 0: disabled; 1: enabled. |
| AuthKey | String | Authentication key. |
| AuthDelta | Integer | Validity period in seconds. |
| AuthBackKey | String | Authentication back key. |

## PublishTime

Push time

Referenced by: DescribeLiveStreamOnlineList.

| Name | Type | Description |
|------|------|-------|
| PublishTime | String | Push time <br/>In UTC format, for example: 2018-06-29T19:00:00Z. |

## PullStreamConfig

Pull configuration

Referenced by: DescribePullStreamConfigs.

| Name | Type | Description |
|------|------|-------|
| ConfigId | String | Pull configuration ID. |
| FromUrl | String | Source URL. |
| ToUrl | String | Target URL. |
| AreaName | String | Region name. |
| IspName | String | ISP name. |
| StartTime | String | Start time. <br/>In UTC format. <br/>For example: 2019-01-08T10:00:00Z. |
| EndTime | String | End time. <br/><br/>In UTC format. <br/>For example: 2019-01-08T10:00:00Z. |
| Status | String | 0: invalid, 1: initial status, 2: running, 3: pull failed, 4: paused. |

## PushAuthKeyInfo

Push authentication key information

Referenced by: DescribeLivePushAuthKey.

| Name | Type | Description |
|------|------|-------|
| DomainName | String | Domain name. |
| Enable | Integer | Whether to enable; 0: disabled; 1: enabled. |
| MasterAuthKey | String | Master authentication key. |
| BackupAuthKey | String | Backup authentication key. |
| AuthDelta | Integer | Validity period in seconds. |

## RecordParam

Recording template parameter

Referenced by: CreateLiveRecordTemplate, DescribeLiveRecordTemplate, DescribeLiveRecordTemplates, ModifyLiveRecordTemplate.

| Name | Type | Required | Description |
|------|------|----------|------|
| RecordInterval | Integer | No | Recording interval. <br/>In seconds, default value: 1800. <br/>Value range: 300-7200. <br/>This parameter is not valid for HLS, and a file is generated from push stream starting to push stream ending when HLS is recorded. |
| StorageTime | Integer | No | Recording storage duration. <br/>In seconds, value range: 0-5184000. <br/>0 means permanent storage. |
| Enable | Integer | No | Whether to enable recording in the current format; 0: no, 1: yes. Default value: 0. |

## RecordTemplateInfo

Recording template information

Referenced by: DescribeLiveRecordTemplate, DescribeLiveRecordTemplates.

| Name | Type | Description |
|------|------|-------|
| TemplateId | Integer | Template ID. |
| TemplateName | String | Template name. |
| Description | String | Description information. |
| FlvParam | [RecordParam](#RecordParam) | FLV recording parameters. |
| HlsParam | [RecordParam](#RecordParam) | HLS recording parameters. |
| Mp4Param | [RecordParam](#RecordParam) | MP4 recording parameters. |
| AacParam | [RecordParam](#RecordParam) | AAC recording parameters. |

## RuleInfo

Rule information

Referenced by: DescribeLiveRecordRules, DescribeLiveSnapshotRules, DescribeLiveTranscodeRules, DescribeLiveWatermarkRules.

| Name | Type | Description |
|------|------|-------|
| CreateTime | String | Rule creation time. |
| UpdateTime | String | Rule update time. |
| TemplateId | Integer | Template ID. |
| DomainName | String | Push domain name. |
| AppName | String | Push path. |
| StreamName | String | Stream name. |

## SnapshotTemplateInfo

Screencapture template information

Referenced by: DescribeLiveSnapshotTemplate, DescribeLiveSnapshotTemplates.

| Name | Type | Description |
|------|------|-------|
| TemplateId | Integer | Template ID. |
| TemplateName | String | Template name. |
| SnapshotInterval | Integer | Screencapture interval. Value range: 5-300 |
| Width | Integer | Screenshot width. Value range: 0-3000. 0: original width and fit to the original ratio |
| Height | Integer | Screenshot height. Value range: 0-2000. 0: original height and fit to the original ratio |
| PornFlag | Integer | Whether to enable porn detection; 0: disabled, 1: enabled. |
| CosAppId | Integer | COS AppId. |
| CosBucket | String | COS bucket name. |
| CosRegion | String | COS region. |
| Description | String | Template description |

## StreamEventInfo

Streaming event information

Referenced by: DescribeLiveStreamEventList.

| Name | Type | Description |
|------|------|-------|
| AppName | String | App name. |
| DomainName | String | Push domain name. |
| StreamName | String | Stream name. |
| StreamStartTime | String | Push start time. <br/>In UTC format. <br/>For example: 2019-01-07T12:00:00Z. |
| StreamEndTime | String | Push end time. <br/>In UTC format. <br/>For example: 2019-01-07T15:00:00Z. |
| StopReason | String | Stop reason. |
| Duration | Integer | Push duration in seconds. |
| ClientIp | String | VJ IP. |
| Resolution | String | Resolution. |

## StreamInfo

Push information

Referenced by: DescribeLiveStreamOnlineInfo.

| Name | Type | Description |
|------|------|-------|
| AppName | String | Name of the application to which the live stream belongs |
| CreateMode | String | Creation mode |
| CreateTime | String | Creation time, for example: 2018-07-13 14:48:23 |
| Status | Integer | Stream status |
| StreamId | String | Stream ID |
| StreamName | String | Stream name |
| WaterMarkId | String | Watermark ID |

## StreamName

Stream name list

Referenced by: DescribeLiveStreamPublishedList.

| Name | Type | Description |
|------|------|-------|
| StreamName | String | Stream name. |

## StreamOnlineInfo

Active push information query

Referenced by: DescribeLiveStreamOnlineList.

| Name | Type | Description |
|------|------|-------|
| StreamName | String | Stream name. |
| PublishTimeList | Array of [PublishTime](#PublishTime) | Push time list |
| AppName | String | App name. |
| DomainName | String | Push domain name. |

## TemplateInfo

Transcoding template information

Referenced by: DescribeLiveTranscodeTemplate, DescribeLiveTranscodeTemplates.

| Name | Type | Description |
|------|------|-------|
| Vcodec | String | Video encoding: <br/>h264/h265. |
| VideoBitrate | Integer | Video bit rate. Value range: 100-8000 Kbps |
| Acodec | String | Audio encoding: aac/mp3<br/>aac/mp3. |
| AudioBitrate | Integer | Audio bit rate. Value range: 0-500 |
| Width | Integer | Width. Value range: 0-3000 |
| Height | Integer | Height. Value range: 0-3000 |
| Fps | Integer | Frame rate. Value range: 0-200 |
| Gop | Integer | Keyframe interval in seconds. Value range: 1-50 |
| Rotate | Integer | Rotation angle. Value range: 0, 90, 180, 270 |
| Profile | String | Encoding quality: <br/>baseline/main/high. |
| BitrateToOrig | Integer | Whether to not exceed the original bit rate. 0: no, 1: yes.  |
| HeightToOrig | Integer | Whether to not exceed the original height. 0: no, 1: yes.  |
| FpsToOrig | Integer | Whether to not exceed the original fps. 0: no, 1: yes.  |
| NeedVideo | Integer | Whether to keep the video. 0: no, 1: yes.  |
| NeedAudio | Integer | Whether to keep the audio. 0: no, 1: yes.  |
| TemplateId | Integer | Template ID. |
| TemplateName | String | Template name |
| Description | String | Template description |

## WatermarkInfo


Watermark information

Referenced by: DescribeLiveWatermark, DescribeLiveWatermarks.

| Name | Type | Description |
|------|------|-------|
| WatermarkId | Integer | Watermark ID |
| PictureUrl | String | Watermark image URL. |
| XPosition | Integer | Display position; X-axis offset. |
| YPosition | Integer | Display position; Y-axis offset. |
| WatermarkName | String | Watermark name. |
| Status | Integer | Current status. 0: not used, 1: in use. |
| CreateTime | String | Creation time. |

