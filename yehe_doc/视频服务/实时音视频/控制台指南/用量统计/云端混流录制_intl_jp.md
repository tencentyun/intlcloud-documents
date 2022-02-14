TRTCコンソールの**クラウドミクスストリーミングの使用量統計**は、主にTRTCの提供する[MCU Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/38929)によって発生する使用量明細を表示するために使用されます。使用するのがCSSの提供する[クラウドミクスストリーミング機能](https://intl.cloud.tencent.com/document/product/267/37665)による課金の場合は、[CSSコンソール](https://console.cloud.tencent.com/live/analysis/bill?tab=record)で確認する必要があります。

## 注意事項
使用統計はリアルタイム更新ではありません。5分ごとに1回統計し、データの表示には5分～20分の遅れがあります。

## 操作手順
1. **TRTCコンソール**に入り、左側のバーの**使用量統計**>**[Cloud MixTranscoding](https://console.cloud.tencent.com/trtc/cloudmcu)**を選択します。
2. 確認したいアプリケーションを選択し、確認したい時間帯を選択します（時間課金モデルを例示します）。

![](https://qcloudimg.tencent-cloud.cn/raw/b2dd0bee1dfe92f965f9d58bcd89b12a.png)

## 詳細フロー

使用量の表示データは秒で計算し、分ごとに整数の値にして、1分未満は1分とします。このため、以下の各行に表示された使用量の分数をそのまま加算すると、実際に決算する分数とは若干の差異が生じます。最終的に課金される使用量は、[請求書センター](https://console.cloud.tencent.com/expense/bill/download) が出力した請求書を基準とします。
![](https://qcloudimg.tencent-cloud.cn/raw/41a6a97a88305ff6ca4a5ca56606d896.png)