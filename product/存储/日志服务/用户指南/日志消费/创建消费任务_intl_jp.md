
## 概要
CLSはCkafkaインスタンスを通してログトピックのデータを消費できます。ログトピックCkafka消費機能を有効にする方法の詳細な説明はここにあります。

## 前提条件

Tencent Cloudメッセージキュー（CKafka）が開かれ、Ckafka消費インスタンスとメッセージキュートピックがログトピックの同じ地域の下に作成されます。

>?Ckafkaインスタンスの作成については、[Ckafkaインスタンスの作成](https://cloud.tencent.com/document/product/597/30931)を参照してください。Ckafkaの使い方については、[Ckafkaの使い方](https://cloud.tencent.com/document/product/597/10112)を参照してください。

## 操作手順

1.[CLSコンソール](https://console.cloud.tencent.com/cls)にログインしてください。  
2.左側のナビゲーションバーで【ログセット管理】をクリックします。  
3.Ckafka消費を構成する必要があるログセットID/名称をクリックして、ログセットの詳細ページに進みます。  
4.消費するログトピックを見つけ、右側の【構成の管理】>【リアルタイム消費】をクリックして、Ckafka消費構成ページに入ります。
![1](https://main.qcloudimg.com/raw/85294af3a9d71265e5cc535b17a58057.png)
5.ページの右側にある【編集】をクリックして、Ckafkaの消費構成ページに入ります。
6.Ckafka消費スイッチをオンにして、消費するCkafkaインスタンスと対応するメッセージキューtopicを選択します。
![2](https://main.qcloudimg.com/raw/ebfac8224553db1011d0d14a3a812cb3.png)
7.【保存】をクリックして、Ckafkaの消費を開始します。Ckafkaの消費状況が「有効」と表示されていれば、起動は成功です。
![](https://main.qcloudimg.com/raw/1ac6ee333d54e068451a68fbcf71af18.png)
