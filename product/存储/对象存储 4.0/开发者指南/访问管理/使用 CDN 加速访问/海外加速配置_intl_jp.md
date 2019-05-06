## 概要

Tencent Cloudの GCD（Global Content Delivery）はTencent Cloudの高性能の加速ノードを世界中で拡張し、世界中で静的コンテンツ加速、ダウンロード配布加速および音声映像VOD加速等の様々な機能へのサポートを提供しています。
現時点では、Tencent Cloud GCDはパブリックテストの段階にあります。テスト対象者の定員が限られているため、テストにつき、パブリックテストの申請書でお申し込みください。詳しくは[申請方法](https://cloud.tencent.com/document/product/673/30415)を参照してください。以下、CDN GCDの構成方法を詳しく説明します。

>!ご申請により、GCD製品をご利用いただけます。

## 適用シナリオ

- 海外のエンドユーザーにアプローチし、アクセスを加速し、またアクセスの時間遅延を改善します。
- 複数の地区、国または大陸間で数GBから数TBまでのデータを送信するシナリオ。
- 高密度で同じコンテンツのダウンロードを繰り返すシナリオ。

## 関連説明

GCD製品の使用申請が承認された方は、Tencent Cloud [GCDコンソール](https://console.cloud.tencent.com/cdn/open_oversea)にアクセスしてCOSのXMLアクセスドメイン名を追加することで加速を実現できます。
現時点では、COSにおいてアクセス内容を**公開**に設定することで、GCDドメイン名をバインディングしてCOSにおける内容にアクセスできます。

## 操作手順
下記操作手順に従って構成を進めてください：【Policy権限の構成】>【GCDへの接続】>【CNAMEの構成】。

### Policy権限の構成

1. Tencent Cloud [COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、管理ページに進みます。【権限の管理】タブをクリックし、公開のアクセスポリシーを追加します。
![](https://main.qcloudimg.com/raw/b1c0862f797da9d1447bc6a13929a927.png)
2. 【ポリシーの追加】をクリックし、下記設定により**ユーザー**、**リソース**と**操作**を構成してください。
 - 効力：許可。
 - ユーザー：すべてのユーザー。
 - リソース：バケット全体。
 - 操作：ファイルの読み取り権限。
![](https://main.qcloudimg.com/raw/953311e15a9ca272dc5fece6a87ac6b7.png)

### GCDへの接続

1. COSドメイン名の取得
[COSコンソール](https://console.cloud.tencent.com/cos5)にて、加速を必要とするバケットのアクセスドメイン名を取得してください。例えば：
```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```
静的サイト機能をオンにしているバケットを加速し、かつ静的サイトの関連機能を使用する場合、静的サイトのドメイン名を使用してください。例えば：
```shell
examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```

2. ドメイン名への接続
Tencent Cloud [GCDコンソール](https://console.cloud.tencent.com/cdn/open_oversea)にログインし、COSにドメイン名を追加します。その構成アイテムの説明を下記に示します：
 - Domain（ドメイン名）：GCDプラットフォームにバインディングするアクセスドメイン名を記入してください。
 - Service Type（サービスタイプ）：COSの多くが非構造化データなので、静的加速Static Contentを使用してください。
 - Origin Type（オリジンサーバーのタイプ）：セルフオリジンExternalを選択してください。
 - Origin Domain（オリジンサーバーのドメイン名）：COSのXML APIドメイン名または静的サイトのドメイン名を記入してください。
 - **Host header（プル型HOST）：オリジンサーバーのドメイン名と同じものを記入しなければなりません**。
![](https://main.qcloudimg.com/raw/691da49e660fb3a5675d371821e702d9.png)
その他のオプションにつき、実際の必要に応じて設定してください。その他の詳しい情報につき、GCDの[クイックスタート](https://cloud.tencent.com/document/product/673/14422)ドキュメントを参照してください。

### CNAMEの構成
DNSサービス業者より関連のCNAME記録を追加してください。構成方法につき、CDNの[CNAMEの構成](https://cloud.tencent.com/document/product/228/3121)ドキュメントを参照してください。

## FAQ
登録されていないドメイン名をGCDに接続できるかどうか等の問題につき、COSの[よくある質問](https://cloud.tencent.com/document/product/436/30737#.E5.B0.9A.E6.9C.AA.E5.A4.87.E6.A1.88.E7.9A.84.E5.9F.9F.E5.90.8D.E5.8F.AF.E4.BB.A5.E6.8E.A5.E5.85.A5.E6.B5.B7.E5.A4.96.E5.8A.A0.E9.80.9F-gcd-.E5.B9.B3.E5.8F.B0.E5.90.97.EF.BC.9F)ドキュメントを参照してください。
CDN加速の詳しい情報につき、GCDの[よくある質問](https://cloud.tencent.com/document/product/673/31673)ドキュメントを参照してください。
