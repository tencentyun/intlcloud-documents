## ユースケース
Appでバックグラウンドを停止するか、プロセスが強制終了になった場合において、ユーザーに通知すべき新しいメッセージがあるときは、オフラインプッシュ機能を使用することができます。iOSでAPNsプッシュがある場合、Androidでは、ユーザーがオフラインメッセージのコールバックを登録する必要があります。

## iOS APNsプッシュ
### プッシュ形式の説明

![](https://main.qcloudimg.com/raw/8bb11ef0a0ff210c1b0a1ab65da63c2f.png)


上図は、シングルチャットメッセージとグループチャットメッセージの事例です。
iOS APNsプッシュ形式の詳細については、[プッシュ形式の説明](https://intl.cloud.tencent.com/document/product/1047/34347)をご参照ください。

### 基本インターフェースの説明
APNをサポートするには、次のインターフェースを呼び出す必要があります。詳細については、[iOS APNsイベントレポート](https://intl.cloud.tencent.com/document/product/1047/34347)をご参照ください。
- Tokenを設定します。
- バックグラウンドに切り替えて未読を報告します。
- フォアグラウンドに切り替えて通知します。

### Ext拡張の設定
アプリケーションは状況に応じて、プッシュされたExt拡張フィールドを設定する必要がある場合があります。これは、ユーザーがリダイレクトをクリックするなどの操作を行う際に便利です。TIMCustomElemのExtフィールドに入力することができ、プッシュすると、IMバックエンドがこのフィールドをExtに入力します。拡張フィールドをカスタマイズする場合、[オフラインメッセージプロパティのカスタマイズ](https://intl.cloud.tencent.com/document/product/1047/34347)をご参照ください。

### プッシュ音の設定
アプリケーションは状況に応じて、単一のメッセージのプッシュ音を設定する必要があります。これは、特定タイプのメッセージのリマインド通知に便利です。サウンドをTIMCustomElemのsoundフィールドに入力でき、プッシュすると、IMバックエンドがこのフィールドをExtに入力します。[プッシュ通知音のカスタム設定](https://intl.cloud.tencent.com/document/product/1047/34347)をご参照ください。

## Androidオフラインプッシュ
Androidは、バージョン1.8.0以降、サービスとプロセスの分離をサポートしています。Appプロセスが強制終了になった場合もサービスは引き続き有効であり、オフラインプッシュ機能を受信することができます。具体的なコンフィグレーションや設定プロセスについては、[Androidオフラインプッシュ](https://intl.cloud.tencent.com/document/product/1047/34336)ドキュメントをご参照ください。

## バックエンドからのメッセージ送信
バックエンドからメッセージを送信するときは、iOSの場合、[プッシュ形式](https://intl.cloud.tencent.com/document/product/1047/34347)を参照して、APNsプッシュの表示形式を設定することができます。Androidの場合、[オフラインプッシュOfflinePushInfo](https://intl.cloud.tencent.com/document/product/1047/33527)を参照して設定することができます。

## 関連ドキュメント
- [オフラインプッシュ証明書の管理](https://intl.cloud.tencent.com/document/product/1047/34540)
- [Appleプッシュ証明書の申請](https://intl.cloud.tencent.com/document/product/1047/34346)
- [iOSオフラインプッシュの設定](https://intl.cloud.tencent.com/document/product/1047/34347)
- [Androidオフラインプッシュの基本設定](https://intl.cloud.tencent.com/document/product/1047/34336)
