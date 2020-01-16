## 操作シナリオ
このドキュメントは、コンソール、API、およびインスタンスメタデータでパブリックIPアドレスを取得する方法について説明します。


## 操作手順

###コンソールで取得する
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
2.インスタンス管理ページで、マウスをプライマリIPアドレス列に移動すると、<img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"></img>が以下に示すように表示されます。
![](https://main.qcloudimg.com/raw/7f184b52a3311b4d3cc45b810bbda04f.png)
3.  <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"></img>をクリックし、このIPアドレスをコピーします。	
>パブリックIPアドレスがNATを介してプライベートIPアドレスにマッピングされるため、インスタンス内部でネットワークインターフェースのプロパティを照会する場合(たとえば、 `ifconfig(Linux)`または `ipconfig(Windows)`コマンドを使用)、パブリックIPアドレスが表示されません。インスタンス内部でインスタンスのパブリックIPアドレスを確認する場合、[インスタンスメタデータで取得する](#jump)をご参照ください。
>

### APIで取得する
[インスタンスリストの照会](https://cloud.tencent.com/document/product/213/15728)にある関連インターフェースをご参照ください。

<span id = "jump">  </span>
### インスタンスメタデータで取得する
1. CVMのインスタンスにログインする。
ログイン方法の詳細については、[Linuxインスタンスのログイン](https://intl.cloud.tencent.com/document/product/213/5436)、および[Windowsインスタンスのログイン](https://intl.cloud.tencent.com/document/product/213/32498)をご参照ください。
2. cURLツールまたはHTTPのGETリクエストを介してmetadataにアクセスし、パブリックIPアドレスを取得します。
```
curl http://metadata.tencentyun.com/meta-data/public-ipv4
```
戻り値は次のような構造を持っている場合、パブリックIPアドレスを照会できます。
![](https://main.qcloudimg.com/raw/03f603e433b7a5da09e33a8b09d731b4.png)
詳細情報については、[インスタンスメタデータの照会](https://intl.cloud.tencent.com/document/product/213/4934)をご参照ください。
