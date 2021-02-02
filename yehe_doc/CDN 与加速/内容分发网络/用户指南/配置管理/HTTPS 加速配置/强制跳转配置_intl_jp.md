## 設定の概要

Tencent Cloud CDNサービスは、HTTPS/HTTP強制リダイレクトの設定をサポートしています。

- HTTPS Secure Acceleration が CDNドメイン名に対して有効になっている場合、301/302リダイレクト方式を指定して、CDNノードに到達するすべてのHTTPリクエストを強制的にHTTPSにリダイレクトさせることができます。
- また、301/302リダイレクト方式を指定して、CDNノードに到達するすべての HTTPSリクエストを強制的に HTTPにリダイレクトさせることができます。
- リダイレクト時はデフォルトで Response headerをつけません。変更可能です。

## 設定ガイド

### 制限について

HTTPS強制リダイレクトを設定するには、HTTPSアクセラレーションを有効にする必要があります。

### 設定方法

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のサイドバーで【ドメイン管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定画面に入ります。【HTTPS設定】タブをクリックし、【強制リダイレクト】セクションを見つけます。この機能はデフォルトで無効になっています。
<img src="https://main.qcloudimg.com/raw/ffbb3a57c19ba1d8a52b25ad66f16508.png" style="width:700px"/>
「リダイレクト設定」をオンに切り替えて、リダイレクトタイプ、リダイレクト方式を設定できます。
<img src="https://main.qcloudimg.com/raw/90aae9a0b02d704dfafd0c080e5972db.png" style="width:450px"/>
【OK】をクリックします。
<img src="https://main.qcloudimg.com/raw/bd1a62d0b49fb4f2e189512e30b8b9ff.png" style="width:700px"/>

