ドメイン名に既存の証明書を設定する場合は、先に次の内容をご参照ください。Tencent Cloud SSL証明書管理からの証明書を設定する場合は、この手順をスキップできます。
## 証明書をアップロードする
CA機構によって提供の証明書は一般的に以下の種類があります。CDNサービスは**Nginx**を使っています。
![](https://main.qcloudimg.com/raw/249538db51d90314f84b2c75a6bccc05.png)
Nginxフォルダーに入り、テキストエディターで「.crt」（証明書）ファイルと 「.key」（プライベートキー）ファイルを開くと、PEMフォーマットの証明書内容及びプライベート内容を確認できます。
![](https://main.qcloudimg.com/raw/2a1b11ff93a7cb475d68e38c7701434f/Nginx_certificate.png)

### 証明書
証明書の拡張子は一般的に「.pem」、「.crt」または「.cer」です。テキストエディターで証明書ファイルを開くと、以下に示すような内容が表示されます。
証明書PEMフォーマット：「-----BEGIN CERTIFICATE-----」で始まり、「-----END CERTIFICATE-----」で終わります。その間の内容は1行あたり64文字であり、最後の行の長さが64文字未満にすることができます。
![img](https://main.qcloudimg.com/raw/60ea02d1a2c9623526d7fa79403e658a.jpg)
証明書が中間CA機関によって発行された場合、証明書ファイルは複数の証明書で構成されます。サーバー証明書と中間証明書を手動でスプライスしてアップロードする必要があります。スプライスのルールとして、サーバー証明書は1部目に、中間証明書は2部目に、サーバー証明書のコンテンツを中間証明書のコンテンツの前に空白行を入れずに配置して、一般的には、機構が証明書を発行する時に、対応する説明がありますので、ルールの説明をよく確認してください。

>
> + 証明書間に空行があってはなりません
> + 証明書はすべてPEMフォーマットです

中間CAにより発行する証明書チェーンのフォーマットは下記の通りです。
```
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
```

### プライベートキー
プライベートキーの拡張子は一般的に「.pem」または「.key」です。テキストエディターでプライベートキーファイルを開くと、以下に示すような内容が表示されます。
プライベートキー PEM フォーマット：「-----BEGIN RSA PRIVATE KEY-----」で始まり、「-----END RSA PRIVATE KEY-----」で終わります。その間の内容は1行あたり64文字であり、最後の行の長さが64文字未満することができます。
![img](https://main.qcloudimg.com/raw/e10009916aeb00d5158a3703115d0354.jpg)
取得したプライベートキーが「-----BEGIN PRIVATE KEY-----」で始まり、「-----END PRIVATE KEY-----」で終わる場合は、opensslツールで形式を変換することをお勧めします。コマンドは下記の通りです。
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

### 他の形式をPEM形式に変換する
現在、CDNはPEM形式の証明書をしか対応していません。ほかの形式の証明書はPEM形式に変換する必要があります。opensslツールで変換を行うことをお勧めします。以下は、証明書形式をPEM形式に変換するためによく使われている方法です。
### DERをPEMに変換する
DER形式は通常、Javaプラットフォームで使用されます。
証明書の変換：
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
プライベートキーの変換：
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```
### P7BをPEMに変換する
P7B形式は通常、Windows ServerおよびTomcatで使用されます。
証明書の変換：
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
テキストエディターでoutcertificat.cerを開くと、PEM形式の証明書内容を確認できます。
プライベートキーの変換：プライベートキーは一般的に IISサーバーにエクスポートすることが可能です。
#### PFXをPEMに変換する
PFX形式は通常、Windows Serverで使用されます。
証明書の変換：
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
プライベートキーの変換：
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```
### 証明書チェーンの補完
プライベート証明書を設定する場合、下図に示すように、**証明書チェーンが補完できない**場合があります。
![img](https://main.qcloudimg.com/raw/ed45f581114cc456a710b7d4997076a2.png)
この場合、CAが発行した証明書（PEM形式）の内容をドメイン名証明書（PEM フォーマット）の末尾に貼り付けることにより、証明書チェーンを補完することができます。またチケットを提出してください。
![img](https://main.qcloudimg.com/raw/c5adc7371454ec06a7f2f8150ec48ed8/cer11.png)

## ホスト証明書

Tencent Cloudは、証明書ホスティングサービス、つまり[SSL証明書](http://console.cloud.tencent.com/ssl)を提供します。既存の証明書をSSL証明書管理プラットフォームにアップロードしてホスティングを行い、他のクラウド製品に展開できます。 また、証明書を購入して申請することもできます。

Tencent Cloud SSL証明書サービスは、各ユーザーにTrustAsiaが無料で発行した20のDV SSL証明書を提供します。
