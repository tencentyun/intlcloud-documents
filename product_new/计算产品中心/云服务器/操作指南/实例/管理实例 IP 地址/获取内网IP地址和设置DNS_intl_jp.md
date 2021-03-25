このドキュメントは、インスタンスのプライベートIPアドレスを取得し、プライベートネットワークDNSを設定する方法について説明します。

## インスタンスのプライベートIPアドレスを取得する
### コンソールで取得する
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/)にログインします。
2. 下図に示すように、インスタンスの管理ページで、確認するプライベートIPのインスタンスを選択し、マウスを「プライマリIPアドレス」列に移動し、<img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;">をクリックして、プライベートIPをコピーします。

### APIで取得する
[DescribeInstances インターフェース](https://intl.cloud.tencent.com/document/product/213/33258)をご参照ください。

### インスタンスのメタデータで取得する

1. CVMにログインします。
2. cURLツールまたはHTTPのGETリクエストを介して、インスタンスのメタデータにアクセスします。
>次の操作では、cURLツールを例として使用します。
>
次のコマンドを実行し、プライベートIPを取得します。
```
curl http://metadata.tencentyun.com/meta-data/local-ipv4
```
返された情報はプライベートIPアドレスです、

インスタンスメタデータの詳細情報については、[インスタンスメタデータの照会](https://intl.cloud.tencent.com/document/product/213/4934)をご参照ください。

## プライベートネットワークDNSを設定する 
ネットワーク解析にエラーが発生した場合、CVMのOSの種類に応じてプライベートネットワークDNSを手動で設定できます。

### Linuxシステム

1. Linux CVMにログインします。
2.次のコマンドを実行して、 `/etc/resolv.conf`ファイルを開きます。
```
vi /etc/resolv.conf
```
3. ** i **または** Insert **を押して編集モードに切り替え、[プライベートネットワークDNS](https://intl.cloud.tencent.com/document/product/213/5225)リストにある対応する各リージョンをもとに、DNS IPを変更します。
たとえば、プライベートネットワークDNS IPを北京リージョンのプライベートネットワークDNSサーバーに変更します。
```
nameserver 10.53.216.182
nameserver 10.53.216.198
options timeout:1 rotate
```
4. ** Esc **を押して**：wq **を入力し、ファイルを保存して戻ります。

### Windows システム

1.  Windows CVMにログインします。
2.OS画面で、【コントロールパネル】>【ネットワークと共有センター】> 【アダプターデバイスの変更】を開きます。
3. 【イーサネット】を右クリックして、【プロパティ】を選択し、「イーサネットのプロパティ」ウィンドウを開きます。
4. 「イーサネットのプロパティ」ウィンドウで、【Internetプロトコルバージョン4(TCP / IPv4)】をダブルクリックして開きます。
5. 【次のDNSサーバーアドレスを使用する】を選択して、[プライベートネットワークDNS](https://intl.cloud.tencent.com/document/product/213/5225)リストにある対応する各リージョンをもとに、DNS IPを変更します。
6. 【OK】をクリックします。
