>!ここでは主に**Tencent Real-Time CommunicationTRTC **のCloud Access Management（CAM）機能関連コンテンツについて紹介します。他製品のCAM関連コンテンツについては、[CAMサポート製品](https://intl.cloud.tencent.com/document/product/598/10588)をご参照ください。

CAMのコア機能は、**特定のアカウントが特定のリソースに対して何らかの操作を実行することを許可または禁止する**と表すことができます。TRTC CAMは、[リソースレベルの承認](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B)をサポートし、リソースの粒度は[TRTC アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)、操作の粒度は[Tencent Cloud API](https://intl.cloud.tencent.com/product/api)であり、[サーバーAPI](https://intl.cloud.tencent.com/document/product/647/34260)とTRTC コンソールにアクセスするときに使用する可能性のあるAPIを含みます。

TRTC CAMを管理する必要がある場合、Tencent Cloud [ルートアカウント](https://intl.cloud.tencent.com/document/product/598/34899)にログインし、[プリセットポリシー](https://intl.cloud.tencent.com/document/product/647/39550)または[カスタムポリシー](https://intl.cloud.tencent.com/document/product/647/39551)を使用して、具体的な認証操作を完了します。


## 承認可能なリソースタイプ
TRTC CAMが承認可能なリソースタイプは、[アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)です。


## リソースレベルの承認をサポートするAPI[](id:Support)
一部の[リソースレベルの承認をサポートしないAPI](#n_Support)を除いて、このセクションにリストアップされているAPI操作は、リソースレベルの承認をサポートします。 [アクセスポリシー構文](https://intl.cloud.tencent.com/document/product/647/39551#grammar)のこれらのAPI操作の**リソース構文の記述**は、いずれも同じです。具体的には次のとおりです。
- すべてのアプリケーションアクセス権限を承認する：`qcs::trtc::uin/${uin}:sdkappid/*`。
- 単一のアプリケーションアクセス権限を承認する：`qcs::trtc::uin/${uin}:sdkappid/${SdkAppId}`。

### サーバーAPIの操作
| インターフェース名                                                     |インターフェースの分類     | 機能の説明               |
| ------------------------------------------------------------ | ------------ | ---------------------- |
| [DismissRoom](https://intl.cloud.tencent.com/document/product/647/39631) | ムール管理     | ムールの解散               |
| [RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) | ルーム管理     | ユーザーの削除               |
|[RemoveUserByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39630)	| ルーム管理	| ユーザーの削除（文字列のルームナンバー） |
|[DismissRoomByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39631)	| ルーム管理	| ルームの解散（文字列のルームナンバー） |
| [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) | ミクスストリーミングトランスコード     | クラウドミクスストリーミングの起動           |
| [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) | ミクスストリーミングトランスコード     | Cloud MixTranscodingの終了           |
| [StartMCUMixTranscodeByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39637) | ミクスストリーミングトランスコード |クラウドミクスストリーミングの起動（文字列のルームナンバー） |
| [StopMCUMixTranscodeByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39636) | ミクスストリーミングトランスコード  |クラウドミクスストリーミングの終了（文字列のルームナンバー） |
| [CreateTroubleInfo](https://intl.cloud.tencent.com/document/product/647/37764) | 通話品質の監視 | 異常情報の作成           |
| [DescribeAbnormalEvent](https://intl.cloud.tencent.com/document/product/647/37763) |通話品質の監視 | 異常体験イベントの確認       |
| [DescribeCallDetail](https://intl.cloud.tencent.com/document/product/647/36759) | 通話品質の監視 | ユーザーリストと通話インジケータの確認    |
| [DescribeHistoryScale](https://intl.cloud.tencent.com/document/product/647/36758) | 通話品質の監視 | ルーム履歴とユーザー数の確認      |
| DescribeRealtimeNetwork | 通話品質の監視 | リアルタイムネットワーク状態の照会       |
| DescribeRealtimeQuality | 通話品質の監視 | リアルタイム品質データの照会       |
| DescribeRealtimeScale | 通話品質の監視 | リアルタイムスケールの照会           |
| [DescribeRoomInformation](https://intl.cloud.tencent.com/document/product/647/36754) | 通話品質の監視 | ルームリストの確認           |
| [DescribeUserInformation](https://intl.cloud.tencent.com/document/product/647/39096) | 通話品質の監視 | 過去のユーザーリストの照会 |




### コンソールAPIの操作
<table>
<thead><tr><th >インターフェース名</th><th>使用モジュール</th><th width="38%">機能の説明</th></tr></thead>
<tbody><tr>
<td>DescribeAppStatList</td>
<td>TRTCコンソール<ul style="margin:0">
<li> <a href="https://console.cloud.tencent.com/trtc">概要</a> 
<li><a href="https://console.cloud.tencent.com/trtc/statistics">使用量の統計</a>
<li><a href="https://console.cloud.tencent.com/trtc/monitor">監視ダッシュボード</a>
<li><a href="https://console.cloud.tencent.com/trtc/usersigtool">開発支援 &gt; UserSig 生成&amp;検証</a> 
<li><a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理</a>
</ul></td>
<td>アプリケーションリストの取得</td>
</tr><tr>
<td>DescribeSdkAppInfo</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; アプリケーション情報</a></td>
<td>アプリケーション情報の取得</td>
</tr><tr>
<td>ModifyAppInfo</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; アプリケーション情報</a></td>
<td>アプリケーション情報の編集</td>
</tr><tr>
<td>ChangeSecretKeyFlag</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; アプリケーション情報</a></td>
<td>権限キーのステータスの変更</td>
</tr><tr>
<td>CreateWatermark</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 素材管理</a></td>
<td>画像のアップロード</td>
</tr><tr>
<td>DeleteWatermark</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 素材管理</a></td>
<td>画像の削除</td>
</tr><tr>
<td>ModifyWatermark</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 素材管理</a></td>
<td>画像の編集</td>
</tr><tr>
<td>DescribeWatermark</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 素材管理</a></td>
<td>画像の検索</td>
</tr><tr>
<td>CreateSecret</td>
<td>TRTCコンソール <a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; クイックマスター</a></td>
<td>対称暗号化鍵の作成</td>
</tr><tr>
<td>ToggleSecretVersion</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; クイックマスター</a></td>
<td>キーバージョンの切り替え（公開鍵・秘密鍵/対称暗号化鍵）</td>
</tr><tr>
<td>DescribeSecret</td>
<td>TRTCコンソール<ul style="margin:0">
<li><a href="https://console.cloud.tencent.com/trtc/quickstart">開発支援 &gt; Demoクイックスタート</a>
<li><a href="https://console.cloud.tencent.com/trtc/usersigtool">開発支援 &gt; UserSig 生成&amp;検証</a>
<li><a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; クイックマスター</a>
</ul></td>
<td>対称暗号化鍵の取得</td>
</tr><tr>
<td>DescribeTrtcAppAndAccountInfo</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/usersigtool">開発支援 &gt; UserSig 生成&amp;検証</a></td>
<td>アプリケーションとアカウント情報、公開鍵・秘密鍵の取得</td>
</tr><tr>
<td>CreateSecretUserSig</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/usersigtool">開発支援 &gt; UserSig 生成&amp;検証</a></td>
<td>対称暗号化鍵を使用してUserSigを生成</td>
</tr><tr>
<td>DescribeSig</td>
<td>TRTCコンソール<ul style="margin:0">
<li><a href="https://console.cloud.tencent.com/trtc/usersigtool">開発支援 &gt; UserSig 生成&amp;検証</a>
<li> <a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; クイックマスター</a>
</ul></td>
<td>旧バージョンの公開鍵・秘密鍵を使用して生成されたUserSigを取得</td>
</tr><tr>
<td>VerifySecretUserSig</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/usersigtool">開発支援 &gt; UserSig 生成&amp;検証</a></td>
<td>対称暗号化鍵生成のUserSig検証</td>
</tr><tr>
<td>VerifySig</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/usersigtool">開発支援 &gt; UserSig 生成&amp;検証</a></td>
<td>公開鍵・秘密鍵で生成されたUserSig検証</td>
</tr>
<tr>
<td>CreateSpearConf</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 画面設定</a></td>
<td>画面設定の構成を追加しました。 この機能設定カードは、iLiveSDK1.9.6以前のバージョンでのみ表示されます。TRTC SDK 6.0以降のバージョンについては、<a href="https://intl.cloud.tencent.com/document/product/647/35153">画質設定</a> をご参照ください</td>
</tr>
<tr>
<td>DeleteSpearConf</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 画面設定</a></td>
<td>画面設定の構成を削除しました。 この機能設定カードは、iLiveSDK1.9.6以前のバージョンでのみ表示されます。TRTC SDK 6.0以降のバージョンについては、<a href="https://intl.cloud.tencent.com/document/product/647/35153">画質設定</a> をご参照ください</td>
</tr>
<tr>
<td>ModifySpearConf</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 画面設定</a></td>
<td>画面設定の構成を変更しました。 この機能設定カードは、iLiveSDK1.9.6以前のバージョンでのみ表示されます。TRTC SDK 6.0以降のバージョンについては、<a href="https://intl.cloud.tencent.com/document/product/647/35153">画質設定</a> をご参照ください</td>
</tr>
<tr>
<td>DescribeSpearConf</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 画面設定</a></td>
<td>画面設定の構成を取得しました。 この機能設定カードは、iLiveSDK1.9.6以前のバージョンでのみ表示されます。TRTC SDK 6.0以降のバージョンについては、<a href="https://intl.cloud.tencent.com/document/product/647/35153">画質設定</a> をご参照ください</td>
</tr>
<tr>
<td>ToggleSpearScheme</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 画面設定</a></td>
<td>画面設定のシナリオを切り替えました。 この機能設定カードは、iLiveSDK1.9.6以前のバージョンでのみ表示されます。TRTC SDK 6.0以降のバージョンについては、<a href="https://intl.cloud.tencent.com/document/product/647/35153">画質設定</a> をご参照ください</td>
</tr>
</tbody></table>


## リソースレベルの承認をサポートしないAPI[](id:n_Support)
特殊な制限により、次のAPIはリソースレベルの承認をサポートしていません。

### サーバーAPIの操作
|インターフェース名|インターフェースの分類|機能の説明|特殊な制限の説明|
|---|---|---|---|
|[DescribeDetailEvent](https://intl.cloud.tencent.com/document/product/647/37762)|通話品質の監視|詳細なイベントを取得|入力パラメータにSDKAppIDがないため、リソースレベルの認証を実行できません。|
| [DescribeRecordStatistic](https://intl.cloud.tencent.com/document/product/647/42972) | その他インターフェース |クラウドレコーディング課金時間の照会  |業務上の理由により、現在のところ、リソースレベルの承認をサポートしていません |
| [DescribeTrtcInteractiveTime](https://intl.cloud.tencent.com/document/product/647/42971) | その他インターフェース |インタラクティブオーディオビデオ課金時間の照会 |業務上の理由により、現在のところ、リソースレベルの承認をサポートしていません |
| [DescribeTrtcMcuTranscodeTime](https://intl.cloud.tencent.com/document/product/647/42970) |  その他インターフェース |バイパストランスコード課金時間の照会   |業務上の理由により、現在のところ、リソースレベルの承認をサポートしていません |

### コンソールAPIの操作
<table>
<thead><tr><th >インターフェース名</th><th width="20%">使用モジュール</th><th width="15%">機能の説明</th></tr>特殊な制限の説明</th></tr></thead>
<tbody><tr>
<td>DescribeTrtcStatistic</td>
<td>TRTCコンソール<ul style="margin:0">
<li><a href="https://console.cloud.tencent.com/trtc">概要</a> 
<li><a href="https://console.cloud.tencent.com/trtc/statistics">使用量の統計</a>
</ul></td>
<td>課金期間中の使用量統計データの取得</td>
<td>このインターフェースには、完全なSDKAppIDを返す統計データが含まれています。不完全なSDKAppIDを制限すると、エラーが返されます。 必要に応じて、DescribeAppStatListインターフェースを介してクエリーできるアプリケーションのリストを制限できます</td>
</tr>
<tr>
<td>DescribeDurationPackages</td>
<td>TRTCコンソール<ul style="margin:0">
<li> <a href="https://console.cloud.tencent.com/trtc">概要</a>
<li><a href="https://console.cloud.tencent.com/trtc/package">パッケージ管理</a>
</ul></td>
<td>前払いパッケージリストの取得</td>
<td>前払いパッケージは単一のTencent CloudアカウントですべてのTRTCアプリによって共有されます。パッケージ情報にSDKAppIDパラメータがないため、リソースレベルの認証を実行できません</td>
</tr>
<tr>
<td>GetUserList</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/monitor">監視ダッシュボード</a></td>
<td>ユーザーリストの取得</td>
<td>入力パラメータにSDKAppIDがないため、リソースレベルの認証を実行できません。必要に応じて、DescribeAppStatListインターフェースを介してクエリーできるアプリケーションのリストを制限できます</td>
</tr>
<tr>
<td>GetUserInfo</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/monitor">監視ダッシュボード</a></td>
<td>ユーザー情報の取得</td>
<td>入力パラメータにSDKAppIDがないため、リソースレベルの認証を実行できません。必要に応じて、DescribeAppStatListインターフェースを介してクエリーできるアプリケーションのリストを制限できます</td>
</tr>
<tr>
<td>GetCommState</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/monitor">監視ダッシュボード</a></td>
<td>通話情報の取得</td>
<td>入力パラメータにSDKAppIDがないため、リソースレベルの認証を実行できません。必要に応じて、DescribeAppStatListインターフェースを介してクエリーできるアプリケーションのリストを制限できます</td>
</tr>
<tr>
<td>GetElasticSearchData</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/monitor">監視ダッシュボード</a></td>
<td>ESデータのクエリー</td>
<td>入力パラメータにSDKAppIDがないため、リソースレベルの認証を実行できません。必要に応じて、DescribeAppStatListインターフェースを介してクエリーできるアプリケーションのリストを制限できます</td>
</tr>
<tr>
<td>CreateTrtcApp</td>
<td>TRTCコンソール <ul>
<li><a href="https://console.cloud.tencent.com/trtc/quickstart">開発支援 &gt; Demoクイックスタート</a> 
<li><a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理</a>
</ul></td>
<td>TRTCアプリケーションの作成</td>
<td>入力パラメータにSDKAppIDがないため、リソースレベルの認証を実行できません。SDKAppIDはTRTCアプリケーションの一意の識別子であり、SDKAppID情報はアプリケーションの作成後にのみ利用できます</td>
</tr>
<tr>
<td>HardDescribeMixConf</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 機能設定</a></td>
<td>Auto-Relayed Pushのステータスのクエリー</td>
<td>入力パラメータにSDKAppIDがないため、リソースレベルの認証を実行できません。必要に応じて、DescribeAppStatListインターフェースを介してクエリーできるアプリケーションのリストを制限できます</td>
</tr>
<tr>
<td>ModifyMixConf</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/app">アプリケーション管理 &gt; 機能設定</a></td>
<td>Auto-Relayed Pushのオン/オフ</td>
<td>入力パラメータにSDKAppIDがないため、リソースレベルの認証を実行できません。必要に応じて、DescribeAppStatListインターフェースを介してクエリーできるアプリケーションのリストを制限できます</td>
</tr>
<tr>
<td>RemindBalance</td>
<td>TRTCコンソール<a href="https://console.cloud.tencent.com/trtc/package">パッケージ管理</a></td>
<td>前払いパッケージ残高アラート情報の取得</td>
<td>前払いパッケージは単一のTencent CloudアカウントですべてのTRTCアプリによって共有されます。パッケージ情報にSDKAppIDパラメータがないため、リソースレベルの認証を実行できません</td>
</tr>
</tbody></table>

>! リソースレベルの承認をサポートしないAPI操作の場合でも、[カスタムポリシー](https://intl.cloud.tencent.com/document/product/647/39551)を介してユーザーに操作を使用する権限を付与できます。ただし、ポリシーステートメントのリソース要素は、必ず`*`と指定する必要があります。
