DRM暗号化証明書管理機能は、サードパーティプロバイダーのSDMC社とDRMtoday社により提供されます。SDMC社とDRMtoday社の証明書管理プラットフォームにアクセスするには、ユーザーキーの情報を提供する必要があります。本書では、SDMC社とDRMtoday社の証明書管理プラットフォームでユーザーキーの情報を取得する方法を説明します。

## SDMC
### 操作手順
1. [SDMC DRMサービス](https://www.xmediacloud.com/contact-us/)にアクセスして登録を行います。
![](https://qcloudimg.tencent-cloud.cn/raw/e92825b46f81fce995a115c0905915cb.png)
2. 必要に応じて入力を完了した後、**send message**をクリックし、SDMCの返事を待ちます。メッセージの送信に成功し一定時間（数時間）が経過すると、SDMCのシステムメールが送信されます。その後、SDMCの営業担当者から連絡があります。必要事項を確認した後、ログイン関連のメールが送信されます。
![](https://qcloudimg.tencent-cloud.cn/raw/73ca49235b99ef7c42c97514a46f47c8.png)
3. SDMCに承認されると、SDMC DRMコンソールのアドレスとログイン用初期パスワードが含まれたメールが送信されます。
4. [SDMC DRMコンソール](https://sso.multidrm.tv/login)にアカウントとパスワードを入力してログインします。
![](https://qcloudimg.tencent-cloud.cn/raw/1833a48650c8ba607ad57701839b6d33.png)
5. コンソールに進んで**DRM SETTING**をクリックし、ユーザーキーの情報であるユーザーID、SecretID、SecretKeyを取得します。
![](https://qcloudimg.tencent-cloud.cn/raw/59b1edb28e121521e9806b0d062b7495.png)
6. Access SecretのユーザーIDとパスワードを取得し、CSSの[DRM管理](https://console.cloud.tencent.com/live/config/drm)に入力します。
![](https://qcloudimg.tencent-cloud.cn/raw/8b1e5a5214c518aa387157921cd9acf6.png)

## DRMtoday
### 操作手順
1. [DRMtoday](https://castlabs.com/free-trials/drmtoday/)にアクセスして登録を行います。
![](https://qcloudimg.tencent-cloud.cn/raw/e775679d700c980bf41e998af8d7fb25.png)
2. 必要に応じて入力を完了した後、**send**をクリックし、drmtodayの返事を待ちます。メッセージの送信に成功し一定時間（数時間）が経過すると、drmtodayのシステムメールが送信されます。その後、ログイン関連のメールが送信されます。
![](https://qcloudimg.tencent-cloud.cn/raw/dd40958e4ac33287ca764587cecdbe0a.png)
3. DRMtodayに承認されると、DRMtodayのログインアドレスと初期パスワードが含まれたメールが送信されます。
![](https://qcloudimg.tencent-cloud.cn/raw/6392ffb43cf33a2180aed06a3a8c51fa.png)
4. [DRMtoday](https://login.castlabs.com/login?response_type=code&client_id=1fc7irb6c3cumm1004dpv8fbs1&scope=openid%20profile%20email&state=bvqz7MJ1DQ4A-X_dzYZDflN3BT_O_jRF6OFxpL3fnvE%3D&redirect_uri=https://fe.staging.drmtoday.com/login/oauth2/code/&nonce=gVEoLbgH7RDiR-EXX6PiAvEgqx3UIg8fCBfDniiHZAY)にアカウントとパスワードを入力してログインします。
![](https://qcloudimg.tencent-cloud.cn/raw/d5355f8f48e0f6056b89cdc0cb2ab108.png)
5. drmtoday管理画面に入ります。
![](https://qcloudimg.tencent-cloud.cn/raw/e6da9e6ff0b15e423f77ede1fbf69879.png)
6. API画面に入って、マーチャントの名前とuuidを取得します。(merchantName\merchantUUID)
![](https://qcloudimg.tencent-cloud.cn/raw/e79ec6a6287cb6ae4ae646e312a88209.png)
7. Users画面に入って、新しいAPIアカウントを作成し、APIアカウントと権限を与えて、パスワードをメモします。
>! パスワードは1回だけ表示されますので、メモしておいてください。APIアカウントとパスワードを取得します。(merchantAPIname/merchantAPIpassword)

![](https://qcloudimg.tencent-cloud.cn/raw/48d71df6591557ff51d8dc911c9d60bf.png)
APIアカウントの新規作成を有効にします。
![](https://qcloudimg.tencent-cloud.cn/raw/d59f5b5cbbaff1fcca550c6962ddaff8.png)
8. Configuration中のIngest settings暗号化キー取得設定のサブ画面に入ります。keyとivを生成するためのkey seedを新規作成します。(keySeedID/ivSeedID)
>? key seedを使用してキーを作成します。これは繰り返し確認できます。DRM暗号化メーカーとのやり取りに使用できます。(簡単なHMAC SHA512：key seedとkeyIdを使用しHMAC SHA512を作成し、暗号化文字列の上位16桁をkeyまたはivとして生成します)。

![](https://qcloudimg.tencent-cloud.cn/raw/5fa20f0cd056e6e91cb8b4df7548ca5c.png)
9.ユーザーの merchantName、merchantUUID、merchantAPIname、merchantAPIpassword、keySeedID、ivSeedIDを取得した後、ユーザー情報をCSSの[DRM管理]に入力します。
![](https://qcloudimg.tencent-cloud.cn/raw/e648c01c8f7892252932ef8a7a6024c4.png)

>? DRM、SDMC、DRMtodayとのやり取りで問題が発生した場合、いつでも[お問い合わせ](https://console.cloud.tencent.com/workorder/category)まで連絡してください。責任をもって協力させていただきます。