### クライアントのNative SDKは、どのポートまたはドメイン名をホワイトリストに設定する必要がありますか。

ファイアウォールのポートは下表のとおりです。

|  TRTC SDK（Native） | ホワイトリスト項目 |
|---------|---------|
| TCPポート | 443、20166 |
| UDP ポート | 8000、8080、16285、9000 |

ドメイン名ホワイトリスト：

```
cloud.tim.qq.com
gz.file.myqcloud.com
avc.qcloud.com
yun.tim.qq.com
dldir1.qq.com
mlvbdc.live.qcloud.com
query.tencent-cloud.com
```


### WebRTCは、どのポートまたはドメイン名をホワイトリストに設定する必要がありますか。

ファイアウォールのポートは下表のとおりです。

| WebRTC（H5） | ホワイトリスト項目 |
|---------|---------|
| TCPポート | 8687 |
| UDPポート | 8000；8080；8800；843；443；16285 |

ドメイン名ホワイトリスト：

```
*.rtc.qq.com
yun.tim.qq.com
```

## TRTC Web端末のプライベートネットワーク環境ではどのようにプロキシを設定しますか。
Nginx+coturnプロキシソリューションを使用できます。

| 方法名 | 適用ケース                             | ネットワーク要件                          |
| :----- | :----------------------------------- | :-------------------------------- |
| 方法1 | クライアントに特定のパブリックネットワークのプロキシサーバーへのアクセスを許可する   | クライアントにパブリックネットワークのproxy serverへのアクセスを許可する |
| 方法2 | クライアントにプライベートネットワークのプロキシサーバーを通じてのパブリックネットワークへのアクセスを許可する | proxy serverのパブリックネットワークアクセスを許可する        |




### WeChat Mini Programは、どのドメイン名をホワイトリストに設定する必要がありますか。

&lt;trtc-room&gt; ドメイン名ホワイトリスト：

```
https://official.opensso.tencent-cloud.com
https://yun.tim.qq.com
https://cloud.tencent.com
https://webim.tim.qq.com
https://query.tencent-cloud.com
```


>!Tencent CloudサーバーのIPアドレスは、固定IPアドレスではなく動的に更新されるため、固定IPリストを提供することはできません。
