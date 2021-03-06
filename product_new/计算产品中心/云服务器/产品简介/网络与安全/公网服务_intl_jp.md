ユーザーはCVMインスタンスでデプロイしたアプリケーションが公共サービスとして提供する必要がある場合、Internetに介してデータを転送し、InternetでのIPアドレス（パブリックIPアドレスとも呼ばれる）が必要です。Tencent CloudのInternetアクセスはTencent Cloudデータセンターの高速インターネットに介して提供します。中国国内のマルチ回線BGPネットワークは20以上のネットワークキャリアをカバーし、BGPパブリックネットワークIPは秒レベルで複数のリージョンを切り替えできます。ユーザーがどのネットワークを使用しても、高速で安全なネットワークを享受できます。

## パブリックIPアドレス
 - **概要：**パブリックIP アドレスはInternet上で保持しないアドレスです。パブリックIPアドレスをもつCVMはインターネットの他のコンピューターと相互にアクセスできます。
 - **獲得：**CVMを作成する時、ネットワークで帯域幅を0Mbpsより大きく設定します。設定完了後、Tencent Cloudシステムは自動的にパブリックIPアドレスプールからIPを取得してインスタンスにアサインします、このアドレスは変更することができます。詳細操作は[パブリックネットワークIPの置き換え](https://intl.cloud.tencent.com/document/product/213/16642)をご参照ください。
 - **設定：**InternetでパブリックネットワークIPアドレスをもつCVMインスタンスにログインして、関連設定を行います。CVMインスタンスのログイン詳細情報について、[Linux インスタンスのログイン](https://intl.cloud.tencent.com/document/product/213/5436)と[Windows インスタンスのログイン](https://intl.cloud.tencent.com/document/product/213/5435)をご参照ください 。
 - **変換：**パブリックIP アドレスはネットワークアドレス変換( NAT )を通して、インスタンスの[プライベートIP アドレス](https://intl.cloud.tencent.com/document/product/213/5225)にマッピングされます。
 - **メンテナンス：**Tencent CloudのすべてのパブリックネットワークインターフェースはTencent Gateway(TGW)に処理されます。Tencent Cloud CVMインスタンスのパブリックネットワークENIは統合インターフェイスレイヤーTGWで構成されているため、CVMが感知無しです。ユーザーがCVMで`ifconfig (Linux)` また `ipconfig (Windows)`コマンドを使用して、ネットワークインターフェースの情報を確認する時、[プライベートネットワーク](https://intl.cloud.tencent.com/document/product/213/5225)の情報のみ確認できます。パブリックネットワーク情報はユーザー自ら[CVM コンソール](https://console.cloud.tencent.com/cvm) にログインしてCVMのリスト/詳細画面で確認します。
 - **費用：**インスタンスがパブリックIP アドレスによってサービスを提供する時、関連する費用を支払い必要があります。詳細については、[ネットワーク帯域幅の購入](https://intl.cloud.tencent.com/document/product/213/10578) をご参照ください。

## パブリックIPアドレスをリリースする
ユーザーがインスタンスと関連するパブリックIP アドレスを主動にアソシエイト・リリースすることができません。
以下のような状況が発生した場合、パブリックIP アドレスはリリースされ、また再アサインされます：
- **インスタンスを廃棄する時 **ユーザーが自主的に従量課金タイプのインスタンスを廃棄する時、Tencent Cloudは該当パブリックIP アドレスをリリースします。
- **[ElasticパブリックIP アドレス](https://cloud.tencent.com/document/product/213/5733)はインスタンスと関連付け・関連付けを解除する時。**インスタンスはElasticパブリックIP アドレスに関連付けられると、Tencent Cloudはこのインスタンスの元のパブリックIPアドレスをリリースします。インスタンスとElastic IP アドレスの関連付けを解除する時、インスタンスが新しいパブリックIPアドレスにアサインされ、リリースされた元のパブリックIPアドレスはパブリックIPアドレスプールに戻されて、再利用することができません。

固定の永続なパブリックIPアドレスが必要な場合、[ElasticパブリックIP アドレス](https://cloud.tencent.com/document/product/213/5733)を使用できます。

## 操作ガイド
パブリックIPアドレスの獲得・置き換えなどの操作を実行できます、詳細な手順については、以下をご参照ください。
- [インスタンスパブリックIPアドレスの獲得](https://intl.cloud.tencent.com/document/product/213/17940)
- [インスタンスパブリックIPアドレスの置き換え](https://intl.cloud.tencent.com/document/product/213/16642)
