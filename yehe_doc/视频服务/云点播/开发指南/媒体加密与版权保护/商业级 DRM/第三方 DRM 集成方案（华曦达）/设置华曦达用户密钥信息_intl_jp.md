サードパーティのDRMキープロバイダ（華曦達SDMC）を使用してDRM機能を統合する場合、華曦達から関連のユーザーキー情報（ユーザーID、SecretID、SecretKey、FairPlay証明書アドレス）を取得する必要があります。そこでここでは、華曦達コンソールからユーザーキー情報を取得する方法を中心にご説明します。

## 操作手順
1. 華曦達のアカウントをお持ちでない場合、登録を行えば、[華曦達(SDMC)公式サイト](https://www.xmediacloud.com/contact-us/)にアクセスできます。
    ![](https://qcloudimg.tencent-cloud.cn/raw/e92825b46f81fce995a115c0905915cb.png)

2. 右側のフォームに必要事項を入力した後、**Send message**をクリックします。通常は数時間すると華曦達のシステムからメールが届き、その後、華曦達の営業スタッフから連絡が入り、関連情報の確認を行います。
    ![](https://qcloudimg.tencent-cloud.cn/raw/73ca49235b99ef7c42c97514a46f47c8.png)

3. 華曦達の審査で承認されると、DRMサービスアクティブ化メールが送られてきます。メールには、華曦達DRMコンソールアドレスおよび初期パスワードが記載されています。

4. [華曦達DRMコンソール](https://sso.multidrm.tv/login)にログインし、アカウントとパスワードを入力すればログイン成功です。
    ![](https://qcloudimg.tencent-cloud.cn/raw/1833a48650c8ba607ad57701839b6d33.png)

5. コンソールに進んで、左側ナビゲーションバーの**DRM SETTING**をクリックし、ユーザーキー情報のユーザーID、SecretID、SecretKeyを照会します。
    ![](https://qcloudimg.tencent-cloud.cn/raw/59b1edb28e121521e9806b0d062b7495.png)

6. Fairplay証明書アドレスを照会して取得します。

    ![](https://qcloudimg.tencent-cloud.cn/raw/81407e990466afe606bba4c378f66fe6.png)

7. Tencent Cloud VODコンソールにログインします。

8. 華曦達のユーザーキー情報（ユーザーID、SecretID、SecretKey、FairPlay証明書アドレスを含む）を提出します。

    （フロントエンドが完了後に追加されるステップ）

## まとめ

  この時点で、Tencent Cloud VODコンソールでのユーザーキー情報の設定が完了しました。
>? DRMまたは華曦達への接続プロセスで発生したいかなる問題についても、[お問い合わせ](https://console.cloud.tencent.com/workorder/category)からチケットを提出することができます。すべての工程でお客様の問題解決をサポートします。
