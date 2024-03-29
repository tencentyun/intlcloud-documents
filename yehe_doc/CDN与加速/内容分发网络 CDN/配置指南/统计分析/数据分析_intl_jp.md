クライアントがユーザー分布と使用状況を理解しやすいよう、アクセスログを利用してユーザーソースを分析し、データ分析ページで各種グラフの表示を提供します。

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のディレクトリで【統計分析】>【データ分析】をクリックし、データ分析ページに移動します。

- 照会できる最大時間間隔は31日で、履歴データは90日間保持されます。
- 照会できる最も古い履歴データは、この照会実行した日から3か月以内のデータです。

> !現時点では、ECDNドメイン名は独立IPアクセス数の照会とアクセスのユーザーエリア分布表示をサポートしていません。

## データの概要

指定したレポートディメンションに基づいて、さまざまなデータの概要を表示します。 
異なる課金方法で表示される概要データは、それぞれに異なります。
トラフィック課金時の表示：総トラフィック、平均トラフィックヒット率およびリクエスト数。
帯域幅課金時の表示：ピーク帯域幅、back-to-originのピーク帯域幅およびリクエスト数。 


## アクセスユーザーのエリア分布

指定したレポートの次元に基づいて、対応するエリアのトラフィック分布図を表示します。クライアントがビジネスユーザーの地理的分布を把握しやすいよう、ソースクライアントIPを介して訪問者が所在する省を特定し、マップとリストを表示します。中国本土では省ごとに集計し、中国本土以外ではエリアごとに集計します。


## トラフィック

指定したレポートディメンションに従って、対応するトラフィック曲線を表示します。課金トラフィックまたはback to originトラフィック曲線の表示を選択できます。


## 帯域幅

指定したレポートの次元に基づいて、対応するトラフィック曲線を表示します。帯域幅の課金またはback-to-origin帯域幅曲線の表示を選択でき、ピーク帯域幅曲線をサポートします。


### リクエスト数

指定したレポートディメンションに応じて、リクエスト数の曲線を表示します。


## エラーコード

指定したレポートディメンションに従って、対応するエラーコードの数と割合を表示します。


## TOP10 URL

指定したレポートの次元に基づいて、対応するTOP10のURLを表示し、使用量またはリクエスト数でランク付けすることを選択できます。


## TOP10項目

指定したレポートの次元に基づいて、対応するTOP10項目を表示します。

## TOP10ドメイン名

指定したレポートの次元に基づいて、対応するTOP10ドメイン名を表示します。

## 独立IPアクセス数

独立IPアクセス数は、指定の時間サイクルに従い、ログ内のアクセスソースクライアントIPを重複排除して計算されます。
時間間隔が1日以下である場合は、5分粒度の重複排除されたIP数曲線が提供されます。
ドメイン名の状況は、1日のDAUの重複を排除して計算され、マルチドメイン名/プロジェクト/アカウントの状況は、各ドメイン名のDAUの5分粒度に従って累積されます。
>! 過去30日間のデータの照会のみをサポートします。



## ユーザーのキャリア分布

クライアントがビジネスユーザーのキャリアを把握しやすいよう、ソースクライアントIPを介して訪問者のキャリアを識別し、円グラフ、リストを表示します。

