StreamLive支持HLS&DASH时移，需要搭配云直播CSS一起配合使用。

时移配置步骤如下：
1. 开通云直播CSS，在云直播CSS将时移域名作为播放域名添加，并配置好CNAME。
2. 提交工单申请开通StreamLive时移能力，需要提供用户账号APPID、时移域名。
3. 等后端配置开通后，在Channel的**TimeShift Information**中打开**Switch**开关，将时移域名填写到**PlayDomain**，配置时移时长**Startover Window**（单位为秒）。
![](https://qcloudimg.tencent-cloud.cn/raw/661fcb79490e1de61a10b5d7ab90f494.png)

时移播放地址格式：
- HLS：http://${play domain}/live/${region}_${Channel Id}-${p0 or p1}_${outputGroupName}/timeshift.m3u8?txMaster=1&delay={$delay}"
- DASH：http://${play domain}/live/${region}_${Channel Id}-${p0 or p1}_${outputGroupName}/timeshift.mpd?delay={$delay}"

>?
>- ${region}对应StreamLive的Channel所属地域。映射关系为：Bangkok -> ap-bangkok；Mumbai -> ap-mumbai；Seoul->ap-seoul；Tokyo->ap-tokyo；Frankfurt->eu-frankfurt。
>- ${delay}为时移间隔，单位为秒。最小值为180，最大值为Startover Window。



例子：
- HLS：http://timeshift.domain.com/ap-bangkok_623ED795CD8247EDA2E1-p0_outputGroupName//timeshift.m3u8?txMaster=1&delay=180
- DASH：http://timeshift.domain.com/ap-bangkok_623ED795CD8247EDA2E1-p0_outputGroupName//timeshift.mpd?delay=180

