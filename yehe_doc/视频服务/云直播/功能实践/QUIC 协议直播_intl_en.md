QUIC (Quick UDP Internet Connections) is a next-generation transport layer network protocol over UDP and designed by Google. In 2018, IETF decided to make QUIC a worldwide standard of HTTP/3 network. QUIC outperforms TCP in data transport scenarios with poor network and high packet loss rate.

Currently, Tencent Video Cloud supports using the QUIC protocol for [live push](#push) and [live pull](#play).

## Supported Versions

CSS supports QUIC v39, v41, v42, v43, v44.

> ! QUIC v43 is recommended.

## Notes

To use QUIC for pull, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to require Tencent Cloud to allow pull using QUIC protocol via corresponding pull domain names.


## Live Push

[](id:push)

### How to push
Live push supports using the RTMP over QUIC protocol to push streams via UDP port 1935. Same as using the RTMP over TCP protocol, you can use the [Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) to [generate a push URL](https://intl.cloud.tencent.com/document/product/267/31084) in the CSS console.

![](https://main.qcloudimg.com/raw/31d20b09de1c8d3c9748872e59f9a828.png)


Push streams in either of the following ways:

- **Use Tencent Cloud [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38150)**: same as when the RTMP over TCP protocol is used, the SDK will use QUIC protocol to push streams to Tencent Cloud.
- **Use your own QUIC client**: you can use a standard push URL to push using the QUIC protocol. The push URLs using the RTMP over QUIC protocol and RTMP over TCP protocol are the same. The former will connect to Tencent Cloud’s QUIC push server. 

[](id:pushtest)


## Live Pull

[](id:play)

### How to pull

Live pull supports using the HTTP over QUIC protocol to pull streams via UDP port 443. Same as using the HTTP-FLV protocol, you can use the [Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) to [generate a pull URL](https://intl.cloud.tencent.com/document/product/267/31084) in the CSS console.
![](https://main.qcloudimg.com/raw/e4727db59f2e195abdd9382456212d14.png)

[](id:playtest)

### Pull test

You can use the Tencent Cloud [TCPlayerDemo](https://imgcache.qq.com/open/qcloud/video/vcplayer/demo/tcplayer-test.html) to test the pull.
> ? Chrome supports QUIC protocol requests, so you can use Tencent Cloud TCPlayerDemo in the Chrome browser to verify whether the QUIC protocol is used for playback.

1. Enable QUIC protocol in the Chrome browser.
   Enter `chrome://flags/#enable-quic` in the Chrome address bar, select **Enabled** for **Experimental QUIC protocol**, and restart Chrome.
   ![](https://main.qcloudimg.com/raw/b5aee3532ef918518206b607cc2d8f53.png) 
2. Open TCPlayerDemo. You’re advised to enter an FLV or HLS pull URL as the HTTPS playback URL. You cannot use an RTMP URL as it can only be played back on the Flash player. Click ![](https://main.qcloudimg.com/raw/5886ad8b68619d7ba99268e0a4e24f2c.png) to start the playback.
![](https://main.qcloudimg.com/raw/a2e4d83ca259b97b4376875215015a22.png)
3. Click the **Network** tab in Chrome’s Developer Tools. You will see that the protocol for the request is `http/2+quic/46`.
![](https://main.qcloudimg.com/raw/e1e61b7ae544881b898ccd7aa116e8a4.png)

> ? 
> - The QUIC version may vary depending on the browser version.
> - If **Protocol** is not displayed, you can right-click and select **Protocol** to display it.
> ![](https://main.qcloudimg.com/raw/ee21e41e7f61e87dccb2f2509ff7678d.png)
