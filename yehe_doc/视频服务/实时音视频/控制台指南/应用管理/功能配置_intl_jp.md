アプリケーション作成後、【機能設定】によって現在のアプリケーションの[Relayed Push](#bypass)、[クラウドレコーディング](#record)、[高度な権限制御](#purview)の機能を有効にできます。この画面の機能設定はいずれも変更完了の約5分後に有効化されます。

<span id="bypass"></span>
## Relayed Push設定

### 注意事項

- UDPトランスポートプロトコルに基づくTRTCサービスは、プロトコル変換を介してオーディオストリームとビデオストリームを [LVB]https://intl.cloud.tencent.com/document/product/267システムに接続します。このプロセスは「Relayed Push」と呼ばれます。
- デフォルトではRelayed Push機能はオフになっています。Relayed Push機能を有効にするには、先にLVBサービスをオンにする必要があります。
- [CDN Relayed live Streaming](https://intl.cloud.tencent.com/document/product/647/35242)にRelayed Pushを使用するとき、LVBでは、ライブストリーミングによって生成されたダウンストリームトラフィック/帯域幅に基づいて関連料金が請求されます。詳細については［LVB>トラフィック帯域幅課金］(https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#bill-by-traffic.2Fbandwidth)の説明をご参照ください。
- ［クラウドレコーディング］(https://intl.cloud.tencent.com/document/product/647/35426)にRelayed Pushを使用するとき、レコーディング、レコーディングファイルのストレージなどの料金が発生します。詳細は、[クラウドレコーディングと再生>関連費用](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8)の説明をご参照ください。
レコーディング、トランスコード、スクリーンキャプチャ、ポルノ検出、ウォーターマーク、およびその他の課金機能テンプレートをhttps://console.cloud.tencent.com/live/domainmanage[LVBコンソール]のRelayed Pushで使用されるプッシュドメイン名（xxxx.livepush.myqcloud.com）にバインドする場合、Relayed Pushの実行時にテンプレートに対応する[付加価値サービス費用]https://intl.cloud.tencent.com/document/product/267/2819が発生します。

<span id="open_bypass"></span>
### Relayed Push機能をオンにする
1. TRTCコンソールに入って【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】を選択します。
2. 機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
3. 【Relayed Push設定】で、【Relayed Pushを有効】の右側のボタンをクリックします。
4. ポップアップした【Relayed Push機能をオンにする】のポップアップボックスで、**リスク説明にしっかりと目を通し**、アクティブ化について確認してから、【Relayed Push機能をオンにする】をクリックします。

<span id="select"></span>
### Relayed Push方式の選択
[Relayed Push機能をオン](#open_bypass)にした後、実際の業務の状況に応じてRelayed Pushの方式を選択することができます。

- **Relayed Push用指定ストリーム**：「Relayed Push用指定ストリーム」を選択後、MixTranscodingが必要ない場合は、クライアントSDK [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) インターフェースを呼び出して、Relayed Pushを直接開始してください。MixTranscodingが必要な場合は、 [Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) ドキュメントガイドに従って操作してください。MixTranscoding後にAuto-Relayed Pushが行われます。
- **Global Auto-relay**：「Global Auto-relay」を選択すると、すべてのTRTCのアップストリームのオーディオ/ビデオストリームはLVBシステムにAuto-relay Pushされます。


<span id="close__bypass"></span>
### Relayed Push機能をオフにする
Relayed Push機能を無効にしたい場合、具体的な操作手順は次のとおりです。
1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックし、機能設定を変更したいアプリケーションを選択して、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【Relayed Push設定】で、【Relayed Pushを有効】の右側のボタンをクリックします。
3. ポップアップした【Relayed Push機能をオフにする】のポップアップボックスで、**リスク説明にしっかりと目を通し**、無効化について確認してから、【Relayed Push機能をオフにする】をクリックします。


<span id="record"></span>
## クラウドレコーディングの設定

### 注意事項
- Relayed Pushを介して[LVB]https://intl.cloud.tencent.com/document/product/267を使用するTRTCサービスの機能は、完全なクラウドレコーディング機能を提供し、レコーディングされたファイルを[VOD]https://intl.cloud.tencent.com/document/product/266プラットフォームに保存します。
- レコーディング機能は、LVBサービスの機能を使用しており、当月のライブレコーディングの同時ピークチャネル数に基づいて、LVBのライブレコーディング料金が発生します。請求ルールの詳細については、[LVB > LVBレコーディングの料金の説明]https://intl.cloud.tencent.com/document/product/267/39605 をご参照ください。
- レコーディングされたファイルはVODプラットフォームに保存されるため、VODの保管料金が発生します。VODプラットフォームに保存されているレコーディングファイルのストレージ容量に基づいて課金されます。課金ルールの詳細は [VOD > ビデオストレージ（日次決済）価格説明](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください 。
- レコーディングされたビデオファイルを再生またはダウンロードする必要がある場合は、VODサービスのトラフィック（ビデオアクセラレーション）料金が発生し、ダウンストリームによってトラフィック課金がアクセラレーションされます。課金ルールの詳細は、[VOD> ビデオアクセラレーション（日次決済）料金説明](https://intl.cloud.tencent.com/document/product/266/14666) をご参照ください。
- クラウドレコーディング機能はデフォルトでオフになっています。クラウドレコーディング機能を有効にするには、LVBとVODのサービスをアクティブにする必要があります
- クラウドレコーディングはRelayed Pushに依存します。先に[Relayed Push](#open_bypass)を有効にしてください。


<span id="open_record"></span>
### クラウドレコーディング機能をオンにする
TRTCのクラウドレコーディングは、ルーム内の各ユーザーの音声・ビデオストリームをレコーディングして個別のファイルにすることができます。クラウドレコーディング機能を有効にしたい場合、詳しい操作ガイドは [クラウドレコーディングと再生の実現](https://intl.cloud.tencent.com/document/product/647/35426#open)をご参照ください。

<span id="change_record"></span>
### クラウドレコーディング設定の変更
>! クラウドレコーディングの設定を変更すると、オンラインで稼働中の作業データに影響を与える可能性があります。リスクを確認してから、注意して続行してください。

1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックし、クラウドレコーディング設定を変更したいアプリケーションを選択して、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【クラウドレコーディング設定】で、右側の【編集】をクリックしてクラウドレコーディング設定の変更画面に入ります。
4. 実際の状況に応じて [設定情報](https://intl.cloud.tencent.com/document/product/647/35426#recordType)を変更して、【OK】をクリックすれば、変更を保存できます。


<span id="close_record"></span>
### クラウドレコーディング機能をオフにする
クラウドレコーディングをオフにすると、オンラインで手動レコーディングや自動レコーディングなどのクラウドレコーディングを実行できなくなります。閉じる前に、業務でクラウドレコーディングが不要であることを確認してください。

1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックし、機能設定を変更したいアプリケーションを選択して、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【クラウドレコーディング設定】で、【クラウドレコーディングの起動】の右側のボタンをクリックします。
3.オフにした後の影響にしっかりと目を通し、クラウドレコーディングの無効について確認してから、【クラウドレコーディングをオフにする】をクリックします。



<span id="purview"></span>
## 高度な権限制御
あるルーム内に入室制限やマイク・オン制限を追加したい場合、つまり指定のユーザーだけにアクセスやマイク・オンを許可し、かつクライアントの権限を判断するに際してクラッキング攻撃に極めて遭いやすいことを懸念する場合は、[高度な権限制御を有効にする]https://intl.cloud.tencent.com/document/product/647/35157を検討することができます。


### 注意事項
高度な権限制御を有効にすると、現在のSDKAppIDの全てのユーザーは、入室するためにTRTCParamsでprivateMapKeyパラメータを正しく渡す必要があります。このSDKAppIDを使用するユーザーがオンラインにいる場合は、この機能を不用意に有効にしないでください。


### 高度な権限制御を有効にする
1. 【アプリケーション管理】をクリックして、高度な権限制御を有効にしたいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【高度な権限制御】で、右側の【高度な権限制御のオン】の右側ボタンをクリックします。

### 高度な権限制御を無効にする
1. 【アプリケーション管理】をクリックして、高度な権限制御を無効にしたいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【高度な権限制御】で、右側の【高度な権限制御のオフ】の右側ボタンをクリックします。

## 関連ドキュメント
- 新しいアプリケーションを作成する必要がある場合、操作の詳細は[アプリケーションの作成](https://intl.cloud.tencent.com/document/product/647/39077)をご参照ください。
- アプリケーションリストで関連アプリケーションを検索する必要がある場合、操作の詳細は[アプリケーション検索](https://intl.cloud.tencent.com/document/product/647/39078)をご参照ください。
- アプリケーションの基本情報を確認する必要がある場合、操作の詳細は[アプリケーション情報](https://intl.cloud.tencent.com/document/product/647/39079)をご参照ください。
- Cloud MixTranscoding時にカスタマイズした背景画像を設定したい場合、素材管理で対応する画像素材を追加できます。操作の詳細は[素材管理](https://intl.cloud.tencent.com/document/product/647/39081)をご参照ください。
- アプリケーションに付属のDemoソースコードをクイック実行する必要がある場合、操作の詳細は[クイックマスター](https://intl.cloud.tencent.com/document/product/647/39082)をご参照ください。





アプリケーション作成後、【機能設定】によって現在のアプリケーションの[Relayed Push](#bypass)、[クラウドレコーディング](#record)、[高度な権限制御](#purview)の機能を有効にできます。この画面の機能設定はいずれも変更完了の約5分後に有効化されます。

<span id="bypass"></span>
## Relayed Push設定

### 注意事項

- UDPトランスポートプロトコルに基づくTRTCサービスは、プロトコル変換を介してオーディオストリームとビデオストリームを [LVB]https://intl.cloud.tencent.com/document/product/267システムに接続します。このプロセスは「Relayed Push」と呼ばれます。
- デフォルトではRelayed Push機能はオフになっています。Relayed Push機能を有効にするには、先にLVBサービスをオンにする必要があります。
- [CDN Relayed live Streaming](https://intl.cloud.tencent.com/document/product/647/35242)にRelayed Pushを使用するとき、LVBでは、ライブストリーミングによって生成されたダウンストリームトラフィック/帯域幅に基づいて関連料金が請求されます。詳細については［LVB>トラフィック帯域幅課金］(https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#bill-by-traffic.2Fbandwidth)の説明をご参照ください。
- ［クラウドレコーディング］(https://intl.cloud.tencent.com/document/product/647/35426)にRelayed Pushを使用するとき、レコーディング、レコーディングファイルのストレージなどの料金が発生します。詳細は、[クラウドレコーディングと再生>関連費用](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8)の説明をご参照ください。
レコーディング、トランスコード、スクリーンキャプチャ、ポルノ検出、ウォーターマーク、およびその他の課金機能テンプレートをhttps://console.cloud.tencent.com/live/domainmanage[LVBコンソール]のRelayed Pushで使用されるプッシュドメイン名（xxxx.livepush.myqcloud.com）にバインドする場合、Relayed Pushの実行時にテンプレートに対応する[付加価値サービス費用]https://intl.cloud.tencent.com/document/product/267/2819が発生します。

<span id="open_bypass"></span>
### Relayed Push機能をオンにする
1. TRTCコンソールに入って【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】を選択します。
2. 機能設定を変更したいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
3. 【Relayed Push設定】で、【Relayed Pushを有効】の右側のボタンをクリックします。
4. ポップアップした【Relayed Push機能をオンにする】のポップアップボックスで、**リスク説明にしっかりと目を通し**、アクティブ化について確認してから、【Relayed Push機能をオンにする】をクリックします。

<span id="select"></span>
### Relayed Push方式の選択
[Relayed Push機能をオン](#open_bypass)にした後、実際の業務の状況に応じてRelayed Pushの方式を選択することができます。

- **Relayed Push用指定ストリーム**：「Relayed Push用指定ストリーム」を選択後、MixTranscodingが必要ない場合は、クライアントSDK [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) インターフェースを呼び出して、Relayed Pushを直接開始してください。MixTranscodingが必要な場合は、 [Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) ドキュメントガイドに従って操作してください。MixTranscoding後にAuto-Relayed Pushが行われます。
- **Global Auto-relay**：「Global Auto-relay」を選択すると、すべてのTRTCのアップストリームのオーディオ/ビデオストリームはLVBシステムにAuto-relay Pushされます。


<span id="close__bypass"></span>
### Relayed Push機能をオフにする
Relayed Push機能を無効にしたい場合、具体的な操作手順は次のとおりです。
1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックし、機能設定を変更したいアプリケーションを選択して、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【Relayed Push設定】で、【Relayed Pushを有効】の右側のボタンをクリックします。
3. ポップアップした【Relayed Push機能をオフにする】のポップアップボックスで、**リスク説明にしっかりと目を通し**、無効化について確認してから、【Relayed Push機能をオフにする】をクリックします。


<span id="record"></span>
## クラウドレコーディングの設定

### 注意事項
- Relayed Pushを介して[LVB]https://intl.cloud.tencent.com/document/product/267を使用するTRTCサービスの機能は、完全なクラウドレコーディング機能を提供し、レコーディングされたファイルを[VOD]https://intl.cloud.tencent.com/document/product/266プラットフォームに保存します。
- レコーディング機能は、LVBサービスの機能を使用しており、当月のライブレコーディングの同時ピークチャネル数に基づいて、LVBのライブレコーディング料金が発生します。請求ルールの詳細については、[LVB > LVBレコーディングの料金の説明]https://intl.cloud.tencent.com/document/product/267/39605 をご参照ください。
- レコーディングされたファイルはVODプラットフォームに保存されるため、VODの保管料金が発生します。VODプラットフォームに保存されているレコーディングファイルのストレージ容量に基づいて課金されます。課金ルールの詳細は [VOD > ビデオストレージ（日次決済）価格説明](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください 。
- レコーディングされたビデオファイルを再生またはダウンロードする必要がある場合は、VODサービスのトラフィック（ビデオアクセラレーション）料金が発生し、ダウンストリームによってトラフィック課金がアクセラレーションされます。課金ルールの詳細は、[VOD> ビデオアクセラレーション（日次決済）料金説明](https://intl.cloud.tencent.com/document/product/266/14666) をご参照ください。
- クラウドレコーディング機能はデフォルトでオフになっています。クラウドレコーディング機能を有効にするには、LVBとVODのサービスをアクティブにする必要があります
- クラウドレコーディングはRelayed Pushに依存します。先に[Relayed Push](#open_bypass)を有効にしてください。


<span id="open_record"></span>
### クラウドレコーディング機能をオンにする
TRTCのクラウドレコーディングは、ルーム内の各ユーザーの音声・ビデオストリームをレコーディングして個別のファイルにすることができます。クラウドレコーディング機能を有効にしたい場合、詳しい操作ガイドは [クラウドレコーディングと再生の実現](https://intl.cloud.tencent.com/document/product/647/35426#open)をご参照ください。

<span id="change_record"></span>
### クラウドレコーディング設定の変更
>! クラウドレコーディングの設定を変更すると、オンラインで稼働中の作業データに影響を与える可能性があります。リスクを確認してから、注意して続行してください。

1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックし、クラウドレコーディング設定を変更したいアプリケーションを選択して、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【クラウドレコーディング設定】で、右側の【編集】をクリックしてクラウドレコーディング設定の変更画面に入ります。
4. 実際の状況に応じて [設定情報](https://intl.cloud.tencent.com/document/product/647/35426#recordType)を変更して、【OK】をクリックすれば、変更を保存できます。


<span id="close_record"></span>
### クラウドレコーディング機能をオフにする
クラウドレコーディングをオフにすると、オンラインで手動レコーディングや自動レコーディングなどのクラウドレコーディングを実行できなくなります。閉じる前に、業務でクラウドレコーディングが不要であることを確認してください。

1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】をクリックし、機能設定を変更したいアプリケーションを選択して、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【クラウドレコーディング設定】で、【クラウドレコーディングの起動】の右側のボタンをクリックします。
3.オフにした後の影響にしっかりと目を通し、クラウドレコーディングの無効について確認してから、【クラウドレコーディングをオフにする】をクリックします。



<span id="purview"></span>
## 高度な権限制御
あるルーム内に入室制限やマイク・オン制限を追加したい場合、つまり指定のユーザーだけにアクセスやマイク・オンを許可し、かつクライアントの権限を判断するに際してクラッキング攻撃に極めて遭いやすいことを懸念する場合は、[高度な権限制御を有効にする]https://intl.cloud.tencent.com/document/product/647/35157を検討することができます。


### 注意事項
高度な権限制御を有効にすると、現在のSDKAppIDの全てのユーザーは、入室するためにTRTCParamsでprivateMapKeyパラメータを正しく渡す必要があります。このSDKAppIDを使用するユーザーがオンラインにいる場合は、この機能を不用意に有効にしないでください。


### 高度な権限制御を有効にする
1. 【アプリケーション管理】をクリックして、高度な権限制御を有効にしたいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【高度な権限制御】で、右側の【高度な権限制御のオン】の右側ボタンをクリックします。

### 高度な権限制御を無効にする
1. 【アプリケーション管理】をクリックして、高度な権限制御を無効にしたいアプリケーションを選択し、対象のアプリケーションがある行の【機能設定】をクリックします。
2. 【機能設定】>【高度な権限制御】で、右側の【高度な権限制御のオフ】の右側ボタンをクリックします。

## 関連ドキュメント
- 新しいアプリケーションを作成する必要がある場合、操作の詳細は[アプリケーションの作成](https://intl.cloud.tencent.com/document/product/647/39077)をご参照ください。
- アプリケーションリストで関連アプリケーションを検索する必要がある場合、操作の詳細は[アプリケーション検索](https://intl.cloud.tencent.com/document/product/647/39078)をご参照ください。
- アプリケーションの基本情報を確認する必要がある場合、操作の詳細は[アプリケーション情報](https://intl.cloud.tencent.com/document/product/647/39079)をご参照ください。
- Cloud MixTranscoding時にカスタマイズした背景画像を設定したい場合、素材管理で対応する画像素材を追加できます。操作の詳細は[素材管理](https://intl.cloud.tencent.com/document/product/647/39081)をご参照ください。
- アプリケーションに付属のDemoソースコードをクイック実行する必要がある場合、操作の詳細は[クイックマスター](https://intl.cloud.tencent.com/document/product/647/39082)をご参照ください。




