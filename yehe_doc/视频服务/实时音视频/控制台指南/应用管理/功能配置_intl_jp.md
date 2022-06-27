アプリケーション作成後、【機能設定】によって現在のアプリケーションの[Relayed Push](#bypass)、[クラウドレコーディング](#record)、[高度な権限制御](#purview)の機能を有効にできます。この画面の機能設定はいずれも変更完了の約5分後に有効化されます。

[](id:bypass)
## Relayed Push設定

### 注意事項

- UDP通信プロトコルによるTRTCサービスは、プロトコル変換することで、オーディオ・ビデオストリーミングを[CSS](https://intl.cloud.tencent.com/document/product/267)のシステムに結合させます。このプロセスを「Relayed Push」と呼びます。
- デフォルトではRelayed Push機能はオフになっています。Relayed Push機能を有効にするには、先にCSSサービスをオンにする必要があります。
- Relayed PushをCDN relayed live streaming に使用する場合、CSSではRelayed live Streamingによる下りトラフィック/帯域幅に基づき、関連費用が課金されます。詳細は、［CSS>トラフィック帯域幅課金］(https://intl.cloud.tencent.com/document/product/267/2818)の説明をご参照ください。
- Relayed Pushを[クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426) に使用する時は、レコーディング、レコーディングファイル保存などの費用が発生します。詳細は、[クラウドレコーディングと再生>関連費用](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8)の説明をご参照ください。
- [CSSコンソール](https://console.cloud.tencent.com/live/domainmanage)でRelayed Pushに使用されるプッシュドメイン名（`xxxx.livepush.myqcloud.com`）にレコーディング、トランスコーディング、スクリーンキャプチャ・ポルノ検出、ウォーターマークなどの課金機能のテンプレートをバインドする場合は、Relayed Push時に、テンプレートに対応する[付加価値サービス費用](https://intl.cloud.tencent.com/document/product/267/2819)が発生します。

[](id:open_bypass)
### Relayed Push機能をオンにする
1. TRTCコンソールに入り、【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】を選択します。
2. 機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
 ![](https://main.qcloudimg.com/raw/f302931ec709c205bd6c4e2378cd14b3.png)
3. 【Relayed Push設定】で、【Relayed Pushを有効】の右側のボタンをクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/ee063851a4b9cc6d391552ac3602a685.png)
4. ポップアップした【Relayed Push機能をオンにする】のポップアップボックスで、**リスク説明にしっかりと目を通し**、アクティブ化について確認してから、【Relayed Push機能をオンにする】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/f964548ce95c678e72a657e8ee69ac00.png)

[](id:select)
Relayed Push### Relayed Push方式の選択
[Relayed Push機能をオン](#open_bypass)にした後、実際の業務の状況に応じてRelayed Pushの方式を選択することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/d9d7e36228a8a163b7700d0830af6671.png)

- **Relayed Push用指定ストリーム**：「Relayed Push用指定ストリーム」の選択後、ミクスストリーミングトランスコードが不要な場合は、クライアントSDK [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a7cbe48ea2cd3fb05a5b10350b6d81265)のインターフェースを呼び出して、直接Relayed Pushを起動させてください。ミクスストリーミングトランスコードが必要な場合は、Cloud MixTranscodingのドキュメントのガイド操作に従ってください。ミクスストリーミングトランスコーディング後にAuto-Relayed Pushが実行されます。
- **Global Auto-relay**：「Global Auto-relay」を選択すると、すべてのTRTCのアップストリームのオーディオビデオストリーミングはCSSシステムにAuto-Relayed Pushされます。


[](id:close__bypass)
### Relayed Push機能をオフにする
Relayed Push機能を無効にしたい場合、具体的な操作手順は次のとおりです。
1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックして、機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【Relayed Push設定】で、【Relayed Pushを有効】の右側のボタンをクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/3583a5bf087294810c6898d6a6baeff9.png)
3. ポップアップした【Relayed Push機能をオフにする】のポップアップボックスで、**リスク説明にしっかりと目を通し**、無効化について確認してから、【Relayed Push機能をオフにする】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/80d988936617936ff82ce23207f93bd0.png)


[](id:record)
## クラウドレコーディングの設定

### 注意事項
- TRTCのサービスは、Relayed Pushが[CSS](https://intl.cloud.tencent.com/document/product/267)の機能を使用することで完全なクラウドレコーディング機能を提供し、レコーディングされたファイルは[VOD](https://intl.cloud.tencent.com/document/product/266)のプラットフォームに保存されます。
- レコーディング機能は、CSSサービスの機能を使用するため、CSSレコーディングの費用が発生し、当月のCSSレコーディングの同時チャネルのピーク値が決算の基準となります。詳しい課金規則については、[CSS > CSSレコーディング料金説明](https://intl.cloud.tencent.com/document/product/267/39605)をご参照ください。
- レコーディング後のファイルはVODプラットフォームに保存され、VODの保存料金が発生します。VODプラットフォームに保存されたレコーディングファイルの保存容量で課金されます。詳しい課金規則については、[VOD > ビデオ保存（日次決算）料金説明](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください。
- レコーディングしたビデオファイルを再生またはダウンロードしたい場合、VODサービスのトラフィック（ビデオアクセラレーション）料金が発生し、下りアクセラレーションのトラフィックに応じて課金されます。詳しい課金ルールは、[VOD> ビデオアクセラレーション（日次決済）料金説明](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください。
- クラウドレコーディング機能はデフォルトでオフになっています。クラウドレコーディング機能を有効にするには、CSSとVODサービスをアクティブにする必要があります
- クラウドレコーディングはRelayed Pushに依存します。先に[Relayed Push](#open_bypass)を有効にしてください。


[](id:open_record)
### クラウドレコーディング機能をオンにする
TRTCのクラウドレコーディングは、ルーム内の各ユーザーのオーディオ・ビデオストリーミングをレコーディングして個別のファイルにすることができます。クラウドレコーディング機能を有効にしたい場合、詳しい操作ガイドは [クラウドレコーディングと再生の実現](https://intl.cloud.tencent.com/document/product/647/35426#open)をご参照ください。

[](id:change_record)
### クラウドレコーディング設定の変更
>! クラウドレコーディングの設定を変更すると、オンラインで稼働中の作業データに影響を与える可能性があります。リスクを確認してから、注意して続行してください。

1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックして、クラウドレコーディングの設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
3. 【機能設定】>【クラウドレコーディング設定】で、右側の【編集】をクリックしてクラウドレコーディング設定の変更画面に入ります。
![](https://main.qcloudimg.com/raw/1c46c6d6f7d87928536ab576975cdcd3.png)
4. 実際の状況に応じて [設定情報](https://intl.cloud.tencent.com/document/product/647/35426#recordType)を変更し、【OK】をクリックして変更を保存します。


[](id:close_record)
### クラウドレコーディング機能をオフにする
クラウドレコーディングをオフにすると、オンラインで手動レコーディングや自動レコーディングなどのクラウドレコーディングを実行できなくなります。オフにする前に、業務でクラウドレコーディングが不要であることを確認してください。

1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックして、機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【クラウドレコーディング設定】で、【クラウドレコーディングの起動】の右側のボタンをクリックします。
![](https://main.qcloudimg.com/raw/72893310f197830b468292b9d0062458.png)
3. オフにした後の影響にしっかりと目を通し、クラウドレコーディングの無効について確認してから、【クラウドレコーディングをオフにする】をクリックします。
![](https://main.qcloudimg.com/raw/b1a41cf54dad0c5cd48f65d2a250e56d.png)



[](id:purview)
## 高度な権限制御
特定のルームに、入室制限またはマイクアクセス制限を追加したい場合、つまり指定したユーザーのみ入室またはマイクアクセスを許可したい場合に、クライアントで権限を判断するとクラッキングされて攻撃されやすいことが懸念される場合は [高度な権限制御を有効にする](https://intl.cloud.tencent.com/document/product/647/35157)ことをご検討ください。
![](https://main.qcloudimg.com/raw/78882ea4eac56c347c89a4e8113d706a.png)


### 注意事項
高度な権限制御を有効にすると、現在のSDKAppIDの全てのユーザーは、入室するためにTRTCParamsでprivateMapKeyパラメータを正しく渡す必要があります。このSDKAppIDを使用するユーザーがオンラインにいる場合は、この機能を不用意に有効にしないでください。


### 高度な権限制御を有効にする
1. 【アプリケーション管理】をクリックして、高度な権限制御を有効にしたいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【高度な権限制御】で、右側の【高度な権限制御のオン】の右側ボタンをクリックします。
![](https://main.qcloudimg.com/raw/d5de4b300cf71969244239d821414db6.png)

### 高度な権限制御を無効にする
1. 【アプリケーション管理】をクリックして、高度な権限制御を無効にしたいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【高度な権限制御】で、右側の【高度な権限制御のオフ】の右側ボタンをクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/b05dfb7bb910e39cd77257cc838ad5e3.png)

## 関連ドキュメント
- 新しいアプリケーションを作成したい場合、具体的な操作方法については、[アプリケーションの作成](https://intl.cloud.tencent.com/document/product/647/39077)をご参照ください。
- アプリケーションリストで関連アプリケーションを検索したい場合、具体的な操作方法については、[アプリケーションの検索](https://intl.cloud.tencent.com/document/product/647/39078)をご参照ください。
- アプリケーションの基本情報を確認したい場合、具体的な操作については、[アプリケーション情報](https://intl.cloud.tencent.com/document/product/647/39079)をご参照ください。
- Cloud MixTranscoding時にカスタマイズした背景画像を設定したい場合、素材管理で対応する画像素材を追加できます。
- アプリケーションに付属するDemoソースコードのクイック実行が必要な場合、具体的な操作については、[クイックマスター](https://intl.cloud.tencent.com/document/product/647/39082)をご参照ください。



