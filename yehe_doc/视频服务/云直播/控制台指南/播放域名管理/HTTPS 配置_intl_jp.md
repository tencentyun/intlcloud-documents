## 操作シナリオ
HTTPSプロトコルはSSL+HTTPプロトコルで構築された暗号化送信とID認証が実行できるネットワークプロトコルであり、HTTPプロトコルに比べ安全です。HTTPSアクセラレーションを有効にする必要がある場合は、再生ドメイン名のHTTPS機能を有効にし、正確かつ有効な証明書を設定することによって実現できます。Tencent Cloud[SSL証明書](https://intl.cloud.tencent.com/product/ssl) で対応する証明書を購入することができます。HTTPS証明書をすでにお持ちの場合は、LVBコンソールにアップロードして設定することができます。ライブストリーミングは、現在、PEM形式のみをサポートしており、証明書が他の形式の場合は、PEM形式に変換する必要があります。証明書の形式要件と設定方法は次のとおりです。

## 前提条件
- [LVBコンソール](https://console.cloud.tencent.com/live)にログイン済みであること。
- [再生ドメイン名を追加](https://intl.cloud.tencent.com/document/product/267/35970)済みであること。


## 操作手順 
### 手順1: HTTPS設定の編集
1. [【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)に進み、設定の必要がある**再生ドメイン名**または右側の【管理】をクリックしてドメイン名詳細ページに進みます。
2. 【高度な設定】を選択し、【HTTPS設定】のタブを表示します。
3. 【編集】をクリックしてHTTPS設定ページに移動し、![](https://main.qcloudimg.com/raw/897761946b06e8f904bfa6301d282817.png)ボタンをクリックしてHTTPSサービスの有効化を選択します。
4. 証明書ソースを選択し、設定する証明書ソースを選択して、関連情報を入力し、【保存】をクリックします。
<table>
<tr><th>証明書タイプ</th><th>入力事項</th></tr>
<tr>
<td>自身の証明書</td>
<td><ul style="margin:0">
<li>証明書名：証明書を識別し易くするために、カスタマイズできます。</li>
<li>証明書の内容： Nginxファイル中の<code>.crt</code> ファイルの内容を入力します。詳細については<a href="#content">証明書の内容</a>をご参照ください。</li>
<li>秘密鍵の内容： Nginx ファイル中の<code>.key</code> ファイルの内容を入力します。詳細については<a href="#private_key">証明書の暗号鍵</a>をご参照ください。</li><ul></td>
</tr><tr>
<td>Tencent Cloudホスト証明書</td>
<td>証明書リスト：Tencent Cloud <a href="https://console.cloud.tencent.com/ssl">SSL証明書サービス</a>でアップロード済みの証明書を選択します。</td>
</tr></table>
<img src="https://main.qcloudimg.com/raw/023725d33c3fdc4e06a4a4eb1791a578.png"></img>

#### 証明書の説明：
[CA](https://intl.cloud.tencent.com/document/product/1007/30192) が提供する証明書には、Apache、IIS、NginxおよびTomcatがあります。**LVBの暗号化サービスではNginxを使用するため、設定ではNginxファイル中の内容を選択する必要があります**。 
【SSL証明書コンソール】>【[証明書管理](https://console.cloud.tencent.com/ssl)】に移動し、表示したい証明書を選択し、操作バーの【ダウンロード】をクリックして、解凍すると、次のファイルを取得できます。
  ![](https://main.qcloudimg.com/raw/f67e31bfa2c233cf8dc0c4a1e58cb6fc.png)
- <b id="content">証明書の内容</b>： Nginx中の`.crt` ファイルを選択し、入力ボックスに`-----BEGIN CERTIFICATE-----` と `-----END CERTIFICATE-----` を含むすべての内容を入力します。
**内容例：**
![](https://main.qcloudimg.com/raw/e6c61fda3637a2f11e56cec30f0f7bd3.png)
>?証明書が中間機関によって発行され、かつ複数の証明書が含まれる場合は、証明書の内容を次の形式で結合してください。
> -----BEGIN CERTIFICATE-----
> -----END CERTIFICATE-----
> -----BEGIN CERTIFICATE-----
> -----END CERTIFICATE-----
- <b id="private_key">証明書の秘密鍵</b>： Nginx中の`.key` ファイルを選択し、入力ボックスに` -----BEGIN RSA PRIVATE KEY----- `と `-----END RSA PRIVATE KEY----- `を含むすべての内容を入力します。
**内容例：**
![](https://main.qcloudimg.com/raw/1ca20b0021b49ccb407df43675be37ba.png)

### 手順2：認証の設定
HTTPS設定は約2時間後に有効になります。証明書の送信から約2時間後にこのドメイン名にアクセスしてください。ブラウザアドレスバーにHTTPSが表示されれば、設定が成功したことを意味します。
![](https://main.qcloudimg.com/raw/b1f54ec35855e5d2adbaeae96a04ef13.png)

### 手順3：設定の変更
HTTPS機能は有効化と無効化をサポートしています。このサービスを無効にすると、LVBはこのドメイン名にHTTPSサービスを提供しなくなります。証明書の期限が切れている場合は、新しい有効な証明書に更新する必要があります。


## よくあるご質問
- [ライブストリーミングHTTPS設定にはどのような形式の証明書を入力しなければなりませんか。](https://intl.cloud.tencent.com/document/product/267/32478)
- [どうやって証明書がPEM形式か、それともDER形式かを判別しますか。](https://intl.cloud.tencent.com/document/product/267/32478)







