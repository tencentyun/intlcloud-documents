ts over SRTプッシュは、**SRTプロトコル**を介してオーディオビデオデータを含むtsストリームを直接伝送し、ダウンストリームは既存のライブストリーミングを多重化しています。TS over SRTは、HaivisionのハードウェアおよびOBSのプッシュ形式規格に準拠しています。
このモードでは、SRTサーバーが負荷（TS）を解析し、RTMPプロトコルにカプセル化して、バックエンドのRTMPサーバーにプッシュします。
![](https://main.qcloudimg.com/raw/5ceb4e1d0d3a2e1f07bb601d17d04eb5.png)

>! アップストリームにSRTプッシュプロトコルを選択しても、コストは増加しません。

## アップストリームのラグ率比較
SRTプッシュを使用すると、次の品質比較図に示すように、ラグ率の改善がはっきりと示されます。
![](https://main.qcloudimg.com/raw/8c55654a4d4050092f98a88b21949e4f.png)


## プッシュのパケット損失率比較
ダウンストリーム側では、SRTプッシュの適用後、アップストリームの品質の最適化により、ダウンストリームのスムーズさも向上します。以下は、闘魚Appでの実際の比較結果です。
- AndroidプラットフォームのSRTプッシュのパフォーマンステストデータ（テストプラットフォーム—MI9）：
![](https://main.qcloudimg.com/raw/91d7a0a3ba846ce2cb92415e4b096b16.png)
- iOSプラットフォームのSRTプッシュのパフォーマンステストデータ（テストプラットフォーム—iphone XR）：
![](https://main.qcloudimg.com/raw/5104e085e29b7bea3b955407086ed342.png)



## アンチパケット損失比較
伝送品質の指標では、QUICと比較しました。SRTは、より正確で高速な再送制御とCSSストリームメディアシーン用のPacingメカニズムにより、同じパケット損失率でもアプリケーション層のパケット損失を低減します。パケット損失率が50%の場合でも、SRTはQUICよりも安定した伝送を保証します。

QUICのアップストリームと比較すると、プッシュ端末の同一リンク、同一ライブストリーミングファイルの場合、5分ごとにパケット損失率が5％増加しました。SRTのプッシュのほうがフレームレートが安定していることが、以下の図からわかります。
![](https://main.qcloudimg.com/raw/638357e7bd47ae34b08423255f354922.png)

## CSSプッシュ
### アクセス方法
CSSプッシュはSRTプロトコルをサポートしますが、**9000ポート**を使用してプッシュする必要があります。プッシュアドレスはCSSコンソールの【[アドレスジェネレーター](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)】の中の [プッシュアドレスの生成](https://intl.cloud.tencent.com/document/product/267/31084) で生成し、以下のルールで接続することができます。

Tencent Cloud SRTプッシュURL：
```
srt://${rtmp-push-domain}:9000?streamid=#!::h=${rtmp-push-domain},r=${app}/${stream},txSecret=${txSecret},txTime=${txTime}
```

>!  `${app}` は表示内容が変更可能であることを示しており、実際には`$`、`{`、`}` の3つの記号を入力する必要はありません。

### 実現方法
SRTサーバーはTSをRTMPにカプセル化して、`${rtmp-push-domain}ドメイン名`にプッシュします。
OBSプッシュコードの入力事例：
![](https://main.qcloudimg.com/raw/d0257df71d0905036eeb0779bcbd74f9.png)

>! SRTプロトコルを使用してプッシュする場合、OBSバージョンを25.0未満にすることはできません。


## ライブストリーミングをプルする
正常なプル再生のフローに従って操作してください。具体的には、 [CSS再生](https://intl.cloud.tencent.com/document/product/267/31559)をご参照ください。



