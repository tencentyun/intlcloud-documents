StreamLive DRM暗号化はユーザーカスタムキー（CustomDRMKeys）およびSDMCDRMをサポートしています。設定エントリーは**Channel Management**にあります。設定したいChannelに対して**Edit**を行い、**Output Group Setting**の**DRM**に進んでモジュールを設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/95418fc6d0cf376df994b1d0423d3d0d.png)

>? 現在、HLSクラスはFairplayに、DASHクラスはWidevineに固定されています。


## CustomDRMKeys
### 1. Fairplay
![](https://qcloudimg.tencent-cloud.cn/raw/8cf25c1d7543cd338a45a6cb9979fc12.png)
- **Cid**：Fairplayの暗号化Content Idです。ご使用のDRMシステムで不要な場合は、代わりに固有のIDを入力することができます。
- **Key**：Fairplayの暗号化Keyです。
- **Iv**：Fairplayの暗号化Ivです。

### 2. Widevine
WidevineはAUDIO、SD、HD、UHD1、UHD2という5タイプのTrackをサポートしています。各TrackにはそれぞれKeyIdとKeyを単独で設定できます。ご使用のDRMシステムがTrackのタイプごとにキーを提供していないか、または同一のキーを使用している場合は、All Track統一設定を使用できます。
![](https://qcloudimg.tencent-cloud.cn/raw/177f7f0dbdefb1d89301b743680c54d8.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0e7ac02908541f47db2c7ccf6f2cf8ad.png)


## SDMCDRM
![](https://qcloudimg.tencent-cloud.cn/raw/ef29af2c0bf02295069e35ef7f9aca0c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/385e2c9d4c16f8c4c3d594b18cb58e8c.png)

- **Cid**：SDMC DRMが提供するContent Id（オプション）です。入力しない場合は代わりにChannel Idを使用します。
- **Uid**：SDMC DRMが提供するUid（ユーザーID）です。
- **Secret id**：SDMC DRMが提供するSecret Idです。
- **Secret key**：SDMC DRMが提供するSecret keyです。
- **Url**：SDMC DRMキーを取得するアドレスであり、SDMC DRMから提供されます。
- **Tokenname**：SDMC DRMキーのアドレスをリクエストする際のToken名（オプション）であり、SDMC DRMから提供されます。入力しない場合はデフォルトで'token'を使用します。
