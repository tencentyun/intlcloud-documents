### IMのプロフェッショナル版とフラッグシップ版に、1日あたりのアクティブユーザー数（DAU）の制限はありますか。
プロフェッショナル版とフラッグシップ版にはDAUの上限は設定されていません。毎月1万DAUまでは無料で提供されます。それを超えた部分には超過料金がかかり、単価は149.99 USD/万/月、1万に満たない場合は1万で計算されます。月次決済・後払い方式を採用し、毎月3日に前月（自然月）に発生した料金が引き落とされます。
月（自然月）内の毎日のDAUがいずれも1万未満の場合、その月にはDAUの超過料金は発生しません。月内のいずれか1日のDAUが1万を超えた場合、その月の最も高いピーク値を用いて決済します。 
課金ルールの詳細については、[料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

### IMでアカウントを100件作成したところエラーが表示されました。どうすればいいですか。
体験版で作成できるアカウントは最大100件までです。正式な環境で使用したい場合は、各々のSDKAppIDにそれぞれパッケージを設定する必要があります。そのほか、体験版のアカウントは削除ができますので、[アカウント削除インターフェース](https://intl.cloud.tencent.com/document/product/1047/34955)を呼び出して使用しなくなったアカウントを削除することもできます。**削除した後は、そのユーザーのデータを復元することはできません**。慎重に処理してください。

### IMは海外でのアクセスをサポートしていますか。
IMは、全世界をカバーし、コネクティビティと信頼性が高く、強力なセキュリティを備えたネットワーク接続チャネルを提供し、自社開発した最適な多重アドレッシングアルゴリズムにより、ネットワーク全体のスケジューリング機能も有しています。端末からログインすると、IM SDKが最寄りのアクセスポイントまたはアクセラレーションポイントにアクセスします。グローバルアクセス・アクセラレーションポイントの分布は以下のとおりです。

- 中国：華南、華北、華東、中国香港、台湾など。
- その他の国（または地域）：
 - アジア：シンガポール、インドネシア、アラブ首長国連邦、タイ、日本、ベトナム、インド、韓国、フィリピンなど。
 - ヨーロッパ：イギリス、オランダ、ドイツ、イタリア、ノルウェー、フランス、ロシア、スペインなど。
 - 南アメリカ：ブラジルなど。
 - 北アメリカ：アメリカ、カナダ、メキシコなど。
 - オセアニア：オーストラリアなど。
 - アフリカ：南アフリカ共和国、ナイジェリアなど。


### IMではオーディオビデオチャットルーム（50室）を作成可能ですが、3室をアクティブにしてから3室を解散した場合、あといくつ作成できますか。
3室をアクティブにしてから3室を解散した場合も50室作成できます。作成可能なオーディオビデオチャットルーム数は実質値となり、作成したチャットルームをすでに解散している場合、そのチャットルームは計上されません。オーディオビデオチャットルームが無人状態でも解散していない場合は、そのチャットルームがお客様のオーディオビデオチャットルーム1つ分のリソースを占有します。

### 作成可能な最大グループ数はいくつですか。
グループの作成に上限は設けていませんが、作成したグループ数が10万件を超過した場合は、一定のリソースの料金を支払う必要があります。累計グループ数は実質値となり、そのグループを解散した場合、グループ総数には計上されなくなります。
具体的な費用としては、累計グループ数が10万件を超えると、10万（10万に満たない場合は10万で計算）件ごとに149.99 USD/月の料金がかかります。[価格ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34350)の説明をご参照ください。


## オーディオビデオ通話機能は無料で使えますか。使用中に他に何か料金が発生しますか。

現在、オーディオビデオ通話機能は社内でテストされていますので、有効期間が60日の無料体験版を提供します。正式有料版は2022年12月にリリースされる予定です。お楽しみにしてください。
オーディオビデオ通話機能の体験版では、**体験版機能の使用権限のみが無料で提供されています。具体的な機能は、[オーディオビデオ通話機能の詳細]()をご参照ください。この機能を利用中に発生した通話時間は、[TRTC使用時間後払い](https://www.tencentcloud.com/zh/document/product/647/42734)に基づいて課金されます。IMは、[IM課金説明](https://www.tencentcloud.com/zh/document/product/1047/34349)に基づいて課金されます**。