## 概要

画像処理は、画像ファイルに対してさまざまな処理を行うことができる[Cloud Infinite](https://www.tencentcloud.com/document/product/1045)（CI）の機能です。画像トリミング、形式変換、ズーム、ウォーターマーク付与などの基本処理機能、Guetzli圧縮、AVIFトランスコーディング圧縮などの画像スリム化機能、ブラインドウォーターマークによる著作権保護機能、画像エンハンスメント、画像タグ、画像スコア評価、画像修正、商品画像キーイングなどのAIベースの認識分析機能などがあり、さまざまな業務のシーンにおける画像処理のニーズに対応できます。

> !
> - 画像処理機能は、パブリッククラウドのリージョンでのみサポートされています。
> - 画像処理機能は課金項目で、Cloud Infiniteによって課金されます。詳細な課金方法については、Cloud Infiniteの[課金と価格](https://intl.cloud.tencent.com/document/product/1045/33431)をご参照ください。
> - 画像処理機能は現時点ではマルチAZバケットをサポートしていません。
>


<table>
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
   <tr>
      <td rowspan=11>画像AI認識サービス</td>
      <td>画像修正</td>
      <td>画像内のロゴ、物体、ウォーターマークなどの内容を除去し、背景に合わせてインテリジェントに補足することで、画像内の特定の部分を効果的に修正および再構成します。</td>
   </tr>
   <tr>
      <td>商品画像マッティング</td>
      <td>画像内の主体部分をインテリジェントに認識し、それ以外の背景を透明化します。</td>
   </tr>
   <tr>
      <td>ロゴ認識</td>
      <td>画像内の事業者のロゴを認識します。ロゴ名、画像内の位置などの情報を返すことができます。</td>
   </tr>
   <tr>
      <td>2次元コード認識</td>
      <td>画像内の2次元コードを認識し、2次元コードの位置およびそれに含まれる内容情報を返します。認識した2次元コードに対しモザイク処理を行うこともできます。</td>
   </tr>
   <tr>
      <td>画像タグ</td>
      <td>画像内のシーン、物などの情報、例えば動物（猫、犬、鳥類など）、グルメ（果物、野菜など）をインテリジェントに認識します。数十のカテゴリーと数千個のタグが含まれます。</td>
   </tr>
   <tr>
      <td>画像品質評価</td>
      <td>画像の視覚的な品質を多方面から評価し、客観的な解像度スコアと主観的な美観スコアを出力します。</td>
   </tr>
   <tr>
      <td>顔認識</td>
      <td>与えられた顔画像に対し、顔の位置、顔の属性、品質情報をチェックします。美顔、ポートレート分割、年齢性別変換などのエフェクト機能もサポートしています。</td>
   </tr>
   <tr>
      <td>FaceID</td>
      <td>身分証明書認識、顔の生体認証チェックなどの機能を提供します。</td>
   </tr>
   <tr>
      <td>自動車認識</td>
      <td>画像内の車両をチェックし、車両の車種、色、位置、ナンバープレートなどの情報を認識します。</td>
   </tr>
   <tr>
      <td>文字認識</td>
      <td>画像上の文字内容を、編集可能なテキストとしてインテリジェントに認識します。</td>
   </tr>
   <tr>
      <td>画像検索</td>
      <td>バケットに画像ライブラリを作成することで、同一または類似した内容の画像の集合を指定の画像ライブラリからスピーディーに検索することができます。</td>
   </tr>
   <tr>
      <td rowspan=1>その他の画像サービス</td>
      <td>異常画像検出</td>
      <td>TSビデオストリームなど、異常が疑われる情報を含む画像を検出できます。</td>
   </tr>
</table>



## 利用方法

#### COSコンソールの使用

COSコンソールを使用して画像の基本処理設定を行うことができます。詳細については、[基本画像処理コンソールガイド](https://intl.cloud.tencent.com/document/product/436/36569)をご参照ください。

#### REST APIの使用

COSの提供するAPIによって画像の基本処理またはAI認識処理を行うことができます。詳細については、[画像処理およびAIコンテンツ認識](https://www.tencentcloud.com/document/product/436/36364)のAPIドキュメントをご参照ください。

## 制限事項

- サポートする形式：JPG、BMP、GIF、PNG、WEBP形式の処理をサポートしています。また、HEIF形式のデコードおよび処理操作もサポートしています。
- ボリューム制限：処理する画像のオリジナル画像は、サイズが32MB以下、幅は30000ピクセル以下でなおかつ総画素数が2.5億ピクセル以下とします。処理結果画像の幅と高さは9999ピクセル以下に設定します。アニメーション画像については、オリジナル画像の幅 x 高さ x フレーム数が2.5億ピクセル以下であることとします。
- アニメーション画像のフレーム数制限：GIFフレーム数は300フレームまでです。
