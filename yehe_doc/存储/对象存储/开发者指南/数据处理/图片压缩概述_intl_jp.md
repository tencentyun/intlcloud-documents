## 概要

画像圧縮とは、画像のストレージスペースを節約し、画像のアクセストラフィックを削減し、画像のアクセス速度を向上させるために、画質を変更せずに可能な限り画像サイズを縮小することを指します。

Cloud Object Storage (COS)は、[Cloud Infinite (Cloud Infinite、CI)](https://intl.cloud.tencent.com/document/product/1045/33422)に基づいて、さまざまな画像圧縮機能を開始しました。画像圧縮の目的を達成するために、独自のサービスシーンに応じてさまざまな圧縮方法を選択できます。現在サポートされている圧縮方法は次のとおりです：

- **WebP圧縮：**画像は、webp形式に変換できます。これは、jpg形式よりも圧縮率が高いです。同じ画質の場合、webp形式の画像サイズはjpg形式の画像サイズより25%以上小さく、マルチターミナルの使用シーンに適合させることができます。
- **HEIF圧縮：**画像は、圧縮率が非常に高いheif形式に変換できます。同じ画質の場合、画像サイズはjpg形式の画像よりも80%以上小さくなります。iOSシステムでは、heif画像をアルバムのデフォルト形式とし、Android PシステムはネイティブでHeifをサポートしています。
- **TPG圧縮：**画像は、tpg形式に画像を変換できます。これは、テンセントによりリリースされた動画をサポートする自社開発の画像形式です。現在、QQブラウザやQQスペースなどの製品は、デフォルトでtpg画像をサポートしています。同じ画質の場合、画像サイズはgif形式の画像よりも90%以上小さくなり、png画像よりも50%以上小さくなります。
- **AVIF圧縮：**画像は、avif形式に変換できます。avifはav1に基づく新しい画像形式です。2020年2月にNetflixによって最初に発表され、現在ChromeやFirefoxなどのブラウザをサポートしています。

>? 画像圧縮は有料サービスであり、Cloud Infiniteにより請求されます。詳細については、Cloud Infiniteの画像処理料金をご参照ください。
>

## ユースケース

画像圧縮機能は、PCやAppなどの多端末画像圧縮のニーズを満たし、eコマースやメディアなどのサービスシーンに適し、画像送信リンクとロード時間を効果的に削減し、帯域幅とトラフィックのコストを削減します。

圧縮機能が異なれば、既存の画像形式やブラウザ環境などとの互換性も異なります。次のテーブルをご参照ください。

| 機能      | サポートされている形式                                                     | サポートされているブラウザとシステム                                            | 互換性 | 圧縮効果 | 圧縮速度 |
| :-------- | :----------------------------------------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- |
| WebP圧縮 | jpg、png、bmp、gif、heif、tpg、avif形式の画像のwebp形式への変換をサポートします。| Edge、Firefox、Chrome、Safari、Android、iOS、WeChatなど、95%以上のブラウザやシステムをサポートします | 強い     | 一般     | 速い       |
| HEIF圧縮 | jpg、png、bmp、webp、avif形式の画像のheif形式への変換をサポートします。      | ブラウザで開くことをサポートしません。iOS11以降およびAndroid Pシステムでネイティブでサポートします      | 弱い     | 強い       | 速い       |
| TPG圧縮 | jpg、png、bmp、gif、heif、webp、avif形式の画像のtpg形式への変換をサポートします。| 特別なデコーダが必要です。QQブラウザなどのいくつかのブラウザでのみサポートします。                   | 弱い     | 強い       | 速い       |
| AVIF圧縮 | jpg、png、bmp、gif、heif、webp、tpg形式の画像のavif形式への変換をサポートします。| Firefox、Chrome、Androidなどのいくつかのブラウザやシステムをサポートします               | 弱     | 非常に強い     | 遅い       |


>? TPG画像を使用する場合、**画像ロード環境がTPGデコードをサポートしている**ことを確認する必要があります。Tencent Cloud Cloud Infiniteは、TPGデコーダが統合された[iOS](https://intl.cloud.tencent.com/document/product/1045/47707)、[Android](https://intl.cloud.tencent.com/document/product/1045/45575)、[Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip)端末SDKを提供しています。TPGにすばやくアクセスして使用するのに役立ちます。
>

## 利用方法

上記の圧縮機能は、基本的な画像処理の形式変換機能を介して使用できます。formatパラメータを指定の圧縮形式に設定すると、画像圧縮機能を使用できます。具体的なパラメータは次のとおりです：

| パラメータ名 | パラメータ説明                                   |
| :----- | :----------------------------------------- |
| webp   | 元の画像をwebp形式に変換して、画像圧縮効果を実現します。|
| heif   | 元の画像をheif形式に変換して、画像圧縮効果を実現します。|
| tpg    | 元の画像をtpg形式に変換して、画像圧縮効果を実現します。  |
| avif   | 元の画像をavif形式に変換して、画像圧縮効果を実現します。|

## 圧縮の例

png形式の元の画像をjpeg、webp、heif、tpg、avif形式に変換します。元の画像のURLは`https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png`であり、効果は次のとおりです：

![img](https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png)

### 例1：jpeg画像への変換

リクエストの最終URL：
```
https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png?imageMogr2/format/jpeg
```

### 例2：webp画像への変換

リクエストの最終URL：

```
https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png?imageMogr2/format/webp
```

### 例3：heif画像への変換

リクエストの最終URL：

```
https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png?imageMogr2/format/heif
```

### 例4：tpg画像への変換

リクエストの最終URL：

```
https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png?imageMogr2/format/tpg
```

### 例5：avif画像への変換

リクエストの最終URL：

```
https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png?imageMogr2/format/avif
```

次の表に、各画像の圧縮方法の圧縮率の比較を示します：

| 形式        | サイズ               |
| :---------- | :----------------- |
| png（元の画像） | 465 KB             |
| jpeg        | 114KB（75.5%減少） |
| webp        | 64 KB（86.2%減少） |
| heif        | 54 KB（88.4%減少） |
| tpg         | 56 KB（88.0%減少） |
| avif        | 32 KB（93.1%減少） |

