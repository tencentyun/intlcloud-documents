[IMコンソール](https://console.cloud.tencent.com/im)にログインし、対象のアプリケーションカードをクリックして、アプリケーションの基本設定ページに進みます。実際の業務に応じて、アプリケーションの基本設定を管理することができます。

## サービスバージョンの変更

【サービスバージョン】エリアの【アップグレード】をクリックすると、アプリケーションのサービスバージョンや設定をアップグレードすることができます。具体的な操作については、 [アプリケーションのアップグレード](https://intl.cloud.tencent.com/document/product/1047/34577)をご参照ください。

## 基本情報の設定
![](https://main.qcloudimg.com/raw/867f34d67ddcca7de31ff17327dee744.png)
【基本情報】エリアでは、次の操作を行うことができます。
- アプリケーション名、アプリケーションタイプ、アプリケーションの説明など、このアプリケーションの基本情報を編集します。
- このアプリケーションを使用停止/削除します。
- このアプリケーションのキーを取得します。

### 基本情報の編集
1. 【アプリケーション情報】の右側の【編集】をクリックして、アプリケーション設定の編集状態に入ります。
2. 【アプリケーション名】、【アプリケーションタイプ】および【アプリケーションの説明】を変更することができます。
3. 【保存】をクリックします。

### アプリケーションの使用停止/削除
>同じTencent Cloudのアカウントで、最大100個のIMアプリケーションを作成することができます。すでにアプリケーションが100個ある場合は、必要のないアプリケーションを先に使用停止し削除すると、新しいアプリケーションを作成することができます。
>**ステータスが【使用停止】のアプリケーションのみ、削除できます。アプリケーションを削除すると、そのSDKAppIDに対応するすべてのデータとサービスが失われます。慎重に操作を行ってください。**



**体験版アプリケーション**
- 手動で使用停止にできます。
 【基本情報】エリアで、【状態】の右側にある【使用停止】をクリックし、ポップアップ表示されたダイアログボックスで【OK】をクリックすると使用停止になります。
- 手動で削除できます。
 【基本情報】エリアで、【状態】の右側にある【削除】をクリックし、ポップアップ表示されたダイアログボックスで【OK】をクリックすると削除されます。

**プロフェッショナル版/フラッグシップ版**
- 料金の支払いが7日遅れるとステータスが自動的に【使用停止】になります。削除が必要な場合は、 [お問い合わせ](https://console.cloud.tencent.com/workorder/category) ください。
- 返金後は【期限切れ】状態になり、7日後には【使用停止】状態になります。削除する必要がある場合は、[お問い合わせ](https://console.cloud.tencent.com/workorder/category) ください。

**TRTC体験版**
TRTC側でアプリケーションを使用停止にした後、 [お問い合わせ](https://console.cloud.tencent.com/workorder/category) してから、このアプリケーションを使用停止して削除することができます。


### キーの取得
**キー情報はセンシティブな情報ですので、適切に機密を保持し、漏洩しないようご注意ください。**2019年8月15日より前に作成されたアプリケーション（SDKAppID）は、デフォルトで公開鍵と秘密鍵を区別する[ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/1047/34385)署名アルゴリズムを使用するためHMAC-SHA256署名アルゴリズムへのアップグレードを選択することができます。

1. 【キー】の右側にある【キーの表示】をクリックします。
2. 【コピー】をクリックすると、キー情報をコピーして保存できます。
    キーはUserSigの生成に使用することができます。詳細な操作については、[UserSigの生成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

## アカウント管理者の設定
アカウント管理者は、REST APIインターフェースの呼び出し、グループの解散、その他の機能に使用することができます。お客様は、システムのデフォルトのアカウント管理者 `administrator` を直接使用したり、アカウント管理者を手動で追加したりすることもできます。各アプリケーションには5個のアカウント管理者をサポートしています。
![](https://main.qcloudimg.com/raw/9cf8914c53cb998fd7ee619ef30836a9.jpg)
<span id="AddAdmin"></span>
###  管理者の追加
1. 【アカウント管理者】の右側にある【管理者の追加】をクリックします。
2.  ポップアップ表示された管理者の追加ダイアログボックスに、管理者アカウント名を入力します。
3.  【追加】をクリックします。

### 管理者の削除
1. 【アカウント管理者】の右側にある【管理者の削除】をクリックします。
2. ポップアップ表示された管理者の削除ダイアログボックスで、削除する管理者アカウントにチェックを入れます。
3. 【削除の確認】をクリックします。

## オフラインプッシュ証明書の管理

### オフラインプッシュ証明書の追加

1. 対応するプラットフォームのプッシュ設定エリアで【証明書の追加】をクリックします。
2. ポップアップ表示された証明書の追加ダイアログボックスに従って、関連パラメータを設定します。
 - Android証明書の追加
 ![](https://main.qcloudimg.com/raw/7821c57eef8b7a63019df23eb347720f.jpg)
 - iOS証明書の追加
 ![](https://main.qcloudimg.com/raw/dc629d1f3ae746e699919930b1f99024.png)
3. 【確定】をクリックして設定を保存します。

### オフラインプッシュ証明書の編集
1. 既存の証明書エリアの【編集】をクリックします。
2. ポップアップ表示されたダイアログボックスで関連パラメータを変更し、【確定】をクリックして設定を保存します。

### オフラインプッシュ証明書の削除
>証明書を削除すると、プッシュメッセージは配達されなくなり、削除後はデータを復元できません。慎重に操作を行ってください。

1. 既存の証明書エリアの【削除】をクリックします。
2. ポップアップ表示された証明書の削除確認において、【確認】をクリックします。

## TRTCサービスのアクティブ化
現在のIMアプリケーションに、音声通話、ビデオ通話、ILVBなどの機能が必要な場合、またはIM SDKとTRTC SDKを同時に統合する必要がある場合は、【TRTCサービスのアクティブ化】エリアで [TRTCサービス](https://intl.cloud.tencent.com/document/product/647)をアクティブにすると、システムは[TRTCコンソール](https://console.cloud.tencent.com/trtc)の現在のIMアプリケーションと同じSDKAppIDを使用してTRTCアプリケーションを作成します。2つのアカウントと認証は再利用できます。

1. 【TRTCサービスのアクティブ化】エリアで【今すぐアクティブにする】をクリックします。
2. ポップアップ表示されたTRTCサービスのアクティブ化のダイアログボックスで、【確定】をクリックします。
