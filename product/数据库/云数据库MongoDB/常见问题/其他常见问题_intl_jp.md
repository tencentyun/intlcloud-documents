### TencentDB for MongoDBの最新バージョン番号は？
TencentDB for MongoDBは現在提供するバージョン番号は3.2.10と3.6.3です。

### MongoDBクラウドデータベースを削除するにはどうすればよいですか。期限切れ後更新しなければ自動的に削除されますか？
TencentDB for MongoDBインスタンスは有効期限が切れた後、更新しなければ、自動的に終了されますので、データを確認してバックアップしてください。コンソールインスタンスリストで【操作】> 【その他】> 【返品払戻】を選択すると、セルフ終了操作が実行されます。

### TencentDB for MongoDBはセキュリティ認証情報の申請方法。
初めてクラウドAPIを使用する前に、Tencent Cloud CVMコンソールでセキュリティ認証情報を申請する必要があります。
セキュリティ認証情報はSecretIdとSecretKeyを含みます。

- SecretId：API呼び出し元IDを識別するために使用されます。
- SecretKey：署名文字列とサーバー側の検証署名文字列を暗号化するために使用される暗号鍵。

>!API暗号鍵は、Tencent Cloud APIリクエストを作成するための重要な証拠であり、Tencent Cloud APIを使用して、利用可能なすべてのTencent Cloudリソースを操作することができます。財産とサービスの安全のために、暗号鍵を適切に保管して、定期的に変更してください。暗号鍵を変更した後には、古い暗号鍵を適時に削除してください。詳細については[署名方法](https://cloud.tencent.com/document/product/240/8329)を参照してください。
 
### TencentDB for MongoDBユーザー名の使用制限は？
Tencent Cloudには、rwuserとmongouserという2つのデフォルト内部構築ユーザーがあります。内部構築ユーザーのロールは[readWriteAnyDatabase + dbAdmin](https://docs.mongodb.com/v3.0/reference/built-in-roles/)です。つまり、このユーザーを使用して任意のデータベースを読み書きできますが、リスクの高い操作の権限はありません。
TencentDB for MongoDBのバージョンによって、一部のインスタンスにはrwuserしかありません（このインスタンスに対して、Tencent Cloudがアップグレードされ、アップグレード前にお客様に連絡します）。
ビジネスニーズを満たすために、アカウントと権限の管理にTencentDB for MongoDBコンソールを使用することもできます。詳細については[制限の説明](https://cloud.tencent.com/document/product/240/622)を参照してください。
 
### MongoDBの選択できるノードが何ですか？
Tencent Cloudホスティングデータセンタはグローバルで複数の場所に設置されています。中国では華南、華東、華北という3つの地区をカバーしています。東南アジアに対して、中国の香港ノードでカバーし、北米に対して、データセンタノードはトロントにあります。
Tencent Cloudは、より多くのノードをカバーするように、利用可能な地域を徐々に増やしています。ノードは、地域（region）とAvailability Zone（zone）で構成されています。
 
- **地域**
Tencent Cloudは現在以下の選択できる地域（region）を提供します。
中国本土地区：華南地区（広州）、華東地区（上海）、華北地区（北京）。
海外地区：東南アジア地区（中国香港）と北米地区（トロント）。
- **ノード**
Availability Zoneとは、同じ地域内で電力とネットワークがお互いに独立しているTencent Cloudの物理データセンターです。
その目標は、Availability Zone間の障害を互いに分離して（大規模な災害や大規模な電源障害を除く）、障害が拡散しないようにして、ユーザー業務の継続的な可用性を保証することです。
[華南地区]広州1区（完売）、広州2区、広州3区
[華東地区]上海1区
[華北地区]北京1区
[東南アジア地区]中国香港1区
[北米地区]トロント1区
詳細については、[MongoDB地域選択](https://cloud.tencent.com/document/product/240/3637)を参照してください。
 


