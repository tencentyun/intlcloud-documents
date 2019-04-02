## 概要
ユーザーは、CLSの使用中に、異なる地域でログセットとログトピックを作成することを選択できます。地域とは、物理データセンターの地理的領域を指し、異なる地域間のネットワークは完全に分離されています。ユーザーは、ログデータのアクセス遅延を減らし、アクセス速度を向上させるために、各自のビジネスシナリオとターゲットユーザーの地理的な位置に応じて最も近い地域を選択できます。


### 深セン/上海金融専門地区に関する特別な注意事項

金融業界の規制要件に合わせたコンプライアンスゾーンは、高いセキュリティと高い分離性を特徴としています。現在、CLSは深センと上海の金融専門地区をサポートしています。認証に合格した金融業界の顧客は、チケットを送信して専門地区を申請できます。[金融専門地区の紹介](https://cloud.tencent.com/document/product/304/2766)を参照してください。


## Availability Zoneと略称

| 地域     | 地域略称        | リクエストドメイン名                         |
| -------- | --------------- | -------------------------------- |
| 北京     | ap-beijing      | ap-beijing.cls.myqcloud.com      |
| 上海     | ap-shanghai     | ap-shanghai.cls.myqcloud.com     |
| 広州     | ap-guangzhou    | ap-guangzhou.cls.myqcloud.com    |
| 成都     | ap-chengdu      | ap-chengdu.cls.myqcloud.com      |
| 深セン金融 | ap-shenzhen-fsi | ap-shenzhen-fsi.cls.myqcloud.com |
| 上海金融 | ap-shanghai-fsi | ap-shanghai-fsi.cls.myqcloud.com |
| トロント   | na-toronto      | na-toronto.cls.myqcloud.com      |



## 注意事項

他のクラウド製品がCLSにアクセスする場合は、他のクラウド製品と同じログセットを選択してみてください。同じ地域のクラウド製品はプライベートネットワークを通じてデータを読み書きできるため、効果的に遅延時間を短縮し、アクセス速度を向上させることができます。
