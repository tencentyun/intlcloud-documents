TS over SRT directly transmits TS streams containing audio/video data using **SRT protocol**. The existing live streaming system is used for playback. TS over SRT is used as the standard push format for Haivision hardware and OBS.
In this mode, the SRT server parses TS streams, remuxes to RTMP streams, and forwards to the backend RTMP server.
![](https://main.qcloudimg.com/raw/0124f28a30572bb0b0f1b0f6fbcb8d86.png)

>! Using SRT for push will not increase the cost.

## Upstream Lag Rate Comparison
Using SRT to push streams reduces lag, as shown in the following figure:
![](https://main.qcloudimg.com/raw/c0bc00e4f081c142ed3c01ed8427d862.png)


## Packet Loss Rate Comparison
Using SRT to push streams optimizes upstream performance, resulting in better playback smoothness. The following shows the performance comparison of the Douyu app.
- Android: performance test data of push over SRT (test device — Mi 9):
![](https://main.qcloudimg.com/raw/6c174b5529010ba188b9b120c1f4d04f.png)
- iOS: performance test data of push over SRT (test device — iPhone XR):
![](https://main.qcloudimg.com/raw/3126fb6c2f2aa65b6be4e9692fad0c44.png)



## Packet Loss Prevention Comparison
Compared with QUIC, SRT reduces packet loss at the application layer under the same packet loss rate, thanks to its faster, more precise retransmission control and pacing mechanism for live streaming scenarios. When the packet loss rate is 50%, SRT can still guarantee stable transmission.

With the same linkage and the same live stream file on the push end, the packet loss rate reduces by 5% every five minutes when SRT is used. The following figure shows that the push frame rate of SRT is more stable.

## Live Push
### Access method
Live push supports using **port 9000** to push streams over SRT. You can [generate a push address](https://intl.cloud.tencent.com/document/product/267/31084) via the [Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)] in the CSS console and splice the address by following the rules below.

Tencent Cloud SRT push address:
```
srt://${rtmp-push-domain}:9000?streamid=#!::h=${rtmp-push-domain},r=${app}/${stream},txSecret=${txSecret},txTime=${txTime}
```

>! `$ {app}` is a variable and should be replaced with the actual value. Note that `$`, `{`, and `}` are not required.

### Implementation method
The SRT server remuxes TS streams to RTMP streams and forward them to the `${rtmp-push-domain}` domain.
Sample of OBS live stream code:

>! If you want to push streams over SRT, the OBS version cannot be lower than v25.0.


## Live Pull
Follow the general pull and playback process. For details, see [CSS Playback](https://intl.cloud.tencent.com/document/product/267/31559).



