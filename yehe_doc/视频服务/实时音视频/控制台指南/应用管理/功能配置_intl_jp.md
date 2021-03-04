アプリケーション作成後、【機能設定】によって現在のアプリケーションの[Relayed Push](#bypass)、[クラウドレコーディング](#record)、[高度な権限制御](#purview)の機能を有効にできます。この画面の機能設定はいずれも変更完了の約5分後に有効化されます。

[](id:bypass)
## Relayed Push設定

### 注意事項

- UDP通信プロトコルによるTRTCサービスは、プロトコル変換することで、音声・ビデオストリームを [LVB](https://intl.cloud.tencent.com/zh/document/product/267) のシステムに結合させます。このプロセスを「Relayed Push」と呼びます。
- デフォルトではRelayed Push機能はオフになっています。Relayed Push機能を有効にするには、先にLVBサービスをオンにする必要があります。
- Relayed Pushを [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) に使用する場合、LVBではrelayed live streamingによる下りトラフィック/帯域幅に基づき、関連費用が課金されます。詳細は、[LVB>トラフィック帯域幅課金](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) の説明をご参照ください。
- Relayed Pushを [クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426) に使用する時は、レコーディング、レコーディングファイル保存などの費用が発生します。詳細は、[クラウドレコーディングと再生>関連費用](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8)の説明をご参照ください。
-  [LVBコンソール](https://console.cloud.tencent.com/live/domainmanage) でRelayed Pushに使用されるプッシュドメイン名（`xxxx.livepush.myqcloud.com`）にレコーディング、トランスコーディング、スクリーンキャプチャ・ポルノ検出、ウォーターマークなどの課金機能のテンプレートをバインドする場合は、Relayed Push時に、テンプレートに対応する[付加価値サービス費用](https://intl.cloud.tencent.com/zh/document/product/267/2819#.E5.A2.9E.E5.80.BC.E6.9C.8D.E5.8A.A1.E8.B4.B9.E7.94.A8) が発生します。

[](id:open_bypass)
### Relayed Push機能をオンにする
1. TRTCコンソールに入り、【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】を選択します。
2. 機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
 ![](https://main.qcloudimg.com/raw/e5b5b5494f2c75a7ea7a48caae32f256.png)
3. 【Relayed Push設定】で、【Relayed Pushを有効】の右側のボタンをクリックします。
![](https://main.qcloudimg.com/raw/b9846f4a7f5ce1e39b3450963e872c90.png)
4. ポップアップした【Relayed Push機能をオンにする】のポップアップボックスで、**リスク説明にしっかりと目を通し**、アクティブ化について確認してから、【Relayed Push機能をオンにする】をクリックします。
![](https://main.qcloudimg.com/raw/d39ff108d2f200cc92a78b42359bff6e.png)

[](id:select)
### Relayed Push方式の選択
[Relayed Push機能をオン](#open_bypass)にした後、実際の業務の状況に応じてRelayed Pushの方式を選択することができます。
![](https://main.qcloudimg.com/raw/3fd6fbe8c5837a6d7f78a19f079b477a.png)

- **Relayed Push用指定ストリーム**：「Relayed Push用指定ストリーム」の選択後、MixTranscodingが不要な場合は、クライアントSDK [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) のインターフェースを呼び出して、直接Relayed Pushを起動させてください。MixTranscodingが必要な場合は、 [Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618)のドキュメントのガイド操作に従ってください。MixTranscoding後に自動的にRelayed Pushされます。
- **Global Auto-relay**：「Global Auto-relay」を選択すると、すべてのTRTCのアップストリームのオーディオ／ビデオストリームはLVBシステムにAuto-relay Pushされます。


[](id:close__bypass)
### Relayed Push機能をオフにする
Relayed Push機能を無効にしたい場合、具体的な操作手順は次のとおりです。
1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックして、機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
3. 【Relayed Push設定】で、【Relayed Pushを有効】の右側のボタンをクリックします。
![](https://main.qcloudimg.com/raw/0ac618f3fb643a3d5fd1ff11566eef31.png)
4. ポップアップした【Relayed Push機能をオフにする】のポップアップボックスで、**リスク説明にしっかりと目を通し**、無効化について確認してから、【Relayed Push機能をオフにする】をクリックします。
![](https://main.qcloudimg.com/raw/1306f736ff0b5337f468325cabdfee54.png)


[](id:record)
## クラウドレコーディングの設定

### 注意事項
- TRTCのサービスは、Relayed Pushが [LVB](https://intl.cloud.tencent.com/zh/document/product/267)の機能を使用することで完全なクラウドレコーディング機能を提供し、レコーディングされたファイルは[VOD](https://intl.cloud.tencent.com/zh/document/product/266) のプラットフォームに保存されます。
- レコーディング機能は、LVBサービスの機能を使用するため、LVBレコーディングの費用が発生し、当月のLVBレコーディングの同時チャネルのピーク値が決算の基準となります。詳しい課金規則については、 [LVB > LVBレコーディング料金説明](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6)をご参照ください。
- レコーディング後のファイルはVODプラットフォームに保存され、VODの保存料金が発生します。VODプラットフォームに保存されたレコーディングファイルの保存容量で課金されます。詳しい課金規則については、[VOD > ビデオ保存（日次決算）料金説明](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください。
- レコーディングしたビデオファイルを再生またはダウンロードしたい場合、VODサービスのトラフィック（ビデオアクセラレーション）費用が発生し、下りアクセラレーションのトラフィックに応じて課金されます。詳しい課金規則は、[VOD> ビデオアクセラレーション（日次決済）料金説明](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください。
- クラウドレコーディング機能はデフォルトでオフになっています。クラウドレコーディング機能を有効にするには、LVBとVideo on Demandサービスをアクティブにする必要があります
- クラウドレコーディングはRelayed Pushに依存します。先に[Relayed Push]を有効(#open_bypass)にしてください。


[](id:open_record)
### クラウドレコーディング機能を有効にする
TRTCのクラウドレコーディングは、ルーム内の各ユーザーの音声・ビデオストリームをレコーディングして個別のファイルにすることができます。クラウドレコーディング機能を有効にしたい場合、詳しい操作ガイドは [クラウドレコーディングと再生の実現](https://intl.cloud.tencent.com/document/product/647/35426#open)をご参照ください。

[](id:change_record)
### クラウドレコーディング設定の変更
>! クラウドレコーディングの設定を変更すると、オンラインの作業データに影響を与える可能性があります。リスクを確認してから、注意して続行してください。

1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックして、クラウドレコーディングの設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
3. 【機能設定】>【クラウドレコーディング設定】で、右側の【編集】をクリックしてクラウドレコーディング設定の変更画面に入ります。
![](https://main.qcloudimg.com/raw/1e0ac1e9704a5901466ad6ec3ccac89b.png)
4. 実際の状況に応じて [設定情報](https://intl.cloud.tencent.com/document/product/647/35426#recordType)を変更し、【OK】をクリックして変更を保存します。


[](id:close_record)
### クラウドレコーディング機能をオフにする
クラウドレコーディングをオフにすると、オンラインで手動レコーディングや自動レコーディングなどのクラウドレコーディングを実行できなくなります。閉じる前に、業務でクラウドレコーディングが不要であることを確認してください。

1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックして、機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【クラウドレコーディング設定】の中で、【クラウドレコーディングの起動】の右側のボタンをクリックします。
![](https://main.qcloudimg.com/raw/93761fae36103906ddbd4e134460be0a.png)
3.無効にした後の影響にしっかりと目を通し、クラウドレコーディングの無効について確認してから、【クラウドレコーディングをオフにする】をクリックします。
![](https://main.qcloudimg.com/raw/3202cb938030085babc0210283ce9221.png)



[](id:purview)
## 高度な権限制御
特定のルームに、入室制限またはマイクアクセス制限を追加したい場合、つまり指定したユーザーのみ入室またはマイクアクセスを許可したい場合に、クライアントで権限を判断するとクラッキングされて攻撃されやすいことが懸念される場合は [高度な権限制御を有効にする](https://intl.cloud.tencent.com/document/product/647/35157)ことをご検討ください。
![](https://main.qcloudimg.com/raw/8fd4b0d09aeea46a15714c59e5e0419e.png)


### 注意事項
高度な権限制御を有効にすると、現在のSDKAppIDの全てのユーザーは、入室するためにTRTCParamsでprivateMapKeyパラメータを正しく渡す必要があります。このSDKAppIDを使用するユーザーがオンラインにいる場合は、この機能を不用意に有効にしないでください。


### 高度な権限制御を有効にする
1. 【アプリケーション管理】をクリックして、高度な権限制御を有効にしたいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【高度な権限制御】の中で、右側の【高度な権限制御のオン】の右側ボタンをクリックします。
![](https://main.qcloudimg.com/raw/196e32293f8f5c159a3513cbf4b9723a.png)

### 高度な権限制御を無効にする
1. 【アプリケーション管理】をクリックして、高度な権限制御を無効にしたいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【高度な権限制御】の中で、右側の【高度な権限制御のオフ】の右側ボタンをクリックします。
![](https://main.qcloudimg.com/raw/b7015cb446cd022d591fda7e22689e44.png)

## 関連ドキュメント
- 新しいアプリケーションを作成したい場合、具体的な操作方法については、[アプリケーション作成](https://intl.cloud.tencent.com/zh/document/product/647/39077)をご参照ください。
- アプリケーションリストで関連アプリケーションを検索したい場合、具体的な操作方法については、[アプリケーション検索](https://intl.cloud.tencent.com/zh/document/product/647/39078)をご参照ください。
- アプリケーションの基本情報を確認したい場合、具体的な操作については、[アプリケーション情報](https://intl.cloud.tencent.com/zh/document/product/647/39079)をご参照ください。
- Cloud MixTranscoding時にカスタマイズした背景画像を設定したい場合、素材管理で対応する画像素材を追加できます。具体的な操作については、[素材管理](https://intl.cloud.tencent.com/zh/document/product/647/39081)をご参照ください。
- アプリケーションとセットになるDemoソースコードのクイック実行が必要な場合、具体的な操作については、[クイックマスター](https://intl.cloud.tencent.com/zh/document/product/647/39082)をご参照ください。





アプリケーション作成後、【機能設定】によって現在のアプリケーションの[Relayed Push](#bypass)、[クラウドレコーディング](#record)、[高度な権限制御](#purview)の機能を有効にできます。この画面の機能設定はいずれも変更完了の約5分後に有効化されます。

[](id:bypass)
## Relayed Push設定

### 注意事項

- UDP通信プロトコルによるTRTCサービスは、プロトコル変換することで、音声・ビデオストリームを [LVB](https://intl.cloud.tencent.com/zh/document/product/267) のシステムに結合させます。このプロセスを「Relayed Push」と呼びます。
- デフォルトではRelayed Push機能はオフになっています。Relayed Push機能を有効にするには、先にLVBサービスをオンにする必要があります。
- Relayed Pushを [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) に使用する場合、LVBではrelayed live streamingによる下りトラフィック/帯域幅に基づき、関連費用が課金されます。詳細は、[LVB>トラフィック帯域幅課金](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) の説明をご参照ください。
- Relayed Pushを [クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/35426) に使用する時は、レコーディング、レコーディングファイル保存などの費用が発生します。詳細は、[クラウドレコーディングと再生>関連費用](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8)の説明をご参照ください。
-  [LVBコンソール](https://console.cloud.tencent.com/live/domainmanage) でRelayed Pushに使用されるプッシュドメイン名（`xxxx.livepush.myqcloud.com`）にレコーディング、トランスコーディング、スクリーンキャプチャ・ポルノ検出、ウォーターマークなどの課金機能のテンプレートをバインドする場合は、Relayed Push時に、テンプレートに対応する[付加価値サービス費用](https://intl.cloud.tencent.com/zh/document/product/267/2819#.E5.A2.9E.E5.80.BC.E6.9C.8D.E5.8A.A1.E8.B4.B9.E7.94.A8) が発生します。

[](id:open_bypass)
### Relayed Push機能をオンにする
1. TRTCコンソールに入り、【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】を選択します。
2. 機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
 ![](https://main.qcloudimg.com/raw/e5b5b5494f2c75a7ea7a48caae32f256.png)
3. 【Relayed Push設定】で、【Relayed Pushを有効】の右側のボタンをクリックします。
![](https://main.qcloudimg.com/raw/b9846f4a7f5ce1e39b3450963e872c90.png)
4. ポップアップした【Relayed Push機能をオンにする】のポップアップボックスで、**リスク説明にしっかりと目を通し**、アクティブ化について確認してから、【Relayed Push機能をオンにする】をクリックします。
![](https://main.qcloudimg.com/raw/d39ff108d2f200cc92a78b42359bff6e.png)

[](id:select)
### Relayed Push方式の選択
[Relayed Push機能をオン](#open_bypass)にした後、実際の業務の状況に応じてRelayed Pushの方式を選択することができます。
![](https://main.qcloudimg.com/raw/3fd6fbe8c5837a6d7f78a19f079b477a.png)

- **Relayed Push用指定ストリーム**：「Relayed Push用指定ストリーム」の選択後、MixTranscodingが不要な場合は、クライアントSDK [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) のインターフェースを呼び出して、直接Relayed Pushを起動させてください。MixTranscodingが必要な場合は、 [Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618)のドキュメントのガイド操作に従ってください。MixTranscoding後に自動的にRelayed Pushされます。
- **Global Auto-relay**：「Global Auto-relay」を選択すると、すべてのTRTCのアップストリームのオーディオ／ビデオストリームはLVBシステムにAuto-relay Pushされます。


[](id:close__bypass)
### Relayed Push機能をオフにする
Relayed Push機能を無効にしたい場合、具体的な操作手順は次のとおりです。
1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックして、機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
3. 【Relayed Push設定】で、【Relayed Pushを有効】の右側のボタンをクリックします。
![](https://main.qcloudimg.com/raw/0ac618f3fb643a3d5fd1ff11566eef31.png)
4. ポップアップした【Relayed Push機能をオフにする】のポップアップボックスで、**リスク説明にしっかりと目を通し**、無効化について確認してから、【Relayed Push機能をオフにする】をクリックします。
![](https://main.qcloudimg.com/raw/1306f736ff0b5337f468325cabdfee54.png)


[](id:record)
## クラウドレコーディングの設定

### 注意事項
- TRTCのサービスは、Relayed Pushが [LVB](https://intl.cloud.tencent.com/zh/document/product/267)の機能を使用することで完全なクラウドレコーディング機能を提供し、レコーディングされたファイルは[VOD](https://intl.cloud.tencent.com/zh/document/product/266) のプラットフォームに保存されます。
- レコーディング機能は、LVBサービスの機能を使用するため、LVBレコーディングの費用が発生し、当月のLVBレコーディングの同時チャネルのピーク値が決算の基準となります。詳しい課金規則については、 [LVB > LVBレコーディング料金説明](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6)をご参照ください。
- レコーディング後のファイルはVODプラットフォームにストレージします。VODで発生したストレージ費用は、レコーディングファイルをVODプラットフォームにストレージしたストレージ容量に従って計上します。費用規則の詳細は [VOD > ビデオストレージ（日割計算）費用説明](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください。
- レコーディングしたビデオファイルを再生またはダウンロードしたい場合、VODサービスのトラフィック（ビデオアクセラレーション）費用が発生し、下りアクセラレーションのトラフィックに応じて課金されます。詳しい課金規則は、[VOD> ビデオアクセラレーション（日次決済）料金説明](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください。
- クラウドレコーディング機能はデフォルトでオフになっています。クラウドレコーディング機能を有効にするには、LVBとVideo on Demandサービスをアクティブにする必要があります
- クラウドレコーディングはRelayed Pushに依存します。先に[Relayed Push]を有効(#open_bypass)にしてください。


[](id:open_record)
### クラウドレコーディング機能を有効にする
TRTCのクラウドレコーディングは、ルーム内の各ユーザーの音声・ビデオストリームをレコーディングして個別のファイルにすることができます。クラウドレコーディング機能を有効にしたい場合、詳しい操作ガイドは [クラウドレコーディングと再生の実現](https://intl.cloud.tencent.com/document/product/647/35426#open)をご参照ください。

[](id:change_record)
### クラウドレコーディング設定の変更
>! クラウドレコーディングの設定を変更すると、オンラインの作業データに影響を与える可能性があります。リスクを確認してから、注意して続行してください。

1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックして、クラウドレコーディングの設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
3. 【機能設定】>【クラウドレコーディング設定】で、右側の【編集】をクリックしてクラウドレコーディング設定の変更画面に入ります。
![](https://main.qcloudimg.com/raw/1e0ac1e9704a5901466ad6ec3ccac89b.png)
4. 実際の状況に応じて [設定情報](https://intl.cloud.tencent.com/document/product/647/35426#recordType)を変更し、【OK】をクリックして変更を保存します。


[](id:close_record)
### クラウドレコーディング機能をオフにする
クラウドレコーディングをオフにすると、オンラインで手動レコーディングや自動レコーディングなどのクラウドレコーディングを実行できなくなります。閉じる前に、業務でクラウドレコーディングが不要であることを確認してください。

1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックして、機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【クラウドレコーディング設定】の中で、【クラウドレコーディングの起動】の右側のボタンをクリックします。
![](https://main.qcloudimg.com/raw/93761fae36103906ddbd4e134460be0a.png)
3.無効にした後の影響にしっかりと目を通し、クラウドレコーディングの無効について確認してから、【クラウドレコーディングをオフにする】をクリックします。
![](https://main.qcloudimg.com/raw/3202cb938030085babc0210283ce9221.png)



[](id:purview)
## 高度な権限制御
特定のルームに、入室制限またはマイクアクセス制限を追加したい場合、つまり指定したユーザーのみ入室またはマイクアクセスを許可したい場合に、クライアントで権限を判断するとクラッキングされて攻撃されやすいことが懸念される場合は [高度な権限制御を有効にする](https://intl.cloud.tencent.com/document/product/647/35157)ことをご検討ください。
![](https://main.qcloudimg.com/raw/8fd4b0d09aeea46a15714c59e5e0419e.png)


### 注意事項
高度な権限制御を有効にすると、現在のSDKAppIDの全てのユーザーは、入室するためにTRTCParamsでprivateMapKeyパラメータを正しく渡す必要があります。このSDKAppIDを使用するユーザーがオンラインにいる場合は、この機能を不用意に有効にしないでください。


### 高度な権限制御を有効にする
1. 【アプリケーション管理】をクリックして、高度な権限制御を有効にしたいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【高度な権限制御】の中で、右側の【高度な権限制御のオン】の右側ボタンをクリックします。
![](https://main.qcloudimg.com/raw/196e32293f8f5c159a3513cbf4b9723a.png)

### 高度な権限制御を無効にする
1. 【アプリケーション管理】をクリックして、高度な権限制御を無効にしたいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【高度な権限制御】の中で、右側の【高度な権限制御のオフ】の右側ボタンをクリックします。
![](https://main.qcloudimg.com/raw/b7015cb446cd022d591fda7e22689e44.png)

## 関連ドキュメント
- 新しいアプリケーションを作成したい場合、具体的な操作方法については、[アプリケーション作成](https://intl.cloud.tencent.com/zh/document/product/647/39077)をご参照ください。
- アプリケーションリストで関連アプリケーションを検索したい場合、具体的な操作方法については、[アプリケーション検索](https://intl.cloud.tencent.com/zh/document/product/647/39078)をご参照ください。
- アプリケーションの基本情報を確認したい場合、具体的な操作については、[アプリケーション情報](https://intl.cloud.tencent.com/zh/document/product/647/39079)をご参照ください。
- Cloud MixTranscoding時にカスタマイズした背景画像を設定したい場合、素材管理で対応する画像素材を追加できます。具体的な操作については、[素材管理](https://intl.cloud.tencent.com/zh/document/product/647/39081)をご参照ください。
- アプリケーションとセットになるDemoソースコードのクイック実行が必要な場合、具体的な操作については、[クイックマスター](https://intl.cloud.tencent.com/zh/document/product/647/39082)をご参照ください。





