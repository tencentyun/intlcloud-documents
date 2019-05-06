COSは、多地域のストレージをサポートします。地域によってデフォルトのアクセスドメイン名が異なります。バケットを作成する時に選択した地域を変更できません。自分の業務シナリオにより近い地域を選択し、それによりオブジェクトのアップロード、ダウンロード速度を向上させます。

## 利用可能な地域およびアクセスドメイン名
>!
>- バケットを作成した後に対応するデフォルトのドメイン名を生成します。[COSコンソール](https://console.cloud.tencent.com/cos5)に進み、バケット【ドメイン名管理】で確認できます。
>- BucketNameは、バケットを作成する時に入力されたカスタマイズ名です。詳細について[バケット命名規則](https://cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83)を参照してください。
>- APPIDは、Tencent Cloudアカウント申請後に得られたアカウントです。システムにより自動的に割り当てられ、固定性と唯一性があります。[Tencent Cloudコンソール](https://console.cloud.tencent.com)を介して【アカウント情報】で確認できます。
>- 過去バージョンの対応地域情報について、[過去バージョン地域リスト](https://cloud.tencent.com/document/product/436/7777)を参照してください。


| 地域       | 地域略語         | デフォルトのドメイン名（アップロード/ダウンロード/管理）                          |
| -------- | ------------ | ---------------------------------------- |
| 北京1区（売り切れ）| ap-beijing-1 | &lt;BucketName-APPID&gt;.cos.ap-beijing-1.myqcloud.com |
| 北京       | ap-beijing   | &lt;BucketName-APPID&gt;.cos.ap-beijing.myqcloud.com |
| 上海（華東）   | ap-shanghai  | &lt;BucketName-APPID&gt;.cos.ap-shanghai.myqcloud.com |
| 広州（華南）   | ap-guangzhou | &lt;BucketName-APPID&gt;.cos.ap-guangzhou.myqcloud.com |
| 成都（西南）   | ap-chengdu   | &lt;BucketName-APPID&gt;.cos.ap-chengdu.myqcloud.com |
| 重慶       | ap-chongqing | &lt;BucketName-APPID&gt;.cos.ap-chongqing.myqcloud.com |
| シンガポール      | ap-singapore | &lt;BucketName-APPID&gt;.cos.ap-singapore.myqcloud.com |
| 香港       | ap-hongkong  | &lt;BucketName-APPID&gt;.cos.ap-hongkong.myqcloud.com |
| トロント      | na-toronto   | &lt;BucketName-APPID&gt;.cos.na-toronto.myqcloud.com |
| フランクフルト     | eu-frankfurt | &lt;BucketName-APPID&gt;.cos.eu-frankfurt.myqcloud.com |
| ムンバイ       | ap-mumbai    | &lt;BucketName-APPID&gt;.cos.ap-mumbai.myqcloud.com |
| ソウル       | ap-seoul     | &lt;BucketName-APPID&gt;.cos.ap-seoul.myqcloud.com |
| シリコンバレー       | na-siliconvalley     | &lt;BucketName-APPID&gt;.cos.na-siliconvalley.myqcloud.com |
| バージニア       | na-ashburn     | &lt;BucketName-APPID&gt;.cos.na-ashburn.myqcloud.com |
| バンコク       | ap-bangkok     | &lt;BucketName-APPID&gt;.cos.ap-bangkok.myqcloud.com |
| モスクワ       | eu-moscow     | &lt;BucketName-APPID&gt;.cos.eu-moscow.myqcloud.com |
|東京       |ap-tokyo  |     &lt;BucketName-APPID&gt;.cos.ap-tokyo.myqcloud.com |

> 例：
> ユーザは所属地域が広州であるバケットを作成し、examplebucketをバケットに名前付け、ユーザのAPPIDを1250000000にすると、バケットのデフォルトのドメイン名：
```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

## プライベートネットワークとパブリックネットワークのアクセス
COSのアクセスドメイン名は、スマートDNS解析を使用し、さまざまな通信プロバイダーのインターネット環境で、COSにアクセスする最適のリンクを検出し、指定します。

Tencent CloudでCOSアクセス用サービスを配置した場合、同じ地域範囲内のアクセスが自動的にプライベートネットワークアドレスに指定されます。地域間にはプライベートネットワークアクセスをサポートしません。デフォルトでパブリックネットワークアドレスが解析されます。

プライベートネットワークとパブリックネットワークのアクセスの関連情報について、[リクエスト作成概要](https://cloud.tencent.com/document/product/436/31315) ドキュメントを参照してください。


