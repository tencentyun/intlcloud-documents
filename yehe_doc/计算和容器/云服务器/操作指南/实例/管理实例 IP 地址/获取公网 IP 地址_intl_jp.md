## 概要
このドキュメントは、コンソール、API、およびインスタンスメタデータでパブリックIPアドレスを取得する方法について説明します。

## 操作手順
<dx-tabs>
::: コンソールを利用した取得
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
  - **リストビュー**：下図のように、マウスをプライマリ IPアドレス列に移動し、<img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"/>をクリックすれば、このIPアドレスをコピーできます。
![](https://qcloudimg.tencent-cloud.cn/raw/de3e24445d11fca4fc194dd51462c406.png)
  - **タブビュー**：下図のように、インスタンスページで、「IPアドレス」のパブリックネットワークアドレス後の<img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"/> をクリックすれば、パブリックIPをコピーできます。
![](https://qcloudimg.tencent-cloud.cn/raw/1a719829bf4f09d9f4785a97f66abfd0.png)

<dx-alert infotype="notice" title="">
パブリックIPアドレスは、NATを介してプライベートIPアドレスにマッピングされるため、インスタンス内部でネットワークインターフェースのプロパティを（`ifconfig (Linux)` または `ipconfig (Windows)`コマンドを介して）確認しても、パブリックIPアドレスは表示されません。インスタンス内部からインスタンスのパブリックIPアドレスを確認したい場合は、[インスタンスメタデータを利用した取得](#jump)をご参照ください。
</dx-alert>


:::
::: \sAPI\sを利用した取得
詳細については、[DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258)をご参照ください。
:::
::: インスタンスメタデータを利用した取得[](id:jump)
1. CVMインスタンスにログインします。
具体的なログイン方法については、標準ログイン方法を使用した[Linuxインスタンスへのログイン](https://intl.cloud.tencent.com/zh/document/product/213/5436)および標準ログイン方法を使用した[Windowsインスタンスへのログイン](https://intl.cloud.tencent.com/document/product/213/41018)をご参照ください。
2. cURLツールまたはHTTPのGETリクエストを介してmetadataにアクセスし、パブリックIPアドレスを取得します。
```
curl http://metadata.tencentyun.com/meta-data/public-ipv4
``` 戻り値に次のような構造がある場合は、パブリックIPアドレスを確認できます。
![](https://main.qcloudimg.com/raw/03f603e433b7a5da09e33a8b09d731b4.png)
詳細については、[インスタンスメタデータの確認](https://www.tencentcloud.com/document/product/213/4934)をご参照ください。
:::
</dx-tabs>
