## リソースパックの使用説明

 メディア処理リソースパックは、リソースを使用する前に、あらかじめメディア処理リソースを購入する方式です。**リソースパックごとに、その機能のリソースのみの相殺をサポートしています**。

## 注意事項：

- リソースパックは購入後すぐ有効になります。有効期間は1年間ですので、リソースパックの有効期間内にご使用ください。有効期限後のリソースパック内のリソースは無効となり、ご利用になれませんのでご注意ください。
- リソースパックは、日次決済のユーザーにのみ購入利用をサポートしています。ユーザーが月次決済に切り替える際に、アカウント内にリソースパックがある場合は、そのリソースパックは凍結され利用できなくなります。
- ユーザーが毎日消費する各メディア処理リソースは、優先的に対応するリソースパック内から相殺され、**対応するリソースを超過する部分**については[従量課金](https://intl.cloud.tencent.com/document/product/1041/33478)に基づき課金します。支払い遅延によりサービスが使用できなくなることを防止するため、リソースパックの消費状況に注意し、適時、リソースパックを購入するか、またはアカウントの残高をチャージしてください。
- リソースパックは重複して購入できます。つまり有効期限内のリソース容量を増やすことができます。リソースパックが複数ある場合は、購入時期の早いものから先に相殺されます。
- 各リソースパックの有効期間は独立して計算されます。複数のリソースパックの有効期限を合算しません。
- メディア処理が提供するリソースパックは、メディア処理製品の有料サービスの使用量についてのみ相殺可能です。
- リソースパックは、5日間は理由の有無を問わず返金可能です（指定条件あり）、 [返金についての説明](https://intl.cloud.tencent.com/document/product/1041/33481) をご参照ください。
- メディア処理は毎日未明に前日に発生した料金が決済されます。リソースパックは購入当日から有効ですので、購入当日のリソースパックは、当日決済の（前日に発生した）料金を相殺することはできません。
- リソースパックのアクティブ化および残容量の状況確認は、コンソールへ移動し、管理者ロール下の、[リソースパック管理](https://intl.cloud.tencent.com/document/product/1041/48790)をご参照ください。


## リソースパックタイプの説明

| リソースパックタイプ               | 説明                                                         |
| --------------------------- | ------------------------------------------------------------ |
| [通常トランスコードパック](#ntrans_page)  | メディア処理の**通常トランスコード、アダプティブビットレートストリーミング**で発生した使用量を相殺可能で、**使用時間**に基づき販売します。トランスコードリソースパックはリージョンを問わず相殺されます。 |
| [超高速HDパック](#ntrans_page)  | メディア処理の**超高速HD（TESHD）**で発生した使用量を相殺可能で、**使用時間**に基づき販売します。超高速HDパックはリージョンを問わず相殺されます。 |

[コンソール](https://console.cloud.tencent.com/mps) でメディア処理リソースの実際の使用量を確認できます。リソースパックの購入は [リソースパック購入ページ](https://buy.cloud.tencent.com/mps)に移動してください。

[](id:ntrans_page)

## 通常トランスコードパック

メディア処理の通常トランスコードパックの専用リソースパックは、メディア処理の*通常トランスコードパック、アダプティブビットレートストリーミング**で発生した使用量を相殺可能です（リージョンを問わず相殺）。通常トランスコードパックは重複して購入できます。複数の通常トランスコードパックが存在する場合は、購入時期の早いものから先に相殺されます。システムは毎日使用したトランスコードの総時間を集計し、リソースパックの容量および解像度の範囲内については、直接残容量から相殺します。リソースパックを超過する部分については[従量課金](https://intl.cloud.tencent.com/document/product/1041/33478)に基づき課金します。

**相殺のルール**：中国本土、中国本土以外のすべてで1：1の比率で相殺します。

### 課金価格

| リソースパックタイプ           | 単価（USD） |
| :------------------- | :--------- |
| 通常トランスコードパック - 5H      | 0.8        |
| 通常トランスコードパック  - 100H    | 16         |
| 通常トランスコードパック  - 1000H   | 151        |
| 通常トランスコードパック - 10000H  | 1058       |
| 通常トランスコードパック - 50000H  | 4056       |
| 通常トランスコードパック - 100000H | 7760       |

### 相殺の比率

メディア処理の通常トランスコードリソースパックは、すべての通常トランスコードの仕様の異なるビデオを相殺可能です。ただし相殺の比率が異なります。相殺の比率は次のとおりです。

| コーデック | 解像度                      | 相殺の比率                         |
| :------- | :-------------------------- | :------------------------------- |
| オーディオトランスコード | -                           | 1 **:** 0.25                     |
| Remux   | -                           | 1 **:** 0.5                      |
| H.264    |  標準SD（短辺 ≤ 480px）     | 1 **:** 1                        |
| H.264    |  高精細度HD（短辺 ≤ 720px）     | 1 **:** 2                        |
| H.264      | フル高精細度FHD（短辺 ≤ 1080px） | 1 **:** 4                        |
| H.264    | 2K（短辺 ≤ 1440px）         | 1 **:** 8                        |
| H.264    | 4K（短辺 ≤ 2160px）         | 1 **:** 16                       |
| H.265    | 標準SD（短辺 ≤ 480px）     | 1 **:** 5                        |
| H.265    | 高精細度HD（短辺 ≤ 720px）     | 1 **:** 10                       |
| H.265    | フル高精細度FHD（短辺 ≤ 1080px） | 1 **:** 20                       |
| H.265    | 2K（短辺 ≤ 1440px）         | 1 **:** 40                       |
| H.265    | 4K（短辺 ≤ 2160px）         | 1 **:** 80                       |
| AV1    | 標準SD（短辺 ≤ 480px）    | 1 **:** 10                       |
| AV1    | 高精細度HD（短辺 ≤ 720px）     | 1 **:** 20                       |
| AV1    | フル高精細度FHD（短辺 ≤ 1080px） | 1 **:** 40                       |
| AV1    | 2K（短辺 ≤ 1440px）         | 1 **:** 80                       |
| AV1    | 4K（短辺 ≤ 2160px）        | 1 **:** 160                      |

### 課金の例

- ユーザーが通常トランスコードH.264 640 × 480のビデオを1分間出力した場合、通常トランスコードのリソースパック内の時間が1分間減ります。
- ユーザーが通常トランスコードH.264 1280 × 720のビデオを1分間出力した場合、通常トランスコードのリソースパック内の時間が2分間減ります。
- アダプティブビットレートのリソースパックの相殺時間は、すべてのサブストリームの相殺時間の合計と一致します。

出力するビデオの解像度が高いほど、リソースパックを使い切る速度は速くなります。 


[](id:strans_page)

## 超高速HDパック

メディア処理の超高速HDパックを処理する専用リソースパックは、メディア処理の*高速高画質トランスコーディング**で発生した使用量を相殺可能です（リージョンを問わず相殺）。超高速HDパックは重複して購入できます。複数の超高速HDパックが存在する場合は、購入時期の早いものから先に相殺されます。システムは毎日使用した超高速HD（TESHD）の総時間を集計し、リソースパックの容量及び解像度の範囲内については、直接残容量から相殺します。リソースパックを超過する部分については[従量課金](https://intl.cloud.tencent.com/document/product/1041/33478)に基づき課金します。

**相殺のルール**：中国本土、中国本土以外のすべてで1：1の比率で相殺します。

### 課金価格

| リソースパックタイプ           | 単価（USD） |
| :------------------- | :--------- |
| 超高速HDパック - 50H     | 26         |
| 超高速HDパック - 100H    | 53         |
| 超高速HDパック - 1000H   | 312        |
| 超高速HDパック - 10000H  | 2645       |
| 超高速HDパック - 100000H | 17637      |

### 相殺の比率

メディア処理の超高速HD（TESHD）リソースパックは、すべての超高速HD（TESHD）の仕様の異なるビデオを相殺可能です。ただし相殺の比率が異なります。相殺の比率は次のとおりです。

| コーデック | 解像度                      | 相殺の比率   |
| :------- | :-------------------------- | :--------- |
| H.264    | 標準SD（短辺 ≤ 480px）     | 1 **:** 1  |
| H.264    | 高精細度HD（短辺 ≤ 720px）     | 1 **:** 2  |
| H.264      | フル高精細度FHD（短辺 ≤ 1080px） | 1 **:** 4  |
| H.264    | 2K（短辺 ≤ 1440px）         | 1 **:** 8  |
| H.264    | 4K（短辺 ≤ 2160px）         | 1 **:** 16 |
| H.265    | 標準SD（短辺 ≤ 480px）     | 1 **:** 5  |
| H.265    | 高精細度HD（短辺 ≤ 720px）     | 1 **:** 10 |
| H.265    | フル高精細度FHD（短辺 ≤ 1080px） | 1 **:** 20 |
| H.265    | 2K（短辺 ≤ 1440px）         | 1 **:** 40 |
| H.265    | 4K（短辺 ≤ 2160px）         | 1 **:** 80 |
| AV1    | 標準SD（短辺 ≤ 480px）     | 1 **:** 10  |
| AV1    | 高精細度HD（短辺 ≤ 720px）     | 1 **:** 20  |
| AV1    | フル高精細度FHD（短辺 ≤ 1080px） | 1 **:** 40  |
| AV1    | 2K（短辺 ≤ 1440px）         | 1 **:** 80  |
| AV1    | 4K（短辺 ≤ 2160px）         | 1 **:** 160 |

### 課金の例

- ユーザーが超高速HD（TESHD）のH264 640 × 480のビデオを1分間出力した場合、超高速HD（TESHD）のリソースパック内の時間が1分間減ります。
- ユーザーが超高速HD（TESHD）の H.264 1280 × 720のビデオを1分間出力した場合、超高速HD（TESHD）のリソースパック内の時間が2分間減ります。

出力するビデオの解像度が高いほど、リソースパックを使い切る速度は速くなります。 
