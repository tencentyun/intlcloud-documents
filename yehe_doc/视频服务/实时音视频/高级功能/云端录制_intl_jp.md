ビジネス用オーディオ・ビデオのソリューションでは、証拠、品質検査、査定、保存などのユースケースを考慮して、レコーディングのニーズがあると想定しています。TRTCサービスでは [LVB](https://intl.cloud.tencent.com/document/product/267) のサービス能力を使用して全体的なクラウドレコーディング機能を提供し、レコーディングしたファイルは [Video on Demand](https://intl.cloud.tencent.com/document/product/266) プラットフォームを通じて取得できます。


>?
>- クラウドレコーディング機能は、デフォルトでは無効になっているので、クラウドレコーディング機能を起動するには、まず [LVB](https://console.cloud.tencent.com/live) および [VOD](https://console.cloud.tencent.com/vod) サービスをアクティブにする必要があります。
>- クラウドレコーディング機能を使用した場合は、LVBサービスのレコーディング料金およびVODサービスの保管料金が発生します。レコーディングしたビデオファイルを再生またはダウンロードする場合は、VODサービスのトラフィック料金（ビデオアクセラレーション）も発生します。料金規定の詳細は [クラウドレコーディング関連料金](https://intl.cloud.tencent.com/document/product/647/34614#.E4.BA.91.E7.AB.AF.E5.BD.95.E5.88.B6.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8) ファイルをご参照ください。 

## プラットフォームのサポート

|   iOS    | Android  |  Mac OS  | Windows  | WeChat Mini Program| Chrome ブラウザ |
| :------: | :------: | :------: | :------: | :--------: | :----------: |
| &#10003; | &#10003; | &#10003; | &#10003; |  &#10003;  |   &#10003;   |

## クラウドレコーディングの起動

1.  [LVB](https://console.cloud.tencent.com/live) および [VOD](https://console.cloud.tencent.com/vod) サービスの両方がアクティブになっていることを確認します。
2.  [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc) にログインし、【アプリケーション管理】ページに入り、【Relayed live streaming】が“使用可能”状態にあることを確認してください。【Relayed live streaming】が“使用不可”の状態にある場合は、アプリケーションリスト右側の【機能設定】をクリックすると、対応する設定ページにて起動させることができます。
3. 【アプリケーション管理】ページで、【グローバルクラウドレコーディング設定】をクリックして【グローバルクラウド自動レコーディング】を起動し、レコーディングファイルのフォーマットを設定します。

    グローバルクラウド自動レコーディングを起動すると、現在のTencent CloudアカウントでTRTCアプリケーションによって自動レコーディングされるすべてのビデオフォーマットは、設定した保存フォーマットで保存されます。

## ミキシング画面

Tencent Real-Time Communicationのオーディオ・ビデオルームのデフォルトでは、ミクスストリーミング機能は無効になっています。クラウドレコーディング機能を有効にしてから、デフォルトはTRTC ルームの各1ストリーム（メインストリームおよびサブストリーム）のアップストリームのビデオのみレコーディングできます。ミキシング後の画面をレコーディングしたい場合は、 [Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618)を使用する必要があります。すなわち、 TRTCCloud の `setMixTranscodingConfig` インターフェースをコールすれば、ミキシング画面のビデオを一個の独立したファイルに録画できます。

## ビデオファイルの取得


### 方法一：コンソールの検索

VODコンソールの [ビデオ管理](https://console.cloud.tencent.com/vod/media) インターフェースで、録画したビデオファイルを検索できます。Tencent Cloud公式サイトの [Demo](https://intl.cloud.tencent.com/document/product/647/35076) を例に、具体的な操作プロセスは次のとおりです。

1. Tencent Cloud公式サイトの Demo のアカウントのLVB bizid は3891です。 [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/rav) > 【アプリケーション管理】>【アプリケーション情報】>【Relayed live streaming情報】からこの bizidを検索できます。
2.  Demo を使って一個のライブルームを新規作成し、ID を `12345`、ユーザー名を `userA`とし、そのルームに対応するライブストリーム ID を`MD5(12345_userA_main)`に計算できます。すなわち、`3891_8d0261436c375bb0dea901d86d7d70e8`です。具体的な計算方法は、ファイル [CDN Relayed live streaming](https://intl.cloud.tencent.com/document/product/647/34617) のライブアドレスの取得についての説明を参照できます。
3. ライブルームの退出では、VODコンソールの [ビデオ管理](https://console.cloud.tencent.com/vod/media) インターフェースで該当するファイルを直接検索するか、ライブストリームIDを用いてプレフィックス検索を実行して該当ファイルを検索します。




### 方法二：REST API 検索

VODサービスが提供する REST API [SearchMedia インターフェース](https://intl.cloud.tencent.com/document/product/266/34179) をコールして、その StreamId パラメータを指定し、レコーディングファイルを検索することができます。StreamId（すなわちライブストリーム ID）の取得方法は [CDN Relayed live streaming](https://intl.cloud.tencent.com/document/product/647/34617) のライブストリーミングアドレス取得についての説明を参照してください。
