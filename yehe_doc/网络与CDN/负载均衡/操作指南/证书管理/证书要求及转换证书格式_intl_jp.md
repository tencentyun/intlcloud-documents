ここではSSL証明書の要件および証明書形式の変換についてご説明します。

## 一般的な証明書申請のフロー
1. OpenSSLツールを使用して、ローカルで秘密鍵ファイルを生成します。その中の`privateKey.pem`が秘密鍵ファイルですので、適切に保管してください。
```
openssl genrsa -out privateKey.pem 2048
```
2. OpenSSLツールを使用して、証明書リクエストファイルを生成します。その中の`server.csr`が証明書リクエストファイルです。証明書の申請に使用できます。
```
openssl req -new -key privateKey.pem -out server.csr
```
3. 証明書リクエストファイルの内容を取得し、CAなどの機関のサイトに送信して証明書の申請を行います。

## 証明書形式の要件
- ユーザーが申請する必要がある証明書は、Linux環境のPEM形式の証明書です。CLBは他の形式の証明書をサポートしていません。その他の形式の証明書の場合は、下記の[証明書のPEM形式への変換の説明](#PEM)の内容をご参照ください。
- root CA機関によって発行された証明書の場合は、取得した証明書が唯一のものであり、追加の証明書は必要ありません。これを設定したサイトは、ブラウザなどのアクセスデバイスによって信頼できるとみなされます。
- 中間CA機関によって発行された証明書の場合は、取得した証明書ファイルに複数の証明書が含まれるため、サーバー証明書と中間証明書を手動で合わせてアップロードする必要があります。
- 証明書に証明書チェーンがある場合は、証明書チェーンの内容をPEM形式の内容に変換し、証明書の内容と合わせてアップロードしてください。
- 結合ルール：サーバー証明書を最初に、中間証明書を2番目に配置し、間に空白行を空けずに結合します。
>?通常、機関が証明書を発行する際には、それに対応する説明が添付されていますので、よくお読みください。

**証明書形式および証明書チェーン形式の例**
証明書形式および証明書チェーン形式の例は次のとおりです。形式が正しいことを確認してからアップロードしてください。
1. root CA機関が発行した証明書：証明書形式はLinux環境のPEM形式です。サンプルは次のようになります。
![](https://main.qcloudimg.com/raw/cdea186a04d6f84e08fb38b19540189c.jpg)
証明書ルールは次のとおりです。
 - [——-BEGIN CERTIFICATE——-、——-END CERTIFICATE——-] を先頭と末尾にします。これらの内容を合わせてアップロードしてください。
 - 1行の文字数は64文字とし、最後の1行は64文字以内とします。
2. 中間機関が発行した証明書チェーン：
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-

 証明書チェーンルールは次のとおりです。
 - 証明書の間には空白行があってはなりません。
 - 各証明書が上記の証明書形式の要件を遵守していることとします。

## RSA秘密鍵形式の要件
サンプルは次のようになります。
![](https://main.qcloudimg.com/raw/bb9f866becc38dd28b8e62c53c1e551a.jpg)
RSA秘密鍵にはすべての秘密鍵（RSAおよびDSA）、公開鍵（RSAおよびDSA）および(x509)証明書を含めることができます。これはBase64でエンコードされたDER形式のデータを使用して保存し、ASCIIヘッダーで囲むため、システム間のテキスト形式での伝送に適しています。

RSA秘密鍵のルール：
- [——-BEGIN RSA PRIVATE KEY——-、——-END RSA PRIVATE KEY——-]を先頭と末尾にします。これらの内容を合わせてアップロードしてください。
- 1行の文字数は64文字とし、最後の1行は64文字に満たなくても構いません。

上記の方法で[——-BEGIN PRIVATE KEY——-、——-END PRIVATE KEY——-]形式の使用可能な秘密鍵を生成していない場合は、次の方法で使用可能な秘密鍵に変換することができます。
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```
その後、new_server_key.pemの内容を証明書と共にアップロードします。

## [](id:PEM)証明書のPEM形式への変換の説明
現在CLBはPEM形式の証明書のみサポートしており、他の形式の証明書はPEM形式に変換してからでなければCLBにアップロードできません。変換はopensslツールによって行うことをお勧めします。証明書の形式をPEM形式に変換する、一般的ないくつかの方法を次に挙げます。
<dx-tabs>
::: DER\sを\sPEM\sに変換
DER形式は一般的にJavaプラットフォームで用いられます。
証明書の変換：
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
秘密鍵の変換：
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```
:::
::: P7B\sを\sPEM\sに変換
P7B形式は一般的にWindows Serverおよびtomcatで用いられます。
証明書の変換：
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
outcertificat.cerの中の[——-BEGIN CERTIFICATE——-、——-END CERTIFICATE——-]の内容を取得し、証明書としてアップロードします。
秘密鍵の変換：秘密鍵は通常、IISサーバーからエクスポートできます。
:::
::: PFX\sを\sPEM\sに変換
PFX形式は一般的にWindows Serverで用いられます。
証明書の変換：
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
秘密鍵の変換：
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```	
:::
::: CER/CRT\sを\sPEM\sに変換
CER/CRT形式の証明書については、証明書ファイルの拡張子を直接変更する方法で変換することができます。例えば、証明書ファイル「servertest.crt」は「servertest.pem」に直接リネームできます。
:::
</dx-tabs>








