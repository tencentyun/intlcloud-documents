﻿
- サブスクリプション・前払い：TencentDB for MySQLの返品・返金を申請した場合、全額でない返金として扱います。
- 従量課金・後払い：TencentDB for MySQLのリソースを直接クリアし、返金することはできません。
サブスクリプションインスタンスと従量課金インスタンス両方とも[TencentDB for MySQLコンソール](https://console.tencentcloud.com/cdb/instance?language=en)のインスタンスリストでセルフ返品を操作できます。

## セルフ返品の説明
- インスタンスを返した後、インスタンスのステータスが「隔離中」になると、このインスタンスに関連する費用が発生しなくなります。
- インスタンスを完全に廃棄した後、データを復元できませんので、事前にインスタンスのデータをバックアップしてください。
- インスタンスを完全に廃棄した後、データベースのバックアップを削除しますので、事前にデータベースのバックアップをダウンロードしてください。
- インスタンスを完全に廃棄した後、データベース監査を削除しますので、事前にデータベースの監査ログをダウンロードしてください。
- サブスクリプションインスタンスが完全に廃棄されると、IPリソースが同時にリリースされ、インスタンスもアクセスできなくなります。このインスタンスには関連付けられた読取専用インスタンスまたはディザスタリカバリインスタンスがある場合
  - 読取専用インスタンスは同時に廃棄されます。
  - ディザスタリカバリインスタンスは同期接続が切断され、自動的にマスターインスタンスに昇格します。
- 従量課金インスタンスを手動で返すと、インスタンスはTencentDBごみ箱に移動され7日間保持されます。その間、インスタンスにはアクセスできません。手動で返したインスタンスを復元するには、TencentDBごみ箱で支払期間を更新してから復元してください。
- 異常返品/悪意のある返品の疑いがある場合、Tencent Cloudには返品申請を拒否する権利があります。
- 一部のイベント参加によって入手したリソースはセルフ返品できません。詳しくは、公式サイトでの紹介をご確認ください。

## 一般セルフ返品
一般セフル返品の場合、使用済み分の利用料金を差し引きしてから、購入したときに使用された現金とクーポンの比率でTencent Cloudアカウントに返金されます。

#### 一般セルフ返品ルール
**返金額 = 現在の有効注文金額 + 未開始注文金額 - 使用済みリソース価額**

- 現在の有効注文金額：割引とクーポンを除く、有効な注文の支払い金額。
- 未開始注文金額：割引とクーポンを除く、将来の有効注文金額。
- 使用済みリソース価額は、次のポリシーで計算されます。
 - 使用済み分は、返金を申請した当日から1ヶ月を満たした場合、1ヶ月で差し引かれ、1ヶ月未満の場合、従量課金で差し引かれます。
 - 使用済み部分は、秒まで正確です。
 -  返金額が0以下の場合、0で計算してリソースをクリアします。

>!
>- 控除金額とクーポンは返金できません。
>- 返金額は購入時に使用した現金とボーナスの比率でTencent Cloudアカウントに返金されます。

## 関連操作
コンソールで従量課金インスタンスとサブスクリプションインスタンスをセルフ返金するには、[インスタンスの廃棄](https://www.tencentcloud.com/document/product/236/31895?lang=en&pg=)をご参照ください。