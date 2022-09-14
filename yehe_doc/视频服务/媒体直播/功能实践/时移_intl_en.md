StreamLive supports time shifting for HLS and DASH streams. This feature must be used together with CSS.

Follow the steps below to configure time shifting:
1. Activate CSS. Add the domain for which you want to enable time shifting to the CSS console as a playback domain and add the CNAME record.
2. Submit a ticket to enable StreamLive’s time shifting feature. You need to provide your account’s AppID and the domain name for which you want to enable time shifting.
3. After time shifting is enabled for your account, in the **TimeShift Information** area of the **Output Group Setting** page, toggle on **Switch**, enter the domain name in **PlayDomain**, and specify the **Startover Window** (in seconds).
![](https://qcloudimg.tencent-cloud.cn/raw/661fcb79490e1de61a10b5d7ab90f494.png)

The format of a time-shifted playback URL is as follows:
- HLS: http://${play domain}/live/${region}_${Channel Id}-${p0 or p1}_${outputGroupName}/timeshift.m3u8?txMaster=1&delay={$delay}"
- DASH: http://${play domain}/live/${region}_${Channel Id}-${p0 or p1}_${outputGroupName}/timeshift.mpd?delay={$delay}"

>?
>- `${region}` is the region of the StreamLive channel. Valid values include `ap-bangkok`, `ap-mumbai`, `ap-seoul`, `ap-tokyo`, and `eu-frankfurt`.
>- `${delay}` is the time between the playback start time and the current time. It cannot be smaller than 180 seconds or larger than the startover window.



Examples:
- HLS: http://timeshift.domain.com/ap-bangkok_623ED795CD8247EDA2E1-p0_outputGroupName//timeshift.m3u8?txMaster=1&delay=180
- DASH: http://timeshift.domain.com/ap-bangkok_623ED795CD8247EDA2E1-p0_outputGroupName//timeshift.mpd?delay=180

