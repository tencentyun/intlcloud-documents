CSSは、Widevine、Fairplay、NormalAESのDRM暗号化プロトコルをベースとするビデオライブストリーミングの暗号化、レコーディングの防止、リンク不正アクセス防止などのサービスを提供し、ユーザーのビデオコンテンツをあらゆる面から保護します。ここでは主に、コンソールからDRM暗号化機能を使用する操作手順についてご説明します。

## 注意事項
Tencent Cloudは、ビデオストリームの暗号化操作のみを提供し、DRM暗号化の証明書管理は、サードパーティのサービスプロバイダである華曦達(SDMC)が提供します。DRM暗号化証明書管理サービスの利用には料金が発生し、華曦達(SDMC)が請求します。具体的な接続や操作については、華曦達(SDMC)に直接お問い合わせください。

## 前提条件
- Tencent Cloud CSSサービスをアクティブ化し、[再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加済みであること。
- [華曦達SDMC DRMサービス](https://www.xmediacloud.com/contact-us/)でサービスアカウントを作成し、アクセスキーを設定していること。

## コンソールの設定
[](id:step1)
### DRMキー情報へのアクセス設定
1. CSSコンソールにログインし、**機能設定** >[DRM管理](https://console.cloud.tencent.com/live/config/drm)と進みます。
2. **編集**をクリックして華曦達(SDMC)DRMキー情報へのユーザーアクセスを設定します。UID、SecretID、SecretKeyを設定する必要があります。これらのキー情報は、証明書のサードパーティプロバイダから入手する必要があります。
![](https://qcloudimg.tencent-cloud.cn/raw/4a88319f757d161c4b86cbeef27cbf84.png)

[](id:step2)
### トランスコードテンプレートの設定とドメイン名のバインド
1. **機能設定** > [CSSトランスコード](https://console.cloud.tencent.com/live/config/transcode)と進みます。
2. **トランスコードテンプレートの作成**をクリックし、DRM暗号化情報を設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/048b9d46b1b5305605b2cd41a0a85b75.png)

<table>
<thead><tr><th width=18%>DRM暗号化設定項目</th><th>入力必須かどうか</th><th>説明</th></tr></thead>
<tbody><tr>
<td>DRM暗号化</td>
<td>いいえ</td>
<td>DRM暗号化スイッチは、デフォルトではオフです。この機能をオンにするには、DRM管理でDRMキーを設定する必要があります</td>
</tr><tr>
<td>暗号化タイプ</td>
<td>はい</td>
<td>Widevine、Fairplay、NomalAESをサポートしています。Fairplayを使用する場合は、プレーヤー側でAppleから申請された証明書をアップロードする必要があります。詳細については、<a href="https://intl.cloud.tencent.com/document/product/267/48069">Fairplay証明書の申請</a></td>をご参照ください
</tr>
</tbody></table>
3. **ドメイン名のバインド**をクリックすると、対応するトランスコードテンプレートが再生ドメイン名にバインドされます。
![](https://qcloudimg.tencent-cloud.cn/raw/96151a6cb6428abceca9e85a66728f99.png)

[](id:step3)
### DRM再生アドレスの取得
DRM暗号化には、再生アドレスがHLS再生プロトコルである必要があります。[アドレスジェネレーター](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)で、対応するトランスコードテンプレートを選択して再生アドレスを発行し、HLS再生プロトコルアドレスを選択してDRM再生アドレスにすることができます。

![](https://qcloudimg.tencent-cloud.cn/raw/823cbe64c7fb7fdcbd88f5b3742eacf5.png) 

[](id:step4)
### プレーヤーの設定
ライブストリーミングDRM暗号化機能を使用する場合、プレーヤーに一定の要件があります。
- プレーヤーと[華曦達(SDMC)](https://www.xmediacloud.com/contact-us/)を接続して、ビデオ情報からLicenseを取得、復号する機能を実装する必要があります。
- iOSプラットフォームはFairplayをサポートし、AndroidプラットフォームはWideVineとNomalAESをサポートしています。
- iOSプラットフォームの場合、証明書を申請し、[華曦達(SDMC)プラットフォーム](https://www.xmediacloud.com/contact-us/)にアップロードする必要があります。

>? DRMまたは華曦達への接続プロセスで発生したいかなる問題についても、[お問い合わせ](https://console.cloud.tencent.com/workorder/category)からチケットを提出することができます。すべての工程でお客様の問題解決をサポートします。
