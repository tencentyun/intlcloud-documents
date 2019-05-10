TencentDBの複数のAvailability Zone配置によりデータベースインスタンスに高可用性と故障移行を提供します。複数のAvailability Zoneは単一のAvailability Zoneをベースに同一地域の複数のAvailability Zoneを組み合わせた物理的ゾーンです。複数のAvailability Zone配置はデータベースをデータベースインスタンスの故障とAvailability Zoneの中断から守ります。Availability Zone情報の詳細について、[地域とAvailability Zone](https://cloud.tencent.com/document/product/236/8458)を参照してください。
>**注意：**
- データベースクラスタ中のインスタンスが複数のAvailability Zoneにまたがるかどうかにかかわらず、各TencentDB for MySQLがリアルタイムにホットバックアップを行うスタンバイサーバーによりデータベースの高可用性を提供します。
- 複数のAvailability Zone配置には、TencentDB for MySQLが異なるAvailability Zoneに1つの同期予備レプリカを自動的に事前配置し維持します。
- プライマリデータベースインスタンスがAvailability Zoneにまたがって予備レプリカに同期的にコピーすることにより、データ冗長性を提供し、I/Oのフリーズを解消し、システムバックアップ期間に遅延ピークを最小限に抑えます。

### サポート地域
TencentDBの複数のAvailability Zone配置は現在深セン金融専門地区、上海地区をサポートします。
### 複数のAvailability Zone配置
1. [Tencent Cloudコンソール][https://console.cloud.tencent.com/]にログインし、ナビゲーションバー【関係型データベース】をクリックし、[データベースコンソール][https://console.cloud.tencent.com/cdb/]に入り、【新規作成】ボタンをクリックします。
2. データベース購入ページの【複数のAvailability Zone配置】の【はい】を選択します。

### 故障移行
TencentDB for MySQLが故障移行を自動的に行うため、管理の関与なくデータベース操作を速やかに復旧できます。以下のいずれかの条件が発生した場合、プライマリデータベースインスタンスが自動的に予備レプリカに切り替えます。
- Availability Zone中断
- プライマリデータベースインスタンス故障

