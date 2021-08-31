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
<img src="https://main.qcloudimg.com/raw/b11157d848d39d4e4bba540598f35eba.png" style="width:700px"/>
「リダイレクト設定」をオンに切り替えて、リダイレクトタイプ、リダイレクト方式を設定できます。
<img src="https://main.qcloudimg.com/raw/731d7bcb51286683d259691178bf2b39.png" style="width:450px"/>
【OK】をクリックします。
<img src="https://main.qcloudimg.com/raw/2dcfbacf16b47fe600935f57aadd2e77.png" style="width:700px"/>

