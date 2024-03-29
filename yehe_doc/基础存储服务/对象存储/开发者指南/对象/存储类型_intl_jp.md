アクセス頻度の高低に基づき、COSは標準ストレージ、低頻度ストレージ、アーカイブストレージの3種類のオブジェクトストレージタイプを提供しています。

>オブジェクトをアップロードする際、ストレージタイプを設定しなければ、デフォルトのストレージタイプは**標準ストレージ**となります。


## 標準ストレージ

標準ストレージ（STANDARD）は信頼性と可用性の高い、ハイパフォーマンスなCOSサービスをユーザーにご提供しています。

標準ストレージはアクセス低遅延、高スループットなどの性能を有することから、大量のホットファイルへのリアルタイムアクセス、頻繁なデータインタラクションなどの業務シーンに適しています。

**特徴**

- 高信頼性、高可用性、高性能
- データ耐久性：99.999999999%
- サービス可用性：99.95%
- 応答：ミリ秒級
- サポートするリージョン：全リージョン
- ストレージ料金：標準

**適用ケース**

ホットビデオ、SNS画像、モバイルアプリケーション、ゲームプログラミング、静的ウェブサイト。

## 低頻度ストレージ

低頻度ストレージ（STANDARD_IA）は、信頼性が高く、ストレージコストが比較的低コストで、アクセス遅延が比較的少ないCOSサービスをご提供しています。

低頻度ストレージは、ストレージ価格を抑えることを基本とした上で、Time To First Byte (TTFB)をミリ秒レベルに保ち、ユーザーがデータ取得シーンで待たされることなく、高速で読み取りを行えるよう保証します。ただしデータ取得料金が発生するため、アクセス頻度が比較的低い（例えば毎月のアクセス頻度が平均1～2回などの）業務シーンに適しています。

**特徴**

- 低頻度アクセス、リアルタイム応答
- データ耐久性：99.999999999%
- サービス可用性：99.9%
- 最短課金期間：30日
- オブジェクトの最小計算単位：64KB
- TTFB遅延：ミリ秒レベル
- サポートするリージョン：全リージョン
- ストレージ料金：比較的低い

**適用ケース**

クラウドストレージデータ、ビッグデータ分析、政府・企業業務データ、低頻度ファイル、監視データ。

## アーカイブストレージ

アーカイブストレージ（ARCHIVE）は、信頼性が高く、ストレージコストが極めて低い、長期保存型のCOSサービスをご提供しています。

アーカイブストレージのストレージ単価は最も低料金ですが、データの読み取りの際に解凍時間が比較的長くかかります。従って、長期保存が必要なアーカイブデータに適しています。

**特徴**

- データ耐久性、サービス可用性、低コスト
- データ耐久性：99.999999999%
- サービス可用性：99.9%
- 最短課金期間：90日
- オブジェクトの最小計算単位：64KB
- 応答：復元には事前申請が必要
- サポートするリージョン：パブリッククラウドリージョンのみ（南京リージョンは現時点ではサポートしていません）
- ストレージ費用：極めて低い

**適用ケース**

ファイルデータ、医療用画像、科学資料といったコンプライアンス関連ファイル、ライフサイクル関連ファイル、操作ログなどのアーカイブおよびリモートディザスタリカバリ。

## ストレージタイプの比較

| 比較項目           | 標準ストレージ           | 低頻度ストレージ      | アーカイブストレージ                     |
| ---------------- | ------------------ | ------------- | ---------------------------- |
| データ耐久性        | 99.999999999%      | 99.999999999% | 99.999999999%                |
| サービス可用性       | 99.95%             | 99.9%         | 99.9%                        |
| 応答             | ミリ秒レベル             | ミリ秒レベル        | 事前に復元申請が必要               |
| オブジェクトの最小計算単位 | オブジェクトの実際のサイズによって計算 | 64KB          | 64KB                         |
| 最短課金期間     | 制限なし             | 30日          | 90日                         |
| サポートするリージョン         |  全リージョン           | 全リージョン      | パブリッククラウドリージョンにのみ適用（南京リージョンは現時点ではサポートしていません）           |
| ストレージ料金         |  標準               | 比較的低い          | 極めて低い                         |
| データ取得料金     | データ取得料金不要 | 比較的低い          | 比較的高い                         |
| 読み取り/書き込みリクエスト料金     |  極めて低い               | 比較的低い          | 極めて低い（データを標準ストレージに復元する必要あり） |




