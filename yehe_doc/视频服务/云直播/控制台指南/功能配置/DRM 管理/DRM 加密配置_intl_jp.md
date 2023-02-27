Cloud Streaming Services (CSS)は、Widevine、Fairplay、NormalAESをベースにしたDRM暗号化プロトコルを使用し、ライブストリーミング暗号化、画面録画禁止、ホットリンク保護などのサービスを提供し、ユーザーのビデオコンテンツを全面的に保護します。本書では、コンソールでDRM暗号化機能を使用する手順を説明します。

## 注意事項
Tencent Cloudは、ビデオストリームに対する暗号化処理のみを提供します。DRM暗号化ベースの証明書管理は、サードパーティのSDMC社とDRMtoday社により提供された有料サービスです。詳しくは、SDMC社またはDRMtoday社までお問い合わせください。

##  前提条件
- Tencent CSSサービスが有効になっており、[再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)が追加されていること。
- [SDMC DRMサービス](https://console.multidrm.tv/setting/drm/index)または[DRMtoday](https://castlabs.com/free-trials/drmtoday/)にサービスアカウントを作成し、アクセスキーを設定していること。

## コンソールの設定
[](id:step1)

### DRMへのアクセスキーの設定
1. CSSコンソールにログインし、**機能設定** > [**DRM管理](https://console.cloud.tencent.com/live/config/drm)に進みます。
2. **編集**をクリックし、キーの情報を入力し、証明書管理サービスのプロバイダー（SDMCまたはDRMtoday）を選択します。詳細な設定は以下の通りです：
- 証明書管理サービスのプロバイダーが**SDMC**の場合
   - ユーザーがSDMCのDRMにアクセスする時に使用するキーの情報（UID、SecretID、SecretKey）を設定します。これらのキーの情報は、サードパーティから入手してください。
![](https://qcloudimg.tencent-cloud.cn/raw/09a9b34d85b87b89c43e5c5831530ee9.png)
- 証明書管理サービスのプロバイダーが**DRMtoday**の場合
   - ユーザーがDRMtodayのDRMにアクセスする時に使用するキーの情報（MerchantName、MerchantUUID、MerchantApiName、MerchantApiPassword、KeySeedID、IvSeedID）を設定します。これらのキーの情報は、サードパーティから入手してください。
![](https://qcloudimg.tencent-cloud.cn/raw/292500dccf57d708dca961985020cbc6.png)

[](id:step2)
### トランスコーディングテンプレートの設定とドメイン名のバインド
1. **機能設定** > [**CSSトランスコーディング**](https://console.cloud.tencent.com/live/config/transcode)に進みます。
2. **トランスコーディングテンプレートを作成**をクリックし、DRM暗号化情報を設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/048b9d46b1b5305605b2cd41a0a85b75.png)
<table>
<thead><tr><th width=18%>DRM暗号化設定項目</th><th>設定要否</th><th>についての説明</th></tr></thead>
<tbody><tr>
<td>DRM暗号化</td>
<td>不要</td>
<td>DRM暗号化の有効/無効。デフォルトでは無効です。有効にするには、DRM管理でDRMキーを設定しておく必要があります</td>
</tr><tr>
<td>暗号化タイプ</td>
<td>必要</td>
<td>Widevine、Fairplay、NomalAESをサポートします。Fairplayを使用するには、プレイヤー側からAppleに申請した証明書をアップロードする必要があります。詳しくは、<a href="https://www.tencentcloud.com/document/product/267/48069">Fairplay証明書の申請</a></td>をご参照ください
</tr>
<td>DRMタグ</td>
<td>必要</td>
<td>SD、HD、UHD1、UHD2を選択できます。</a></td>
</tr>
</tbody></table>

3. **ドメイン名をバインド**をクリックし、トランスコーディングテンプレートと再生ドメイン名をバインドします。
![](https://qcloudimg.tencent-cloud.cn/raw/96151a6cb6428abceca9e85a66728f99.png)

[](id:step3)
### DRM再生アドレスの取得
DRM暗号化を使用するには、再生アドレスはHLS再生プロトコルを使用する必要があります。[アドレスジェネレータ](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)で対応するトランスコーディングテンプレートを選択し、再生アドレスを生成して、HLS再生プロトコルを使用するアドレスをDRM再生アドレスとして使用してください。

![](https://qcloudimg.tencent-cloud.cn/raw/823cbe64c7fb7fdcbd88f5b3742eacf5.png) 

[](id:step4)
### プレーヤーの設定
ライブストリーミングDRM暗号化機能を使用する場合、プレイヤーは以下の要件を満たさなければなりません。
- プレイヤーは [SDMC](https://www.xmediacloud.com/contact-us/) と連携し、ビデオ情報を通しライセンスを取得して復号化する必要があります。
- iOSプラットフォームはFairplayをサポートし、AndroidプラットフォームはWideVineとNomalAESをサポートしています。
- iOSプラットフォームの場合、証明書を申請し[SDMCプラットフォーム](https://console.multidrm.tv/licenses/drm/index)にアップロードする必要があります。

>? SDMCプラットフォームを操作するには、登録してアカウントを取得する必要があります。登録方法については、[ユーザーキーの取得](https://www.tencentcloud.com/document/product/267/48070)をご参照ください。DRMまたはサードパーティプロバイダーとのやり取りで問題が発生した場合、いつでも[お問い合わせ](https://console.cloud.tencent.com/workorder/category)までご連絡ください。責任をもって協力させていただきます。
