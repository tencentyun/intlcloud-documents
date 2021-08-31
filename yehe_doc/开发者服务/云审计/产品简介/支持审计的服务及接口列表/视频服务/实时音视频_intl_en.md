Based on Tencent's 21 years of experience in network and audio/video technologies, Tencent Real-Time Communication (TRTC) offers audio/video call and low-latency interactive live streaming solutions that suit different scenarios, helping you quickly develop cost-effective, low-latency, and high-quality interactive audio/video services.

TRTC operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|------------------------------|------|-------------------------------|
| Modifying permission key status                     | trtc | ChangeSecretKeyFlag           |
| trtcCreateMixConf            | trtc | CreateMixConf                 |
| Creating key on new version                       | trtc | CreateSecret                  |
| Generating signature with key                     | trtc | CreateSecretUserSig           |
| Adding Spear configuration                    | trtc | CreateSpearConf               |
| Creating exception information                       | trtc | CreateTroubleInfo             |
| Registering TRTC application                  | trtc | CreateTrtcApp                 |
| Uploading watermark image                       | trtc | CreateWatermark               |
| Deleting Spear configuration                    | trtc | DeleteSpearConf               |
| Deleting watermark image                       | trtc | DeleteWatermark               |
| Querying exceptional experience event                     | trtc | DescribeAbnormalEvent         |
| Getting the application list of user                  | trtc | DescribeAppStatList           |
| Getting the list of duration packages                    | trtc | DescribeDurationPackages      |
| Querying the number of historical rooms and users                   | trtc | DescribeHistoryScale          |
| trtcDescribeLiveList         | trtc | DescribeLiveList              |
| trtcDescribeMixConf          | trtc | DescribeMixConf               |
| Getting stream mix configurations of applications in batches                  | trtc | DescribeMixConfs              |
| Querying real-time network status                     | trtc | DescribeRealtimeNetwork       |
| Querying real-time quality data                     | trtc | DescribeRealtimeQuality       |
| Querying real-time scale                       | trtc | DescribeRealtimeScale         |
| Querying room list                       | trtc | DescribeRoomInformation       |
| trtcDescribeRoomList         | trtc | DescribeRoomList              |
| Getting `SkdAppID` information              | trtc | DescribeSdkAppInfo            |
| Getting key                         | trtc | DescribeSecret                |
| Getting legacy `Sig`                      | trtc | DescribeSig                   |
| Getting Spear configuration                    | trtc | DescribeSpearConf             |
| Getting application and account information                    | trtc | DescribeTrtcAppAndAccountInfo |
| trtcDescribeTrtcSdkAppIdList | trtc | DescribeTrtcSdkAppIdList      |
| Getting TRTC duration statistics                | trtc | DescribeTrtcStatistic         |
| Querying the status of the user in room                  | trtc | DescribeUserState             |
| Querying the status of the user in room                  | trtc | DescribeUserStateByStrRoomId  |
| Searching for watermark image                       | trtc | DescribeWatermark             |
| Dismissing room                         | trtc | DismissRoom                   |
| Dismissing room                         | trtc | DismissRoomByStrRoomId        |
| Dismissing room                         | trtc | DissolveRoom                  |
| Dismissing room                         | trtc | DissolveRoomByStrRoomId       |
| Getting call status                       | trtc | GetCommState                  |
| Querying ES data                       | trtc | GetElasticSearchData          |
| Getting room list                       | trtc | GetRoomList                   |
| Getting user information                       | trtc | GetUserInfo                   |
| Getting user list                       | trtc | GetUserList                   |
| Querying application stream mix configuration or automatically creating one if it does not exist          | trtc | HardDescribeMixConf           |
| Determine whether the upstream duration package can be purchased              | trtc | IfCanBuyOldPackage            |
| Determining whether the user is an `AvSdk` user               | trtc | IsAvSdkUser                   |
| Determining whether the user is a new TRTC user              | trtc | IsNewTrtcUser                 |
| Determining whether the `uin` is a TRTC user               | trtc | IsTrtcUser                    |
| Kicking out user                           | trtc | KickOutUser                   |
| Kicking out user                           | trtc | KickOutUserByStrRoomId        |
| Modifying application information                       | trtc | ModifyAppInfo                 |
| Modifying stream mix configuration parameter                     | trtc | ModifyMixConf                 |
| trtcModifyRecordMode         | trtc | ModifyRecordMode              |
| Modifying Spear configuration                    | trtc | ModifySpearConf               |
| Modifying watermark image                       | trtc | ModifyWatermark               |
| Removing user                         | trtc | RemoveUser                    |
| Removing user                         | trtc | RemoveUserByStrRoomId         |
| Displaying room list                       | trtc | ShowRoomList                  |
| Displaying user list                       | trtc | ShowUserList                  |
| Enabling On-Cloud MixTranscoding                       | trtc | StartMCUMixTranscode          |
| Ending On-Cloud MixTranscoding                       | trtc | StopMCUMixTranscode           |
| Switching key version                       | trtc | ToggleSecretVersion           |
| Switching Spear scenario                    | trtc | ToggleSpearScheme             |
| trtcUpdateNewUserStep        | trtc | UpdateNewUserStep             |
| Verifying signature (`UserSig`)                | trtc | VerifySecretUserSig           |
| Verifying old public/private key `Sig`                   | trtc | VerifySig                     |
