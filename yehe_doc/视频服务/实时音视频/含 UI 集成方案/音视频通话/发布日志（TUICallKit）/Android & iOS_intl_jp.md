>? **新バージョン（1.1.0.103）のTUICallEngineインターフェースに関連する変更：**
>- 開発中に、maven latest更新メカニズムが原因でAndroid構築エラーが発生した場合は、次の2つの方法で解決できます。
	  - TUICallKitを最新バージョンにアップグレードする。
	  - tuicallkit/build.gradleのtuicallengineを1.0の固定バージョン：`com.tencent.liteav.tuikit:tuicallengine:1.0.0.53`に依存するよう変更する。
>- 開発中に、pod updateの実行が原因でiOS構築エラーが発生した場合は、次の2つの方法で解決できます。
	  - TUICallKitを最新バージョンにアップグレードする。
	  - Podfileファイルに`pod 'TUICallEngine'、'1.0.0.53'`を追加する。

### Version 1.1.0.103  @ 2022.09.30
- Android&iOS：グループ通話中のグループメンバー招待機能を最適化しました。
- Android&iOS：通話フローで、通話応答前にレコーディング、審査などの料金が発生しないように改善しました。
- Android&iOS：カスタムオーディオビデオ通話のオフラインプッシュメッセージをサポートしました。
- Android&iOS：一部の**TUICallEngine**インターフェースパラメータを変更しました。詳細については、[call()](https://www.tencentcloud.com/document/product/647/51006#call)、[groupCall()](https://www.tencentcloud.com/document/product/647/51006#groupcall)、[inviteUser()](https://www.tencentcloud.com/document/product/647/51006#inviteuser)、およびコールバックインターフェース[onCallReceived()](https://www.tencentcloud.com/document/product/647/51007#oncallreceived)をご参照ください。
- Android&iOS：グループ通話中に、少量のコールバックの異常が発生することがある問題を修正しました。
- Android&iOS：重複ログインおよびUserSigの期限切れによるステータス異常の問題を修正しました。
- iOS：TUCallKit Objective-CとSwiftの混合コンパイルの際に、`init`インターフェースエラーが発生する問題を修正しました。
- Android：Kotlinでのフローティングウィンドウ機能統合の際にコンパイルエラーが発生する問題を修正しました。

### Version 1.0.0.53   @ 2022.08.15

#### 新規リリース： 
- Android&iOS：1v1オーディオビデオ通話、グループオーディオビデオ通話をサポートしました。
- Android&iOS：主要メーカーのオフライン通知をサポートしました。
- Android&iOS：プロフィール画像のカスタマイズ、ニックネームのカスタマイズをサポートしました。
- Android&iOS：通話中のフローティングウィンドウ有効化をサポートしました。
- Android&iOS：カスタム着信音の設定をサポートしました。
- Android&iOS：複数のプラットフォームにログインした状態での着信サービスをサポートしました。