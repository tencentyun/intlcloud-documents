[//]: # (chinagitpath:XXXXX)

完全なTencent Cloud APIリクエストには、共通リクエストパラメータとAPIリクエストパラメータの2種類のリクエストパラメータが必要です。この文章では、Tencent Cloud APIリクエストに必要なAPIリクエストパラメータについて説明します。APIリクエストパラメータの詳細については、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/377/4153)の章を参照してください。
APIリクエストパラメータは具体的なAPIと関連します。異なるAPIでサポートされているAPIリクエストパラメータは異なります。共通リクエストパラメータと異なって、APIリクエストパラメータの最初の文字は小文字です。
>**注意：**
>文章に記載されているパラメータはTencent Cloud CVMを例として挙げられますが、各Tencent Cloud製品の実際のパラメータについては、実際の製品APIパラメータを参照してください。

以下のパラメータリストは、Tencent Cloud CVM[インスタンスリストの照合](https://cloud.tencent.com/document/api/229/831)のAPI（DescribeInstances）を例とします。このAPIがサポートしているAPIリクエストパラメータは以下の通りです。

| パラメータ名 |   説明 | タイプ |必須  |
|---------|---------|---------|---------|
| instanceIds.n  |照合するCVMインスタンスID配列、配列の添字は0から始まります。instanceIdとunInstanceIdを使用できますが、統一のリソースID：unInstanceIdを使用することをお勧めします。| String |いいえ |  
| lanIps.n | 照合するCVMのプライベートネットワークIP配列。 | String | いいえ | 
| searchWord | ユーザーが設定されたCVM別名。| String | いいえ |
| offset |オフセット、デフォルトは0です。 |   Int | いいえ |
| limit | 一度に照合できるサーバーの最大数、デフォルトは20、最大は100です。|Int | いいえ | 
| status | 照合待ちのCVMのステータス。| Int | いいえ |
| projectId |  プロジェクトID。転送しないとすべてのプロジェクトのCVMインスタンスを照合します。| String |いいえ |
| simplify | 非リアルタイムデータを取得。転送されたパラメータにsimplify=1を追加する場合、非リアルタイムデータを取得します。| Int | いいえ |
| zoneId |Availability Zone ID。転送しないとすべてのAvailability ZoneのCVMインスタンスを照合します。Availability Zoneを指定する必要があれば、[Availability Zoneの照合](https://cloud.tencent.com/document/api/213/15707)（DescribeAvailabilityZones）APIを呼び出して照合できます。|  Int | いいえ |

各フィールドの説明は以下の通りです。

**パラメータ名**このAPIでサポートされているリクエストパラメータの名前。このAPIを使用する場合、ユーザーはそれをAPIリクエストパラメータとして使用できます。パラメータ名が「.n」で終わっていれば、このパラメータが配列であることを意味するので、使用時に配列パラメータを順番に渡す必要があります。
**必須：**このパラメータが必須かどうかを示すタグ。「はい」：このAPIを呼び出すとき、パラメータを渡す必要がある；「いいえ」：パラメータを渡す必要がない。
**タイプ：**このAPIパラメータのデータタイプ。
**説明：**このAPIリクエストパラメータの内容を簡単に説明します。

### 使用例
Tencent Cloudの各クラウド製品APIリクエストリンクでは、APIリクエストパラメータは次の通りです。Tencent Cloud CVMを例として、ユーザーがスケーリンググループのリストを照合したい場合、リクエストリンクは次の形式になります。

<pre>
https://cvm.api.qcloud.com/v2/index.php?
&<共通リクエストパラメータ>
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003
</pre>


