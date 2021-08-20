VOD [ウォーターマーク](https://intl.cloud.tencent.com/document/product/266/33939) が提供する画像ウォーターマークと文字ウォーターマークは簡単なウォーターマークの要件を実現できますが、複雑なウォーターマークの要件（例えば、画像と文字が混在するウォーターマーク、フィルター等）については、対応する難度は高くなります。このため、VODがSVG(Scalable Vector Graphics)ウォーターマークを導入することで使用者はウォーターマークコンテンツを便利かつ柔軟にカスタマイズでき、画像や文字コンテンツを自由に配置し、画像作成、フィルターの追加、グラデーション等の特殊効果に対応することができます。

## SVGの紹介
- [SVG](https://developer.mozilla.org/zh-CN/docs/Web/SVG)(Scalable Vector Graphics) はXMLをベースにしたマークアップ言語です。2次元ベクトル画像を記述するために用いられるオープンネットワーク標準で、CSS、DOM、JavaScript等の各種ネットワーク標準に広く応用されています。
- VODはSVGの幅と高さに制限がないだけでなく、完全な要素を含むことができる最小の矩形を自動計算し、これをSVGウォーターマークの元のサイズ（幅と高さ）とします。例：最小の矩形を計算して下図の点線で囲まれた部分を取得します。
![](https://main.qcloudimg.com/raw/539c2ca84d5ff2f6738b03c086bf7c2a.png)
<span id="editor"></span>
>?
>- オンライン上には多くのWebベースの無料のSVGオンラインデバッグツールがあり、お客様はこのツールを使用して満足のいく図形を作成し、完成後XMLにエクスポートすることができます。
>- 詳細な設定（要素の整列属性、フォントサイズ等）については、手動でXMLを変更できます。最終的な効果を確認してXMLコードを取得します。

## SVGウォーターマークの使用フロー
### 手順1：SVGウォーターマーク効果のデバッグ
1. SVGデバッグツールを使用して（簡単な[オンラインHTML WYSIWYG編集ツール](https://www.w3schools.com/graphics/tryit.asp?filename=trysvg_myfirst)、またはより豊富な[オンラインSVGエディタ](https://c.runoob.com/more/svgeditor/)を操作して）、お気に入りの図形をデバッグし、WYSIWYG全行程を操作します。完了後、SVGを`.html` 拡張子ファイルで保存すると、ブラウザを開いて効果を表示することができます。
>?異なる要素間で整列の要件がある場合、各要素の整列クラス属性を柔軟に活用し、要素の内容を変更して有効かどうか検証することをお勧めします（例：画像と文字を混在させて、テキストの長さを増減し、画像とテキストが常に整列の要件を満たしていることを確認する）。完全なチュートリアルは以下をご参照ください。[SVGチュートリアル](https://www.runoob.com/svg/svg-tutorial.html)。具体的な事例はテキスト下の[事例](#example)を参照することができます。

### 手順2：SVGウォーターマークテンプレートの作成

[ウォーターマークテンプレートの作成] (https://intl.cloud.tencent.com/document/product/266/34163)インターフェースを呼び出し、ウォーターマーク位置、幅と高さ等の情報を指定します。作成完了後、ウォーターマークテンプレートIDを取得します。

### 手順3：SVGビデオウォーターマークの追加

ビデオ処理タスクの開始、およびタスク結果を取得する方法については、[ビデオ処理タスクシステム](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。
[ビデオ処理](https://intl.cloud.tencent.com/document/product/266/34125)インターフェースで説明します。[事例2 ウォーターマーク付きのトランスコードタスクの開始](https://intl.cloud.tencent.com/document/product/266/34125#.E7.A4.BA.E4.BE.8B2-.E5.8F.91.E8.B5.B7.E5.B8.A6.E6.B0.B4.E5.8D.B0.E7.9A.84.E8.BD.AC.E7.A0.81.E4.BB.BB.E5.8A.A1)で、`WatermarkSet.N.Definition` は手順2で取得したテンプレートIDを使用します。また、SVGウォーターマークを使用しているため、手順1で取得したXMLをパラメータ `WatermarkSet.N.SvgContent`に渡す必要があります。
<span id="example"></span>
## 事例
以下では、具体的な事例を挙げ複雑なウォーターマークの追加方法をご紹介します。可変テキストの文字と画像が混在するウォーターマークを実現します。

### 要件の説明
特定の顧客はビデオにウォーターマークを追加する必要があります。要件は以下のとおりです。
- ウォーターマークはブランドLogoとログインユーザーのアカウントID（テキスト）で構成されます。
- ウォーターマークをビデオの右上隅に設定し、ビデオの右枠線からの[ウォーターマーク始点](https://intl.cloud.tencent.com/document/product/266/34163)のオフセットサイズはビデオ幅の2%、ビデオの上部枠線からのオフセットサイズはビデオの高さの5%とします。
- ウォーターマークの幅はビデオの短辺の30%、高さは元の図などの比例に応じて拡大縮小します。
- 文字はブランドLogoを上詰め右側に揃えます。
- 文字フォントはゴシック体、背景色は白、ガウシアンぼかしの影、影の色を黒に設定します。ブランドLogoを拡大縮小しない場合の文字サイズは50ピクセルです。

### 手順1：SVGウォーターマーク効果のデバッグ
SVGのXMLソースコードは以下のとおりです。

```xml
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="1000px" height="1000px">
    <defs>
        <filter id="filter" x="0" y="0">
            <feGaussianBlur stdDeviation="2"/>
            <feOffset dx="0" dy="3"/>
        </filter>
    </defs>

    <image id="img_watermark"  xlink:href="data:image/png;base64,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"
        x="74.4%" y="0px" height="185px" width="256px"/>
    <text id="text_watermark_shadow" text-anchor="end" font-family="SimHei" font-style="Regular" font-size="50px"
        x="100%" y="245px" style="opacity:1;" fill="black" filter="url(#filter)">@Tencent</text>
    <text id="text_watermark" text-anchor="end" font-family="SimHei" font-style="Regular" font-size="50px"
        x="100%" y="245px" fill="white">@Tencent</text>
</svg>
```

効果の検証：
- 方式1：上記のコードを[オンラインHTML WYSIWYG編集ツール](https://www.w3schools.com/graphics/tryit.asp?filename=trysvg_myfirst) ページ左側のテキスト入力ボックスにコピーし、ページ上の**Run**ボタンをクリックすると、以下のとおり、効果がページ右側に作成されます。
![](https://main.qcloudimg.com/raw/3a2d9e5234339fe78e39670d0b5db9e3.png)
- 方式2：上記のコードを `.html` 拡張子のファイルに保存し、ブラウザで開くと、図2：白背景のウォーターマーク効果を確認できます。

| 図1：透明背景| 図2：白背景 | 図3：黒背景 | 
|---------|---------|---------|
|![](https://main.qcloudimg.com/raw/703d7f9818c4cecb9eb3cb8733835312.png)|   ![](https://main.qcloudimg.com/raw/c96e49aec06dd4d5795788b50e86c65d.png)           |![](https://main.qcloudimg.com/raw/e3ac33c3bb998ddcfc6343681ee8c06d.png)|


#### SVGの説明

| パラメータ | 説明 |属性|
|---------|---------|---------|
| `<svg>`|SVGキャンバスの定義。 | width="1000px" height="1000px"`：幅と高さはそれぞれ1000px。ここではSVG内に要素を完全に含むことができればOK。|
|`<filter id="filter">`|使用するフィルターの定義。|-|
|`<feGaussianBlur>`|ガウシアンぼかしフィルター。|`stdDeviation="2"`|
|`<feOffset>`|フィルター要素のオフセット。|`dx="0" dy="3"`：フィルター要素を「下方向」へ3ピクセルオフセットするよう設定。|
|`<image id="img_watermark">`|ブランドLogo画像。|<li>`xlink:href="data:image/png;base64,{画像データのbase64}"`：ローカル画像を参照。</li><li>`height="185px" width="256px"`：元の画像の幅と高さ。</li><li>`x="74.4%" y="0px"`：必要に応じて画像は上部にあるため、y軸のオフセットは0pxに設定し、`x`値を連続的に***调整***して効果を確認することで、最終的に`x="74.4%"`が期待どおりであることを確認。</li>|
|`<text id="text_watermark_shadow">`|文字のシャドウ効果の実現。|<li>`font-family="SimHei" font-style="Regular" font-size="50px"`：文字のフォントとサイズを設定。</li><li>`text-anchor="end"`：文字の整列方法を設定。テキストの文字列の末尾は現在のテキストの初期位置。</li><li>`x="100%"`：x軸に沿って要素を「右端」にオフセットするよう設定。ブランドLogoの位置（タグ`<image id="img_watermark">`の `x` 属性）を調整するため、`text-anchor`、`x`属性の設定により、テキストの最後の文字をSVGキャンバス「右端」に「固定」。</li><li>`style="opacity:1;"`：透明度を不透明に設定。</li><li>`fill="black"`：塗りつぶし色を黒に設定。</li><li>`filter="url(#filter)`： `id`をフィルターのfilterとして使用。</li><li>`y="245px"`：要素のy軸オフセットサイズを設定。ブランドLogoの高さが185ピクセルの場合、文字サイズは50ピクセル（文字サイズは高さと近似）のため、`y`を`185+50=235`以上に設定し、 ***调整*** を使用して245の効果が適切であると判断。</li>|
|`<text id="text_watermark">`|文字。|属性を`<text id="text_watermark_shadow">`と比較し、大部分の属性は同じ。違いはフィルターの未使用（`filter`属性がない）、かつ文字色が白（属性`fill="white"`）であること。|

- 最終的に効果を検証する際、テキストの長さ（SVG `<text>`タグの内容）の増減により、効果が要件を満たしているか確認することをお勧めします。例：`@Tencent`を`@Tencentは善良な人です`に置き換えます。
- 使用の際、異なるユーザーIDについては、SVG `<text>`タグの内容を置き換えるだけでOKです。

### 手順2：SVGウォーターマークテンプレートの作成
```http
https://vod.tencentcloudapi.com/?Action=CreateWatermarkTemplate
&Type=svg
&Name=テスト
&CoordinateOrigin=TopRight
&XPos=2%
&YPos=5%
&SvgTemplate.Width=30S%
&SvgTemplate.Height=0px
&<パブリックリクエストパラメータ>
```

パラメータの説明：

| パラメータ | 説明 |
|---------|---------|
| Type=svg | 作成するウォーターマークテンプレートのタイプはSVGです。|
|Name=テスト|テンプレートの名称。非入力必須パラメータ。|
|CoordinateOrigin=TopRight|ウォーターマークはビデオ右上隅に設定。|
|XPos=2%|ビデオの右枠線からの[ウォーターマーク始点](https://intl.cloud.tencent.com/document/product/266/34163)のオフセットサイズはビデオ幅の2%です。|
|XPos=5%|ビデオの上部枠線からの[ウォーターマーク始点](https://intl.cloud.tencent.com/document/product/266/34163)のオフセットサイズはビデオの高さの5%です。|
|SvgTemplate.Width=30S%|ウォーターマーク幅はビデオの短辺の30%です。|
|SvgTemplate.Height=0px|ウォーターマークの高さは元の図などの比例に応じて拡大縮小します。|

作成後、SVGウォーターマークテンプレートIDは12345と仮定します。

### 手順3：SVGビデオウォーターマークの追加
ビデオ処理の開始：
```http
https://vod.tencentcloudapi.com/?Action=ProcessMedia
&FileId=5285485487985271487
&MediaProcessTask.TranscodeTaskSet.0.Definition=30
&MediaProcessTask.TranscodeTaskSet.0.WatermarkSet.0.Definition=12345
&MediaProcessTask.TranscodeTaskSet.0.WatermarkSet.0.SvgContent={手順1のXML}
&<パブリックリクエストパラメータ>
```

### ビデオにウォーターマーク効果を追加する
![](https://main.qcloudimg.com/raw/a9ed65074f61b99324b55ccc86c4e659.gif)


## 付録

### 対応するフォントリスト

- SimHei,ゴシック体:style=Regular
- Roboto:style=Bold

その他フォントをご要望の際は、[テクニカルサポート](https://intl.cloud.tencent.com/document/product/266/19905)までお問い合わせください。
