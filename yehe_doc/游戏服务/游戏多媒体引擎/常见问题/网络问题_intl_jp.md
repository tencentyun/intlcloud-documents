
### GMEのリアルタイム音声を使用するときのトラフィック使用量はどのぐらいですか？
流暢音質のビットレートは30kbpsです。標準音質とHD音質のビットレートは64kbpsです。トラフィックはビットレートだけではなく、ルーム内の通話人数にも関係しています。計算式は以下のとおりです：ビットレート x 人数 / 8 = バイト数

### ルームに参加するとき、ネットワークエラーが発生し、エラーコード7004が出力されました。どうすればいいですか？
次の手順に従ってトラブルシューティングを行ってください。
1. AppId、UIN、AuthBuffer（ドキュメントを参照）など、ルーム参加APIのパラメータの正当性を確認してください（詳しくは、各プラットフォームの [インターフェースドキュメント](https://intl.cloud.tencent.com/zh/document/product/607/18522)をご参照ください）。
2. 開発者のテストデバイスが、開発者のプライベートネットワークに存在するかパブリックネットワークに存在するかを確認してください。プライベートネットワークに存在する場合、 [社内ファイアーフォール制限への対応について](https://intl.cloud.tencent.com/document/product/607/35232)をご参照ください。
3. 以下を参照してトラブルシューティングを行ってください。

### ネットワーク問題が発生した場合のトラブルシューティング

- **ネットワーク診断**
	- [ドメイン名チェックtcloud.tim.qq.com](https://ping.huatuo.qq.com/tcloud.tim.qq.com)
	- [ドメイン名チェックgmeconf.qcloud.comをチェック](https://ping.huatuo.qq.com/gmeconf.qcloud.com)
	- [ドメイン名チェックyun.tim.qq.comをチェック](https://ping.huatuo.qq.com/yun.tim.qq.com )

ネットワーク問題が発生したマシンで、ブラウザを使用し上記の3リンクをクリックし、チェック処理を実行してください。チェック処理に約5秒～10秒が必要です。チェック処理が完了すると、**チェック結果URLをクリックして共有**をクリックし、[チケットを送信](https://console.cloud.tencent.com/workorder/category)にて相談窓口にお問い合わせください。
![](https://main.qcloudimg.com/raw/0b540f4bf6222c6b9548b148496a15bb.png)

- **SSO診断**
ネットワーク問題が発生したマシンで、[ドメイン名チェックtcloud.tim.qq.com](https://tcloud.tim.qq.com)をクリックし、チェック結果のスクリーンショットまたは具体的な情報を [チケットを送信](https://console.cloud.tencent.com/workorder/category)にて提供し相談窓口にお問い合わせください。
サンプルコードは以下のとおりです：
```
{"ActionStatus":"FAIL","ErrorCode":60002,"ErrorInfo":"HTTP parse Error"}
```
