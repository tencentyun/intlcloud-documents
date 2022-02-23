用户使用StreamLive直播时移动服务前，需要先开通云直播CSS、媒体服务StreamLive。在云直播CSS将时移域名作为播放域名，按域名流程添加。



### 开通StreamPackage直播时移功能

[提交工单](https://console.cloud.tencent.com/workorder/category) 申请开通StreamLive时移能力。需要提供用户账号APPID、时移域名。


### 配置StreamLive直播时移

在工单配置好时移之后即可通过控制台或者API给StreamLive的OutputGroup开启时移能力。绑定时移域名。

>! 只有HLS_ARCHIVE和DASH_ARCHIVE才能开启时移。

1. 进入StreamLive控制台**Channel Management**页面，
2. 新建Channel，或选择要配置时移的频道，点击“**edit channel**”
3. 在“**Output settings page**”页面，将“**Basic Information**”-“**Out put Group Type**”设置成 **HLS_ARCHIVE / DASH_ARCHIVE** 
4. 在**TimeShift Information**栏目中，开启时移开关，并输入时移时长

>! 时移时长须介于300秒至1209600秒之间。

![](https://qcloudimg.tencent-cloud.cn/raw/46388651f1047edb0a1a8b8128ae2e02.png)
