## 概要

メディア処理はCloud Object Storage（COS）とは、Cloud Infiniteをベースにしてリリースした、マルチメディアファイル処理サービスです。オーディオビデオトランスコーディング、ビデオフレームキャプチャなどの基本的なオーディオビデオ処理サービスのほか、Tencent Cloudの先進的なAI技術を組み合わせた、インテリジェントカバーなどの高度な処理サービスを網羅しています。

| 機能           | 説明                                                        |
| -------------- | ------------------------------------------------------------ |
| オーディオビデオトランスコーディング     | オーディオ、ビデオなどのメディアファイルのトランスコード機能をご提供します。これは、ファイルのビットストリームを別のビットストリームに変換するプロセスです。トランスコードによって、コーデック、解像度、ビットレートなどの元のビットストリームのパラメータを変更して、様々なデバイスやネットワーク環境での再生に適合させます。|
| 高速高画質トランスコーディング   |  ビデオサイズをさらに小さくし、より鮮明にするトランスコード機能をご提供します。画質の修復とエンハンスメント、コンテンツアダプティブパラメータの選択、V265エンコーダなど一連のビデオ処理ソリューションを統合しています。ネットワークリソースの低消費を保証すると同時に、さらに優れた視覚体験をユーザーにもたらします。 |
| ブロードキャストグレードフォーマットのトランスコーディング | XAVC、ProResなどの特殊な形式のトランスコードをサポートしています。 |
| ハイライトコレクション       | ビデオのハイライト部分を正確に抽出し、ビデオの内容、モーション、シーンなどに対し、様々な次元で認識と集計を行うことで、ビデオのハイライトコレクションをプロの編集レベルでスピーディーにトリミングして生成します。  |
| ビデオエンハンスメント       | ディテールエンハンスメント、カラーエンハンスメント、SDR to HDRの変換などの一連の機能により、ビデオ画質を最適化し、視覚効果を向上させます。  |
| 超解像度      | ビデオコンテンツの認識と、ビデオのディテールおよび部分的な特徴の高画質輪郭再構成により、一連の低解像度画像から高解像度な画像が得られます。ビデオエンハンスメントと併用することで、古い映像をアップグレードすることができます。  |
| 関数のカスタマイズ処理  | ユーザーによる柔軟でスピーディーな業務のオーダーメイド化実現を支援します。開発期間を短縮でき、課金は必要な分だけとなり、低コストで効率がアップします。  |
| ビデオ暗号化       | HLS標準暗号化方式でビデオデータを暗号化し、ビデオのセキュリティを保障します。  |
| ビデオタグ       | ビデオタグはビデオのビジョン、シーン、行動、物体などの情報を分析し、マルチモーダルな情報融合とアライメント技術を組み合わせることで、高精度なコンテンツ認識を実現します。ビデオのマルチディメンショナルなコンテンツタグを自動的に出力します。  |
| 音声合成       | 音声合成は、先進的なディープラーニング技術によって、テキストを自然で流暢な音声に変換する機能です。複数の音声の種類を選択可能です。  |
| 人の声の分離       | 指定したビデオ（またはオーディオ）の中の人の声と背景音を分離し、独立したオーディオ素材を生成します。その後に他のスタイルに加工する際に便利です。   |
| HLSアダプティブパッケージ  |  単一のソースビデオからマルチビットレートのアダプティブファイルをワンステップで生成する機能をご提供し、ビデオを様々な再生端末およびネットワークに適合できるようにします。|
| HDR to SDR変換 | 変換後のビデオ画面のディテールを元のビデオに最大限近づけ、様々な種類の端末デバイスに適合できるようにし、画面にひずみや不鮮明さが生じないようにします。     |
| ビデオフレームキャプチャ       | ビデオのあるタイムノードに対しスクリーンキャプチャを行う機能をご提供します。フレームキャプチャ開始時点、フレームキャプチャ間隔、フレームキャプチャ数、出力画像サイズ、出力形式などをカスタム設定でき、フレームキャプチャの多様なニーズを満たします。 |
| オーディオビデオスプライシング     | 指定したビデオ（またはオーディオ）のセグメントを切り取ってビデオ（またはオーディオ）ファイルの先頭または末尾に結合し、新しいビデオ（またはオーディオ）ファイルを生成することができます。 |
| オーディオビデオセグメンテーション     | 指定したビデオ（またはオーディオ）をいくつかのセグメントに分割することができます。 |
| ビデオのアニメーション画像生成     | ビデオ形式のファイルをアニメーション形式のファイルに変換できます。ビデオの指定時間帯の変換、ビデオフレーム抽出方式、アニメーションフレームレートの出力、アニメーションサイズ、アニメーション形式などを選択でき、様々なシーンでのアニメーション化のニーズを満たします。 |
| インテリジェントカバー       | Tencent Cloudの先進的なAI技術を統合することで、ビデオの内容を理解し、ビデオフレームの品質、重要度、内容の関連度をインテリジェントに分析し、最適なフレームを抽出してスクリーンキャプチャを生成し、それをカバーにすることでコンテンツの魅力を高めます。 |
| ビデオメタ情報の取得 | COSに保存されたビデオ、オーディオ、字幕などのメディアファイルについて、例えばビデオファイルのコーデック形式、コーデック名、ピクセル形式、ビデオ時間、ビットレート、フレームレート、幅と高さなど、オーディオファイルのビットレート、サンプリング形式、サンプルレート、チャネル数、長さなどの関連のメタ情報を取得できます。また、字幕の言語の種類を同時に取得し、必要な各種メディア情報を得ることができます。 |



## 適用ケース

#### 複数端末への適合

コンテンツプラットフォームは通常、複数の端末を使用します。このため、様々なユーザーの様々な端末に合わせて異なる形式のメディアファイルを提供する必要があります。オーディオビデオトランスコーディング機能は大部分のオーディオビデオトランスコードのニーズをカバーできるほか、多様な圧縮機能によって圧縮率を向上させ、ファイルボリュームを小さくすることで、ラグを減らしてストレージスペースおよびトラフィック料金を節約することもできます。

#### ビデオプラットフォーム

従来のビデオプラットフォームはビデオカバーを作成する際、手動でビデオを閲覧してフィルタリングする必要があり、多くの人手を費やすため、ビデオのリリースまでに時間がかかります。

インテリジェントカバー機能は最も重要な画面をスピーディーに選んでカバーを作成できるため、人的資源を節約し、新規ビデオのリリース速度を向上させることができます。

ビデオのアニメーション画像生成機能は、ビデオの中のハイライト部分を選択してアニメーション化し、ビデオプレビューとすることが可能です。ユーザーはビデオ全体を再生しなくても、ビデオのハイライト部分を知ることができます。従来の静的なビデオカバーと異なり、アニメーションカバーはユーザーのクリック率を向上させ、ビデオの再生回数を増やすことにつながります。

## 使用方法

メディア処理機能はタスクまたはワークフロー方式で利用できます。効率アップと、ユーザーの操作の繰り返しを減らすため、オーディオビデオトランスコーディング、オーディオビデオスプライシング、ビデオフレームキャプチャ、ビデオのアニメーション画像生成機能については、[タスク](https://intl.cloud.tencent.com/document/product/436/46409)または[ワークフロー](https://intl.cloud.tencent.com/document/product/436/46408)を作成する際に、使用するテンプレートを指定することができます。テンプレートページでは、[システムプリセットテンプレート](https://intl.cloud.tencent.com/document/product/436/46411)、およびご自身の業務ニーズに応じてカスタマイズできる[カスタムテンプレート](https://intl.cloud.tencent.com/document/product/436/46411)をご提供しています。

### タスク

COSに保存されている既存データについては、タスク方式でメディア処理タスクを作成することができます。

#### タスクの管理

- コンソール方式：COSコンソールを使用して、タスクをビジュアル的に作成することができます。使用の詳細については、[タスクの作成](https://intl.cloud.tencent.com/document/product/436/46409)をご参照ください。
- API方式：APIインターフェースを使用して、メディア処理タスクを作成、削除、照会、検索することができます。使用の詳細については、[APIドキュメント](https://www.tencentcloud.com/document/product/436/49192)をご参照ください。

### ワークフロー

メディアワークフローを設定することで、オーディオビデオ処理フローを必要に応じてスピーディーかつフレキシブルに構築することができます。各ワークフローを、バケットに入力するパスにバインドし、ファイルがそのパスに**アップロード**されると、そのメディアワークフローが**自動的にトリガー**され、指定された処理操作が実行され、処理結果が出力バケットの指定されたパスに自動的に保存されます。ワークフローには**オーディオビデオスプライシング**タスク、**オーディオビデオトランスコーディング**タスク、**ビデオフレームキャプチャ**タスク、**ビデオのアニメーション画像生成**タスク、**インテリジェントカバー**タスクを設定できます。

#### ワークフローの管理

- コンソール方式：COSコンソールを使用して、ワークフローをビジュアル的に作成することができます。使用の詳細については、[ワークフローの設定](https://intl.cloud.tencent.com/document/product/436/46408)をご参照ください。
- API方式：APIインターフェースを使用して、メディア処理ワークフローを作成、削除、照会、検索することができます。使用の詳細については、APIドキュメントをご参照ください。

