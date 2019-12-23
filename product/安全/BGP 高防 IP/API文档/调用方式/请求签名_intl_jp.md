

Tencent Cloud APIは各アクセスリクエストを認証します。すなわち、各リクエストは、共通リクエストパラメータに署名情報（Signature）を含めてユーザーの身元を認証する必要があります。署名情報は、ユーザーが持っているセキュリティ認証によって生成されます。セキュリティ認証には、SecretIdとSecretKeyがあります。ユーザーがセキュリティ認証を持っていない場合、自分でTencent Cloudの公式Webサイトで申請する必要があります。セキュリティ認証がないと、クラウドAPIを呼び出すことができません。

## セキュリティ認証の申請
Tencent Cloud APIを初めて使用する前に、ユーザーが【Tencent Cloudコンソール】 > 【[API暗号鍵管理](https://console.cloud.tencent.com/cam/capi)】で、セキュリティ認証を申請する必要があります。セキュリティ認証には、SecretIdとSecretKeyがあります。そのうち、

- **SecretId：**API呼び出し元IDを識別するために使用されます。
- **SecretKey：**署名文字列とサーバー側の検証署名文字列を暗号化するために使用される暗号鍵。

>API暗号鍵は、Tencent Cloud APIリクエストを作成するための重要な証拠であり、Tencent Cloud APIを使用して、利用可能なすべてのTencent Cloudリソースを操作することができます。財産とサービスの安全のために、暗号鍵を適切に保管して、定期的に変更してください。暗号鍵を変更した後には、古い暗号鍵を適時に削除してください。


#### セキュリティ認証の申請手順：

1. [Tencent Cloudコンソール](https://console.cloud.tencent.com/)にログインします。
2. 【クラウド製品】をクリックして、【管理ツール】下の【クラウドAPI暗号鍵】を選択して、クラウドAPI暗号鍵管理ページにアクセスします。
![](//mc.qcloudimg.com/static/img/a771465c47830d54730f8f431d586991/image.png)
3. [ API暗号鍵管理](https://console.cloud.tencent.com/capi)ページで、【暗号鍵の新規作成】をクリックして、SecretId/SecretKeyのペアを作成できます。

>
> - 開発者アカウントは、最大2組のSecretId/SecretKeyを持つことができます。
> - サブユーザーとして開発者によって追加されたQQアカウントは、異なる開発者コンソールで異なるセキュリティ認証を申請できます。
> - サブユーザーのセキュリティ認証は、現在、一部のAPIのクラウドAPIのみを呼び出すことができます。

##  署名文字列の生成
セキュリティ認証SecretIdとSecretKeyがあれば、署名文字列を生成できます。署名文字列を生成する詳細なプロセスは以下の通りです。

![](//mc.qcloudimg.com/static/img/3a3a616ba175bb95be68123d86715e77/image.png)

例えば、ユーザーのSecretIdとSecretKeyが次のようになるとします。
SecretId： AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
SecretKey： Gu5t9xGARNpq86cd98joQYCN3Cozk1qA

>これは一例に過ぎません。ユーザーは実際のSecretIdとSecretKey、およびリクエストパラメータに従って、操作を続けてください。

Tencent Cloud CVMを例として、ユーザーがTencent Cloud CVMの[インスタンスリストの表示](https://cloud.tencent.com/document/api/213/15728)（DescribeInstances）APIを呼び出すとき、リクエストパラメータは次のようになります。

| パラメータ名 | 説明 | パラメータ値| 
|---------|---------|---------|
| Action | メソッド名| DescribeInstances | 
| SecretId | 暗号鍵ID  | AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA | 
| Timestamp | 現在のタイムスタンプ | 1465185768 | 
| Nonce | ランダムな正の整数 | 11886 | 
| Region | インスタンスの所属地域 | ap-guangzhou | 
| SignatureMethod | 署名方法 | HmacSHA256 | 
| InstanceIds.0 | 照合待ちのインスタンスID | ins-09dx96dg | 

### 1. パラメータを並び替えます
まず、すべてのリクエストパラメータをパラメータ名の昇順で辞書順に並べ替えます。（辞書順の昇順に並べ替えとは、単語が辞書で並べ替えられる順と同じです。アルファベットまたは数字の昇順に従って並べ替え、すなわち、まず最初の「アルファベット」を比較し、同じ場合、2番目の「アルファベット」を比較するようにします。）プログラム言語の関連並べ替え関数を使用してこの機能を実現できます。例えば、PHPの中のksort関数。上記のパラメータ例の並べ替え結果は次の通りです。

```shell
{
    "Action" : "DescribeInstances",
    "InstanceIds.0" : "ins-09dx96dg",
    "Nonce" : 11886,
    "Region" : "ap-guangzhou",
    "SecretId" : "AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA",
    "SignatureMethod" : "HmacSHA256",
    "Timestamp" : 1465185768
}
```
同じ結果を取得できれば、他のプログラム言語で上記の例のパラメータを並べ替えることも可能です。

### 2. リクエスト文字列をつなぎ合わせます
このステップはリクエスト文字列を生成します。
前のステップで並べ替えられたリクエストパラメータを`「パラメータ名」=「パラメータ値」`の形式にフォーマットします。例えば、Actionパラメータに対して、そのパラメータ名が`「Action」`で、パラメータ値が`「DescribeInstances」`なので、フォーマットされた後に、`Action=DescribeInstances`になります。

>
- 「パラメータ値」は元の値であり、URLエンコード値ではありません。
- 入力されたパラメータのKeyにアンダースコアが含まれている場合は、それを`.`に変換する必要がありますが、Valueの中のアンダースコアが変換する必要はありません。例えば、`Placement_Zone=CN_GUANGZHOU`が`Placement.Zone=CN_GUANGZHOU`に変更必要があります。

それから、フォーマットされた各パラメータを`「＆」`でつなぎ合わせて、最後に生成されたリクエスト文字列は次の通りです（テキスト中の改行を無視してください）：

```shell
Action=DescribeInstances
&InstanceIds.0=ins-09dx96dg
&Nonce=11886
&Region=ap-guangzhou
&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
&SignatureMethod=HmacSHA256
&Timestamp=1465185768
```

### 3. 署名原文文字列をつなぎ合わせます
このステップで署名原文文字列を生成します。
署名原文文字列のつなぎ合わせ規則は次の通りです。
> **リクエスト方法 + リクエストCVM +リクエストパス + ? + リクエスト文字列**

パラメータ構成の説明：
* **リクエスト方法：** POSTおよびGETの方法をサポートします。ここでGETリクエストを使用します。メソッドはすべて大文字です。
* **リクエストCVM：**つまりCVMドメイン名。リクエストドメイン名は、APIが属する製品またはそれが属する製品のモジュールによって決まり、異なる製品または異なる製品のモジュールのリクエストドメイン名は異なります。例えば、Tencent Cloud CVMの照合インスタンスリスト（DescribeInstances）のリクエストドメイン名：`cvm.api.qcloud.com`。具体的な製品リクエストドメイン名については、各APIの説明を参照してください。
* **リクエストパス：** Tencent Cloud APIの対応製品のリクエストパスは、通常、1つの製品に1つの固定パスが対応します。例えば、Tencent Cloud CVMの固定リクエストパスは`/v2/index.php`です。
* **リクエスト文字列：** つまり前のステップで生成されたリクエスト文字列です。


したがって、上記の例の署名原文文字列のつなぎ合わせ結果は次のようになります（テキスト中の改行を無視してください）：
```shell
GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances
&InstanceIds.0=ins-09dx96dg
&Nonce=11886
&Region=ap-guangzhou
&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
&SignatureMethod=HmacSHA256
&Timestamp=1465185768
```

### 4. 署名文字列を生成します
このステップで署名文字列を生成します。
>署名の計算方法はHmacSHA256とHmacSHA1という2種類があります。ここでは、指定した署名アルゴリズム（SignatureMethodパラメータ）に基づいて署名文字列を生成します。SignatureMethodをHmacSHA256と指定した場合、HmacSHA256を使用して署名を計算する必要があり、それ以外の場合、HmacSHA1を使用して署名を計算します。

まず、署名アルゴリズム（HmacSHA256またはHmacSHA1）を使用して前の手順で取得した**署名原文文字列**に署名します。次に、Base64を使用して生成された署名文字列をコーディングして最終署名文字列を取得します。

具体的なコードは以下の通りです。PHP言語を例として、この例で使用された署名アルゴリズムが**HmacSHA256**ですので、生成された署名文字列のコードは以下の通りです（取得された署名文字列が例と一致する限り、他のプログラム言語で上記の例の原文文字列を使用して署名検証を実行することも可能です）：

```php
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3Cozk1qA';
$srcStr = 'GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Nonce=11886&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&SignatureMethod=HmacSHA256&Timestamp=1465185768';
$signStr = base64_encode(hash_hmac('sha256', $srcStr, $secretKey, true));
echo $signStr;
```

最後に取得された署名文字列は：

```
0EEm/HtGRr/VJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s=
```

同じように、指定された署名アルゴリズムが**HmacSHA1**の場合、署名文字列を生成するコードは次のようになります：
```php
$secretKey = 'Gu5t9xGARNpq86cd98joQYCN3Cozk1qA';
$srcStr = 'GETcvm.api.qcloud.com/v2/index.php?Action=DescribeInstances&InstanceIds.0=ins-09dx96dg&Nonce=11886&Region=ap-guangzhou&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA&SignatureMethod=HmacSHA1&Timestamp=1465185768';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $secretKey, true));
echo $signStr;
```

最後に取得された署名文字列は：
```
nPVnY6njQmwQ8ciqbPl5Qe+Oru4=
```


##  署名文字列のコーディング
生成された署名文字列はリクエストパラメータとして直接使用することはできません。URLコーディングする必要があります。
前のステップで生成された署名文字列が`0EEm/HtGRr/VJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s=`であれば、コーディング後は`0EEm%2FHtGRr%2FVJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s%3D`になります。したがって、最後に取得された署名文字列リクエストパラメータ（Signature）が`0EEm%2FHtGRr%2FVJXTAD9tYMth1Bzm3lLHz5RCDv1GdM8s%3D`で、これで最後のリクエストURLを生成します。

>ユーザーのリクエスト方法がGETの場合、すべてのリクエストパラメータのパラメータ値に対してURLコーディングを行う必要があります；さらに、一部の言語ライブラリは自動的にURLをコーディングし、コーディングを繰り返すと署名の検証が失敗する場合があります。

## 認証失敗
認証が失敗すると、下表のようなエラーが発生する可能性があります。

| エラーコード | エラータイプ | エラー説明|
|---------|---------|---------|
| 4100 | 身元認証失敗 | 身元認証失敗。リクエストパラメータのSignatureが上記のように正しく計算されていることを確認してください。特に、リクエストを送信する前に、SignatureのURLコーディングを行う必要があることとにも注意してください。|
| 4101 | 開発者がこのAPIにアクセスすることを許可していない | このサブユーザーがこのAPIを呼び出す権限がありません。開発者に連絡して承認を依頼してください。詳細については、[認証ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)を参照してください。|
| 4102 | 開発者がこのAPIで操作されているリソースにアクセスすることを許可していない | リクエストされたリソースパラメータの中に、開発者がアクセスを許可していないリソースがあります。messageフィールドで、表示が許可されていないリソースIDを参照してください。</br>開発者に連絡して承認を依頼してください。詳細については、[認証ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)を参照してください。|
| 4103 | 開発者以外のSecretIdは、このAPIの呼び出しをサポートしない | サブユーザーのSecretIdでこのAPIを呼び出すことはできません。開発者だけが呼び出し可能です。|
| 4104 | SecretIdが存在しない | 署名に使用されたSecretIdが存在しないか、暗号鍵のステータスが正しくありません。API暗号鍵が有効で禁止されていないことを確認してください。|
| 4110 | 認証失敗 | 権限の検証に失敗しました。アクセスしたリソースを使用する権限があることを確認してください。|
| 4500 | リプレイ攻撃エラー | Nonceパラメータは2回繰り返すことはできません。TimestampはTencentサーバーの時間から2時間以上離れてはいけません。|

