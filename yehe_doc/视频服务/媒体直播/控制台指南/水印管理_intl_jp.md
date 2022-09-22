ウォーターマーク機能とは、StreamLiveのビデオ出力に静的画像またはテキストを重ねることを指します。その中で、静的画像は静止画像を指し、PNGまたはJPG形式のみです。

## ウォーターマークの確認
左側のナビゲーションバーで**Watermark Management**をクリックして、ウォーターマーク画像のプレビュー、ウォーターマークテキストの表示、画像のサイズ、幅や高さなどの情報を含む、作成されたウォーターマークリストをページに表示できます。
![](https://qcloudimg.tencent-cloud.cn/raw/0cd3973c8d34202dff84257a9ae3eddc.png)

## ウォーターマークの追加
新しいウォーターマークを追加する必要がある場合は、**Watermark Management**ページで**Create Template**ボタンをクリックし、追加ページで設定します。
![](https://qcloudimg.tencent-cloud.cn/raw/a919f169397bef249904ae88c3a08b23.png)
共通設定：

- **Template Name**：ウォーターマークテンプレート名です。入力文字は数字、大文字と小文字、およびアンダーバーで、長さは16文字に制限されています。
- **Watermark Type**：ウォーターマークのタイプです。ドロップダウン リストからText WatermarkテキストウォーターマークまたはImage Watermark静的画像ウォーターマークを選択できます。
- **Origin**：ウォーターマークの元の位置です。ドロップダウン リストからTop Left（左上）、Bottom Left（左下）、Top Right（右上）、Bottom Right（右下）をそれぞれ選択できます。
- **Vertical Offset**：元の位置からの垂直オフセットです。
- **Horizontal Offset**：元の位置からの水平オフセットです。

### テキストウォーターマークの追加
- **Watermark Text**：ビデオに重ねるテキストです。テキストウォーターマークを追加するためには必須です。
- **Front Size**：フォントサイズです。
- **Coloer**：フォントの色です。
![](https://qcloudimg.tencent-cloud.cn/raw/41770c54a01cb9b2eebeaf48c266a981.png)
入力後、**Confirm**ボタンをクリックして作成を完了します。

### 画像ウォーターマークの追加
- **Watermark Image**：**Click to upload**をクリックして画像をアップロードするか、マークされた領域に画像を直接ドラッグできます。画像ウォーターマークを追加するには必須です。
- **Watermark Size**：ビデオ出力に対するウォーターマーク画像のスケーリング比です。入力なしまたは入力した0は、スケーリングせずにウォーターマーク画像の元のサイズを維持することを意味します。
![](https://qcloudimg.tencent-cloud.cn/raw/0bc5a62b8fbe88edca116802414ae9be.png)
入力後、**Confirm**ボタンをクリックして作成を完了します。

## ウォーターマークの検索
ウォーターマークリストページの右上隅にある入力ボックスに、ウォーターマークテンプレート名またはウォーターマークIDを入力します。
![](https://qcloudimg.tencent-cloud.cn/raw/17bba7c53601f53fb2daa46d227146b5.png)

## ウォーターマークの編集
ウォーターマークリストから編集するウォーターマークを選択し、**Operation**の**Edit**ボタンをクリックして、ウォーターマークの設定を再編集できます。注：ウォーターマークのタイプは修正できません。
![](https://qcloudimg.tencent-cloud.cn/raw/e9485a741dc02eb763022d34e111a2d3.png)

## ウォーターマークの削除
ウォーターマークリストから削除するウォーターマークを選択し、**Operation**の**Delete**ボタンをクリックして、ウォーターマークを削除できます。
![](https://qcloudimg.tencent-cloud.cn/raw/6770bdf42d44e9f2b01d4b880c4ebdca.png)
ウォーターマークがチャネルで既に使用されている場合は、削除できません。**Template Binding**は、バインディングされたチャネルの数を表示します。
![](https://qcloudimg.tencent-cloud.cn/raw/f5cbff44d5f19a16a721e7d9d5d49933.png)

## ウォーターマークのチャネルへのバインディング
ウォーターマークテンプレートの作成後、チャネル管理ページで指定したチャネルにウォーターマークテンプレートをバインディングできます。設定方法：ウォーターマークを設定する必要があるチャネルを選択し、**Output Group Setting**で**Video Watermark**スイッチをオンにし、**Video Watermark Template**から既に作成したウォーターマークテンプレートを選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/00b231219d0e51cfb4004c018a64ff15.jpg)

>!  設定変更は次回のライブストリーミングの際に有効になります。




