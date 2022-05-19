## 概要

Tencent Cloud COSは[Cloud Infinite](https://intl.cloud.tencent.com/document/product/1045)（CI）のプロフェッショナルな一体化マルチメディアソリューションを統合し、画像の処理、審査、認識などの機能をすべてカバーします。詳細については下表のとおりです。COSのアップロードおよび処理インターフェースを通じてメディアデータの処理操作を行うことができます。

> !
> - 画像処理機能は、パブリッククラウドのリージョンでのみサポートされています。
> - 画像処理機能は課金項目で、Cloud Infiniteによって課金されます。詳細な課金方法については、Cloud Infiniteの[課金と価格](https://intl.cloud.tencent.com/document/product/1045/33431)をご参照ください。



<table>
   <tr>
      <th>サービス</td>
      <th>機能</td>
      <th>説明</td>
   </tr>
   <tr>
      <td rowspan=12>基本画像処理サービス</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">缩放</a></td>
      <td>等倍ズーム、幅および高さ指定ズームなどの複数の方式</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">裁剪</a></td>
      <td>通常トリミング、ズームトリミング、内接円、スマートトリミング</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">旋转</a></td>
      <td>自動回転、通常回転</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">フォーマット変換</a></td>
      <td>フォーマット変換、GIFフォーマット最適化、プログレッシブ表示</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">质量变换</a></td>
      <td>JPGおよびWEBP画像に対し画質変換を行います</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">ガウシアンぼかし</a></td>
      <td>画像のぼかし処理を行います</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">锐化</a></td>
      <td>画像のエッジ強調処理を行います</td>
   </tr>
   <tr>
      <td>ウォーターマーク追加</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">画像ウォーターマーク</a>、<a href="https://intl.cloud.tencent.com/document/product/436/36374">テキストウォーターマーク</a></td>
   </tr>
   <tr>
      <td>画像情報の取得</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">基本情報</a>、<a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF情報</a>、<a href="https://intl.cloud.tencent.com/document/product/436/36377">メインカラートーン</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">メタ情報除去</a></td>
      <td>EXIF情報を含む</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">クイックサムネイルテンプレート</a></td>
      <td>画像フォーマット変換、サムネイル化、トリミングなどの機能をクイック実装し、サムネイルを生成します</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33443">スタイル設定</a></td>
      <td>画像のスタイルを設定します。異なるニーズに合わせた画像の管理に役立ちます</td>
   </tr>
</table>



## 利用方法

#### COSコンソールの使用

COSコンソールを使用して画像処理設定を行うことができます。詳細については、[画像処理の有効化](https://intl.cloud.tencent.com/document/product/436/36569)をご参照ください。

#### REST APIの使用

COSの提供するAPIによって画像処理設定を行うことができます。詳細については、[基本的な画像処理](https://intl.cloud.tencent.com/document/product/436/36365)のAPIドキュメントをご参照ください。

## 制限事項

- サポートする形式：現時点でJPG、BMP、GIF、PNG、WEBP形式の処理をサポートしています。また、HEIF形式のデコードおよび処理もサポートしています。
- ボリューム制限：処理する画像のオリジナル画像は、サイズが20MB以下、幅は30000ピクセル以下でなおかつ総画素数が2.5億ピクセル以下とします。処理結果画像の幅と高さは9999ピクセル以下に設定します。アニメーション画像については、オリジナル画像の幅 x 高さ x フレーム数が2.5億ピクセル以下であることとします。
- アニメーション画像のフレーム数制限：GIFフレーム数は300フレームまでとします。

