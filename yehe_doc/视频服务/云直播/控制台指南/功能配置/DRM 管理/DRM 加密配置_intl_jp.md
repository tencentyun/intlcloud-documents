Cloud Streaming Services (CSS)は、Widevine、Fairplay、NormalAESをベースにしたDRM暗号化プロトコルを使用し、ライブストリーミング暗号化、 画面録画禁止、ホットリンク保護などのサービスを提供し、ユーザーのビデオコンテンツを全面的に保障します。本書では、コンソールでDRM暗号化機能を使用する手順を説明します。

## 注意事項
Tencent Cloudは、ビデオストリームに対する暗号化処理だけを提供します。DRM暗号化ベースの証明書管理は、サードパーティのSDMC社により提供された有料サービスです。詳しくは、SDMC社までお問い合わせください。

##  前提条件
- Tencent CSSサービスが有効になっており、[再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)が追加されていること。
- [SDMC DRMサービス](https://www.xmediacloud.com/contact-us/)にサービスアカウントが作成され、アクセスキーが設定されています。

## コンソールの設定
[](id:step1)

### DRMへのアクセスキーの設定
1. CSSコンソールにログインし、**機能設定** > [**DRM管理**](https://console.cloud.tencent.com/live/config/drm)に進みます。
2. **編集**をクリックし、ユーザーがSDMCのDRMにアクセスするときに使用するキーの情報（UID、SecretID、SecretKey）を設定します。これらのキーの情報は、サードパーティから入手してください。
![](https://qcloudimg.tencent-cloud.cn/raw/4a88319f757d161c4b86cbeef27cbf84.png)

[](id:step2)
### トランスコーディングテンプレートの設定とドメイン名のバインド
1. **機能設定** > [**CSSトランスコーディング**](https://console.cloud.tencent.com/live/config/transcode)に進みます。
2. **トランスコーディングテンプレートを作成**をクリックし、DRM暗号化情報を設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/048b9d46b1b5305605b2cd41a0a85b75.png)

<table>
<thead><tr><th width=18%>DRM暗号化設定項目</th><th>設定要否</th><th>についての説明</th></tr></thead>
<tbody><tr>
<td>DRM暗号化</td>
<td>いいえ</td>
<td>DRM暗号化の有効/無効。デフォルトでは無効です。有効にするには、DRM管理でDRMキーを設定してください</td>
</tr><tr>
<td>暗号化タイプ</td>
<td>はい</td>
<td>Widevine、Fairplay、NomalAESをサポートします。Fairplayを使用するには、プレイヤー側からAppleに申請した証明書をアップロードしてください。詳しくは、 <a href="https://intl.cloud.tencent.com/document/product/267/48069">Fairplay証明書の申請</a>をご参照ください</td>
</tr>
</tbody></table>

3. **ドメイン名をバインド**をクリックし、トランスコーディングテンプレートと再生ドメイン名をバインドします。
![](https://qcloudimg.tencent-cloud.cn/raw/96151a6cb6428abceca9e85a66728f99.png)

[](id:step3)
### DRM再生アドレスの取得
DRM暗号化を使用するには、再生アドレスはHLS再生プロトコルを使用してください。[アドレスジェネレータ](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)で対応するトランスコーディングテンプレートを選択し、再生アドレスを生成して、HLS再生プロトコルを使用するアドレスをDRM再生アドレスとして使用してください。

![](https://qcloudimg.tencent-cloud.cn/raw/823cbe64c7fb7fdcbd88f5b3742eacf5.png) 

[](id:step4)
### プレーヤーの設定
ライブストリーミングDRM暗号化機能を使用する場合、プレイヤーは以下の要件を満たさなければなりません：
- プレイヤーは [SDMC](https://www.xmediacloud.com/contact-us/) と連携し、ビデオ情報を通しライセンスを取得して復号化する必要があります。
- iOSではFairplay、AndroidではWideVineとNomalAESがサポートされています。
- iOSでは、証明書を申請して[SDMCプラットフォーム](https://www.xmediacloud.com/contact-us/)にアップロードしてください。
