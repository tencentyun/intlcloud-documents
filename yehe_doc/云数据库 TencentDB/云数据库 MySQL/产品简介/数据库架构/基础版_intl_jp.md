MySQLは、高可用性エディション、ファイナンスエディション、単一ノード高IOエディション、基本エディションの4つのアーキテクチャをサポートしています。このドキュメントは、基本エディションのアーキテクチャを紹介します。

基本エディションは単一ノードを使用して配置するものであり、安価でコスト・パフォーマンスが高い。

## ユースケース
基本エディションは個人学習、ミニWebサイト、非コアの小規模企業システム及び中規模から大規模の企業の開発テスト環境向けに設計されたものであり、正式なサービス環境では推奨されません。

## アーキテクチャ特徴
-計算とストレージを分離するようにします。計算ノードに障害が発生した場合には、ノードを交換することで迅速なリカバリを実現します。基盤となるデータはクラウドストレージのトリプル・コピーを使用して保存し、データの信頼性が確保されており、ディスクの障害は、ディスクのスナップショットモードで迅速に復旧できます。
- 基本エディションはデータベースへの接続、アクセス、リソースなど、様々な側面から20以上の監視項目を提供し、相応のアラームポリシーを設定することで、CVMの自社構築よりも手間がかからないと同時に、CVMと比較して40%のコスト削減を実現する価格優位性があります。基本エディションのノードはCVM上に配置されており、ユーザーが自ら構築することよりも優れたデータベースパフォーマンスを提供します。
- MySQL基本エディションの基盤となるストレージメディアは90%のI/Oシーンに適した高性能クラウドストレージを使用しており、優れた品質、安価、安定したパフォーマンスです。具体的なIOPS範囲の計算式：{min 1500 + 8 * ディスク容量、max 4500}。例えば、ディスク容量は50GBの場合、IOPS範囲は{min 1900、max 4500}となります。

## アーキテクチャの基本枠組み図
![Alt text](https://main.qcloudimg.com/raw/fc709a3c5b65fd750ebb3ccb86ed8408.png)

>! MySQL基本エディションは単一ノードアーキテクチャであるため、このノードに障害が発生した場合、リカバリの所要時間はCVMの障害回復よりもわずかに長いです（インスタンスの起動とデータのリカバリが含まれます）。高可用性を必要とするサービスでは、MySQLの高可用性エディションまたはファイナンスエディションのインスタンスを使用することをお勧めします。

