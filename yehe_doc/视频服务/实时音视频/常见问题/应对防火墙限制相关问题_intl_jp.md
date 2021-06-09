### クライアントのNative SDKは、どのポートまたはドメイン名をホワイトリストに設定する必要がありますか？

ファイアウォールのポートは下表のとおりです。

|  TRTC SDK（Native） | ホワイトリスト項目 |
|---------|---------|
| TCPポート | 443、20166 |
| UDPポート | 8000、8080、16285、9000 |

ドメイン名ホワイトリスト：

<pre>
cloud.tim.qq.com
gz.file.myqcloud.com
avc.qcloud.com
yun.tim.qq.com
dldir1.qq.com
mlvbdc.live.qcloud.com
query.tencent-cloud.com
</pre>

 
### WebRTCは、どのポートまたはドメイン名をホワイトリストに設定する必要がありますか？

ファイアウォールのポートは下表のとおりです。

| WebRTC（H5） | ホワイトリスト項目 |
|---------|---------|
| TCPポート | 8687 |
| UDPポート | 8000；8080；8800；843；443；16285 |

ドメイン名ホワイトリスト：

<pre>
qcloud.rtc.qq.com
</pre>


### WeChat Mini Programは、どのドメイン名をホワイトリストに設定する必要がありますか？

&lt;trtc-room&gt; ドメイン名ホワイトリスト：

<pre>
https://official.opensso.tencent-cloud.com
https://yun.tim.qq.com
https://cloud.tencent.com
https://webim.tim.qq.com
https://query.tencent-cloud.com
</pre>


>!Tencent CloudサーバーのIPアドレスは、固定IPアドレスではなく動的に更新されるため、固定IPリストを提供することはできません。
