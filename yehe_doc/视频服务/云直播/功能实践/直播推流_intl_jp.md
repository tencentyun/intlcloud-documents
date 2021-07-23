CSSのサービスは本質的に放送プロセスの一環であり、テレビ局のライブストリーミングプログラムがケーブルネットワークを介して何百万もの世帯に送信されるといった行程と類似しています。このプロセスを完成するには、CSSには収集とプッシュのためのデバイス（カメラに類似）、CSSサービス（テレビ局のケーブルネットワークに類似）および再生デバイス（テレビに類似）が必要です。収集とプッシュのデバイスおよび再生デバイスをスマートフォン、PC、Padなどのスマート端末およびWebブラウザとすることができ、また、弊社は対応するデバイスのプッシュソフトウェアのDemoも提供しています。

[](id:step1)
## 準備作業
1. [Tencent CSSサービス](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)をアクティブ化します 。
2. [【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)を選択して、【ドメイン名の追加】を選択し、ICP登録したプッシュドメイン名を追加します。詳細については、[独自のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。
>? CSSはデフォルトのプッシュドメイン名を提供します。形式は`xxx.livepush.myqcloud.com`ですが、実際の業務でこのドメイン名をプッシュドメイン名として使用することはお勧めしません。

[](id:push_add)
## プッシュアドレスの取得
CSSコンソールの【CSSツールボックス】>[【アドレスジェネレーター】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)に移動し、プッシュアドレスを発行します。設定は次のとおりです。
- 発行タイプの選択：**プッシュドメイン名**。
-ドメイン名管理で追加したプッシュドメイン名を選択します。
- 同一ドメイン名の複数Appを区別するために使用されるアドレスパスであるAppNameを入力します。デフォルト値はliveです。
- カスタマイズされたストリーム名StreamNameを入力します（例：liveteststream）。
- アドレス期限を選択します（例：` 2019-10-18  23:59:59`）。
- 【アドレスの発行】を選択します。 

>!
>- ライブストリーミングのセキュリティを保護するために、システムが自動的にプッシュ認証を有効にします。[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)で変更するプッシュドメイン名を選択し、右側の【管理】を選択して、ドメイン名詳細情報ページの【プッシュ設定】に移動し、認証設定情報をカスタマイズすることもできます。プッシュアドレスの形式は次のとおりです。
`rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
>-  上記方法以外にも、CSSコンソールの[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)でプッシュドメイン名を選択して、【管理】を選択し、【プッシュ設定】を選択して、プッシュアドレスの期限切れ時間とカスタマイズされたストリーム名StreamNameを入力し、【プッシュアドレスの発行】を選択すると、プッシュアドレスを発行できます。
>- **長期的に有効なプッシュアドレス**が必要な場合は、[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)に移動し、プッシュドメイン名を選択したのち【管理】を選択。【プッシュ設定】をまた選択後、【プッシュアドレスサンプルコード】にありますサンプルコードから発行します。具体的なクエリー方式については、 [プッシュサンプルコードのクエリー方法](https://intl.cloud.tencent.com/document/product/267/31059)をご参照ください。

[](id:live_push)
## CSSプッシュ
業務のシナリオに応じて次の方式でCSSプッシュを実現できます。

[](id:pc)
### シーン1 ：PCプッシュ
PC（Windows/Mac）でプッシュする場合は、実際の状況に応じて [OBS](https://obsproject.com/download) または [XSplit](https://www.xsplit.com/zh-cn) のインストールを選択して、プッシュすることができます。 OBSはWindows、Mac、Linuxなどのシステムをサポートする無償オープンソースのビデオレコーディングおよびビデオリアルタイムストリームソフトウェアです。XSplitの使用は有償ですが、XSplitにはゲームライブストリーミング用の個別のインストールパッケージがあります。ゲームライブストリーミングでない場合は、BroadCasterの使用をお勧めします。
![](https://main.qcloudimg.com/raw/dcb203971ac99415258ea0b0ee1529a8.png)
ここではOBSプッシュのインストールを例示します。操作ステップは次の説明のとおりです。準備の完了したプッシュアドレスが次のとおりであると仮定します。

```
rtmp://3891.livepush.myqcloud.com/live/3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F
```


1. [OBSオフィシャルサイト](https://obsproject.com/download) に移動し、プッシュツールをインストールします。
2. OBSを開き、下部ツールバーの【コントロール】>【設定】を選択し、ボタンを押して設定インターフェースに移動します。
3. 【プッシュ】を選択し、プッシュ設定ページに移動して、次の設定を行います。
  1. サービスタイプ：カスタムを選択します。
  1. サーバーに `rtmp://3891.livepush.myqcloud.com/live/`のようにプッシュアドレスの前半部分を入力します。
  1. ストリームキーに`3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F`のようにプッシュアドレスの後半部分を入力します。
  1. 右下隅の【OK】を選択します。
![](https://main.qcloudimg.com/raw/7b5365a0be590c3694fbb6d0ded8e5e3.png)
4. ツールバーの【コントロール】>【プッシュ開始】を選択すれば、プッシュテストを実行できます。OBS操作の詳細については、[OBSプッシュ](https://intl.cloud.tencent.com/document/product/267/31569)をご参照ください。

[](id:web)
### シーン2：Webプッシュ
1. CSSコンソールにログインします。
2. 【支援ツール】>[【Webプッシュ】](https://console.cloud.tencent.com/live/tools/webpush)を選択します。
3. Webプッシュのページで次の設定を行います。
  1. プッシュドメイン名を選択します。
  2. 同一ドメイン名の複数Appを区別するために使用されるアドレスパスのAppNameを入力します。デフォルト値はliveです。
  2. カスタマイズされたStreamNameを入力します（例：liveteststream）。
  3. 期限を選択します（例：`2019-10-30 23:59:59`）。
  4. 【プッシュ開始】を選択し、カメラの承認を完了すると、プッシュを開始できます

>! Webプッシュ機能は、デバイスにカメラがインストールされている必要があり、かつブラウザがカメラ許可を呼び出すFlashプラグインをサポートしている必要があります。

![](https://main.qcloudimg.com/raw/9da7489bb2387049859131e792364124.png)

[](id:mobile)
### シーン3：モバイルプッシュ
1. スマートフォンで2次元コードをスキャンし、モバイル[ビデオクラウドツールキット](https://intl.cloud.tencent.com/document/product/1071/38147)をインストールすることで体験できます。
2. ツールキットを開き、【モバイルライブストリーミング】>【カメラプッシュ】を選択します。
3. [プッシュアドレス](#step1)を手動入力するか、または2次元コードをスキャンして入力します。
4. 左下隅のスタートボタンを選択すれば、プッシュを開始することができます。

>? 事前にプッシュアドレスを準備していない場合は、カメラプッシュページでプッシュアドレス右側の【NEW】を選択すれば、システムが自動的にプッシュアドレスを入力し、対応する再生アドレスが提供されます。この再生アドレスを介してCSSプッシュ機能を確認できます。

[](id:sdk)
### シーン4：ライブストリーミングSDKプッシュ
CSSプッシュ機能を既存のAppに統合するのみの使用は、以下の手順に従うことで利用可能です。
1. [モバイルライブストリーミングSDK](https://intl.cloud.tencent.com/document/product/1071/38150) 開発パッケージをダウンロードします。
2. ドッキングドキュメント（[iOS](https://intl.cloud.tencent.com/document/product/1071/38157) & [Android](https://intl.cloud.tencent.com/document/product/1071/38158)）を参照してアクセスを完了します。

ライブストリーミングSDKはモバイル端末ライブストリーミングソリューションの集合であり、無償のソースコードの形式で表示されます。CSS、VOD、IM、COS等のサービスを組み合わせて利用し、最適なライブストリーミングソリューションを構築します。詳細については、 [モバイルライブストリーミング](https://intl.cloud.tencent.com/product/mlvb)をご参照ください。 


## よくあるご質問
- [CSS再生はどのように実現するのですか。](https://intl.cloud.tencent.com/document/product/267/31559)
- [プッシュURLはどのようにスプライスするのですか。](https://intl.cloud.tencent.com/document/product/267/38393)
- [ホットリンク防止はどのように計算するのですか。](https://intl.cloud.tencent.com/document/product/267/31560)

