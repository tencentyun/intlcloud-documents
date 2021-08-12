Delayed playback is a feature that allows you to delay the playing of streams. It is mainly used in important live streaming events to allow organizers time to handle emergencies. You can enable this feature through parameter setting.

## Notes
You can enable delayed playback via two methods:
- Call the [playback delaying API](https://intl.cloud.tencent.com/document/product/267/30850).
- Add a `txDelayTime` parameter to the end of a **push URL**. For details, please see [Push Configuration](#push_delay).

>? The API method is not recommended because calling an API involves configuration caching, which makes it difficult to estimate when the feature takes effect. You are advised to enable the feature using the second method.

## Preparations
1. Activate [CSS](https://console.cloud.tencent.com/live?from=product-banner-use-lvb) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Log in to the CSS console, select [**Domain Management**](https://console.cloud.tencent.com/live/domainmanage), and click **Add Domain Name** to add a push domain name. For more information, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:push_delay)
## Push Configuration
1. Log in to the CSS console, go to **CSS Toolkit** > [**Address Generator**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator), select **Push Domain** for **Domain Type**, and click **Generate Address**.
![](https://main.qcloudimg.com/raw/025aeea991996ddc35e6b61341714282.png)
2. Add `txDelayTime` to the end of the push address, and push streams via OBS. For detailed directions, please see [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569).
![](https://main.qcloudimg.com/raw/11cc2aee28d263e5740b1b6d0701652f.png)
>! Set `txDelayTime` to the number of seconds for which you want to delay playback. The value must be an integer and cannot exceed 600.


## Delayed Playback
1. Log in to the CSS console, go to **CSS Toolkit** > [**Address Generator**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator), select **Playback Domain** for **Domain Type**, and click **Generate Address**.
2. Use [VLC](https://intl.cloud.tencent.com/document/product/267/32483), FFmpeg, or other tools for playback. For details, please see [CSS Playback](https://intl.cloud.tencent.com/document/product/267/31559).

 In the figure above, the delay time set for playback via the `txDelayTime` parameter in the push address is 30s, and the actual playback latency is 34s, which indicates that the delayed playback feature has taken effect.
