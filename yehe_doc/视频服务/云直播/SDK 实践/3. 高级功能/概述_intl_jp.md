本書では、ご自分のプログラムにライブストリーミングの高度な機能を統合する方法を説明します。

## AV1フォーマットのビデオの再生
AV1はオープンかつロイヤリティフリーなビデオ圧縮規格であり、前世代のH.265[HEVC]規格に比べ、画質が同じである前提で、ビットレートを30%以上減らすことができます。つまり、同じ帯域幅でより良い画質で転送することができます。CSSではAV1規格がすでにサポートされていますが、AV1フォーマットのビデオを再生するには、プレイヤーにはAV1フォーマットのビデオをデコードする機能を持つ必要があります。
固有のプレイヤーでAV1デコードをサポートするように、以下の手順で実施してください：

### コンテナのフォーマットとデリバリープロトコル
AV1 in FLVについて、Tencent Cloudはプライベート化をめぐって拡張（in T-FFmpeg）を実装しているため、プレイヤーを改造する必要があります。ソースコードの方はT-FFmpegが提供する[Patchファイル](https://github.com/tencentyun/AV1/tree/main/patch)をベースにして拡張してよいです。詳しくは、[FLV拡張でAV1規格へ対応](https://github.com/tencentyun/AV1)をご参照ください。

### デコード
- **ハードウェアデコード**
PC系のAMD、Intel、Nvidiaの比較的新しいGPUでは、ほとんどAV1のハードウェアデコードがサポートされています。
AV1のハードウェアデコードをサポートしているデバイスは以下のとおりです：
<table>
<thead>
<tr>
<th>タイプ</th>
<th>ブランド</th>
<th>プロセッサー</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=23>携帯電話</td>
<td>realme X7 Pro</td><td>Dimensity1000+</td>
</tr><tr>
<td>oppo reno 5 pro</td><td>Dimensity1000+</td>
</tr><tr>
<td>HONOR V40</td><td>Dimensity1000+</td>
</tr><tr>
<td>Redmi k30 Ultra</td><td>Dimensity1000+</td>
</tr><tr>
<td>vivo iQOO Z1</td><td>Dimensity1000+</td>
</tr><tr>
<td>Redmi Note 10 Pro</td><td>Dimensity1000+</td>
</tr><tr>
<td>vivo S9</td><td>Dimensity1100</td>
</tr><tr>
<td>realme Q3 Pro</td><td>Dimensity1100</td>
</tr><tr>
<td>vivo s10</td><td>Dimensity1100</td>
</tr><tr>
<td>vivo s12</td><td>Dimensity1100</td>
</tr><tr>
<td>vivo s12 pro</td><td>Dimensity1200</td>
</tr><tr>
<td>OPPO Reno6 Pro</td><td>Dimensity1200</td>
</tr><tr>
<td>OPPO Reno7 Pro</td><td>Dimensity1200</td>
</tr><tr>
<td>Redmi K40 pro</td><td>Dimensity1200</td>
</tr><tr>
<td>realme GT Neo</td><td>Dimensity1200</td>
</tr><tr>
<td>HONOR X20</td><td>Dimensity1200</td>
</tr><tr>
<td>OnePlus Nord 2</td><td>Dimensity1200</td>
</tr><tr>
<td>realme GT Neo2</td><td>Dimensity1200</td>
</tr><tr>
<td>OPPO K9 Pro</td><td>Dimensity1200</td>
</tr><tr>
<td>OPPO Find X5 Pro Dimensity版</td><td>Dimensity9000</td>
</tr><tr>
<td>Redmi K50</td><td>Dimensity9000</td>
</tr><tr>
<td>Galaxy S21(Samsungチップ版）</td><td>Exynos 2100</td>
</tr><tr>
<td>Galaxy S22(Samsungチップ版）</td><td>Exynos 2200</td>
</tr><tr>
<td>テレビ</td><td>Samsung 新フラッグシップ 8K QLEDテレビ Q950TS</td><td>-</td>
</tr>
</tbody></table>

- **ソフトウェアデコード**
	- av1d（Tencentが最適化を行ったAV1デコーダーで、性能がdav1dより良く、外部にクローズドソースのライブラリを提供できます。統合方法については、[av1d統合説明](https://doc.weixin.qq.com/doc/w3_APEAMQbpAEs1nkQ8rfiR02j8K8srn?scode=AJEAIQdfAAo21jd3VvAPEAMQbpAEs&version=4.0.8.6617&platform=win)をご参照ください。T-FFmpegがFFmpeg分の統合Patchとav1dライブラリを提供しています
	- [dav1d](https://code.videolan.org/videolan/dav1d) 
	- libgav1
	- Android 10.0にAV1デコーダーが統合されています
	- Chrome系ではAV1デコードがサポートされています

### ブラウザの対応状況
Chrome系対応、iOS系未対応
![](https://qcloudimg.tencent-cloud.cn/raw/5e2045b9c9f721306675c3f812a52d04.png)
>! このデータは[AVI公式サイト](https://caniuse.com/?search=AV1)の2022年07月までの集計情報です。公式サイトで最新の集計情報を確認できます。

## メディア転送SDK (TMIO SDK)
TMIO SDKは、ストリームプロトコルSRT、QUICなどに向けてカプセル化して最適化を行うことで、安定したアップストリームプッシュを確保し、低遅延の転送、パケットドロップの低減、マルチリンク転送の最適化、タイムアウト時の再転送を実現し、プルデータソースの安定さを厳しく要求するシーンや遠距離転送シーン向けです。

### 機能説明
- 遠距離転送シーンと放送分野向けです。
- Android、iOS、Windows、MacOS、Linuxなど主流的なOSでサポートされています。

### 導入方法
SDKの導入方法については、[導入手順](https://www.tencentcloud.com/document/product/267/51158)をご参照ください。


## LEB転送レイヤーSDK
LEB転送レイヤーSDK (libLebConnection)はネイティブWebRTCエンハンス版をベースにした転送機能を提供します。ユーザは既存のプレイヤーを簡単に改造するだけで、LEBに迅速に導入できます。LVBのプッシュ、クラウド側のメディア処理機能と完全な互換性を持った上で、高並列低遅延のストリーミングを実装しています。これにより、ユーザは既存のLVBからスムーズにLEBに移行できます。さらに、既存のRTCシーンでコストの低いビッグルーム低遅延バイパスライブストリーミングを速やかに実装することもできます。

### 機能説明
- オーディオビデオプル。低遅延の性能と遅くて安定しないネットワーク対策機能を備えています。
- ビデオはH.264、H.265、AV1をサポートします。Bフレームをサポートします。ビデオ出力フォーマットはビデオフレームの生データです（H.264/H.265はAnnexB、AV1はOBU）。
- オーディオはAACとOPUSをサポートします。オーディオ出力フォーマットはオーディオフレームの生データです。
- Android、iOS、Windows、Linux、Macでサポートされています。

### 導入方法
SDKの導入方法については、[導入手順](https://www.tencentcloud.com/document/product/267/51159#.E6.8E.A5.E5.85.A5.E6.96.B9.E5.BC.8F)をご参照ください。

### 美顔エフェクト
ライブストリーミング中に美顔、フィルター、ステッカーなどの美顔エフェクト機能を使用するには、Tencent Effect SDKを導入してください。

### APPへの導入
[Tencent Effect SDK](https://www.tencentcloud.com/document/product/1143/45377)をダウンロードして統合します。具体的な導入方法は、ドキュメント（[iOS](https://www.tencentcloud.com/document/product/1143/45387) & [Android](https://www.tencentcloud.com/document/product/1143/45388)）をご参照ください。


### 詳細はこちら
[Tencent Effect SDK](https://www.tencentcloud.com/document/product/1143/45377)を使用する時、利用料金が発生します。詳しくは、[価格概要](https://www.tencentcloud.com/document/product/1143/45371)をご参照ください。