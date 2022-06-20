### クライアントのNative SDKは、どのポートまたはドメイン名をホワイトリストに設定する必要がありますか？

ファイアウォールのポートは下表のとおりです：

|  TRTC SDK (Native) | ホワイトリスト項目 |
|---------|---------|
| TCPポート | 443、20166、10443、10444、10445、10446、10447、10448、10449、10450、10451、13275、23275、33000、37528 |
| UDPポート | 8000、8080、8001、8002、8003、8004、8005、8006、8007、8008、8009、16285、9000 |

ドメイン名ホワイトリスト：

```
intl-query.trtc.tencent-cloud.com
intl-accelerate.trtc.tencent-cloud.com
trtc-client-log-overseas-1258344699.cos.ap-singapore.myqcloud.com
intl-sdklog.trtc.tencent-cloud.com
sdkdc.live.qcloud.com
speedtestint.trtc.tencent-cloud.com
intl-query.trtc.tencent-cloud.com
hwapi.im.qcloud.com
videoapi-sgp.im.qcloud.com
trtc-sdk-config-1258344699.file.myqcloud.com         
```

 
### WebRTCは、どのポートまたはドメイン名をホワイトリストに設定する必要がありますか？

ファイアウォールのポートは下表のとおりです：

| WebRTC（H5） | ホワイトリスト項目 |
|---------|---------|
| TCPポート | 8687 |
| UDPポート | 8000；8080；8800；843；443；16285 |

ドメイン名ホワイトリスト：

```
intl-signaling.rtc.qq.com
intl-signaling.rtc.qcloud.com
intl-schedule.rtc.qq.com
intl-schedule.rtc.qcloud.com
videoapi-sgp.im.qcloud.com
```

### TRTC Web端末のプライベートネットワーク環境ではどのようにプロキシを設定しますか？
Nginx+coturnプロキシスキームを使用できます。詳細については、[企業プライベートネットワークプロキシスキーム](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-34-advanced-proxy.html)をご参照ください。

| 方法名 | 適用ケース                             | ネットワーク要件                          |
| :----- | :----------------------------------- | :-------------------------------- |
| 方法1 | クライアントに特定のパブリックネットワークのプロキシサーバーへのアクセスを許可する   | クライアントにパブリックネットワークのproxy serverへのアクセスを許可する |
| 方法2 | クライアントにプライベートネットワークのプロキシサーバーを通じてのパブリックネットワークへのアクセスを許可する | proxy serverのパブリックネットワークアクセスを許可する        |


