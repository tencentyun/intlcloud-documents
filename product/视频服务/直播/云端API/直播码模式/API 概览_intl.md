Tencent Cloud provides a set of LVB Code management APIs for your backend server, delivering status query, status management and other features.

### APIs

| API                                | Feature Description |
|---------------------------------|--------------------------------------------------------------|
| [Get_LiveStat](https://intl.cloud.tencent.com/document/api/267/6110)  | Statistics query - queries the push and playback information |
| [Get_LivePushStat](https://intl.cloud.tencent.com/document/api/267/6110) | Statistics query - queries the push information |
| [Get_LivePlayStat](https://intl.cloud.tencent.com/document/api/267/6110)  | Statistics query - queries the playback information |
| [Get_LivePushStatHistory](https://intl.cloud.tencent.com/document/product/267/9579)| Obtains the historical statistics of push |
| [Get_LivePlayStatHistory](https://intl.cloud.tencent.com/document/product/267/9580)| Obtains the historical statistics of playback |
| [Live_Channel_GetStatus](https://intl.cloud.tencent.com/document/api/267/5958) | Queries only the status information of a stream (old version API) | 
| [Live_Channel_SetStatus](https://intl.cloud.tencent.com/document/api/267/5959) | Bans an LVB stream. It is mainly used for porn detection. | 
| [Live_Tape_GetFilelist](https://intl.cloud.tencent.com/document/api/267/5960)| Queries the list of videos recorded during LVB for a certain stream | 
| [Live_Queue_Get](https://intl.cloud.tencent.com/document/api/267/5958)| Queries the list of screenshots captured during LVB for a certain stream |
| [Live_Channel_GetChannelList](https://intl.cloud.tencent.com/document/product/267/7997)| Queries the channel list |
| [Live_Channel_GetLiveChannelList](https://intl.cloud.tencent.com/document/product/267/8862)| Queries the channel list in LVB |
| [mix_streamv2.start_mix_stream_advanced](https://intl.cloud.tencent.com/document/product/267/8832)| API for stream mixing on the cloud |
| [channel_manager](https://intl.cloud.tencent.com/document/product/267/9500)| Stops pushing stream and delays the availability of API. It can disable push for a specified stream. |
| [Live_Tape_Start](https://intl.cloud.tencent.com/document/product/267/9567)| Creates a recording task. It supports scheduled recording and real-time recording. |
| [Live_Tape_Stop](https://intl.cloud.tencent.com/document/product/267/9568)| Ends a recording task |

### Error codes
1. HTTP error codes 

| Error Code | Description | Note |
|---------|---------|---------|
| 403 | Forbidden | Verification is enabled for the API to ensure security. If this error occurs when you perform verification via a browser, you can check whether skey is contained in cookie. |
| 404 | Not Found | Check whether the request comes with host |

2. Returned error codes

| Error Code | Description | Note |
|---------|---------|---------|
| appid is invalid | Invalid appid, which indicates the feature is not activated | <br>|

>**Note:**
>The above error codes apply to the APIs listed in this document and do not include [Event Message Notification](https://intl.cloud.tencent.com/document/product/267/5957).

 

