**Channel Management**インターフェースを開き、チャネル名をクリックしてチャネル詳細画面に進みます。チャネル詳細画面には、チャネルの情報、入力、出力、Alerts、Healthなどの詳細情報が表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/8dfb1c1aecc0cd21270d688b8acaf271.png)

## アラート
いずれかのチャネルのいずれかのパイプラインで問題または潜在的な問題が発生すると、StreamLiveはそのチャネルのアラームを生成します。**Set time**はアラームが発生した時間で、**Cleared time**はアラームが削除された時間です。同じアラーム記録に状態が更新されます。アラーム記録が**SET**状態の場合、Set time、Stateは赤で表示されます。アラーム記録が削除されると、状態が**CLEARED**になると同時に、上記の赤い表示は消えます。アラームは、問題が発生したパイプライン、アラームタイプおよび詳細情報を明確に記録します。データクエリーは過去5日間のみクエリーを実行でき、クエリー期間は24時間未満です。
![](https://qcloudimg.tencent-cloud.cn/raw/b4048bc6f2407aaffc13e26d0e6adbf4.png)
![](https://qcloudimg.tencent-cloud.cn/raw/ae75774f87c1cb2f7bb71fb1feedd766.png)

## 健康データのモニタリング
**Health**はユーザーに対し、チャネル入力（帯域幅・入力ビデオフレームレート・入力オーディオフレームレート）と出力（帯域幅）の情報および対応するグラフを提供して、現在のチャネルが正常に機能しているかどうか判断します。データクエリーは過去5日間のみクエリーを実行でき、クエリー期間は24時間未満です。
![](https://qcloudimg.tencent-cloud.cn/raw/29a6e05aa80db9bdc1fdc495dad041f1.png)
![](https://qcloudimg.tencent-cloud.cn/raw/858815c461e124c41e82da194e6f77a3.png)


