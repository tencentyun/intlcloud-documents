1. [VODコンソール](https://console.cloud.tencent.com/vod)にログインして、左側ナビゲーションバーの**アプリケーション管理**をクリックして、アプリケーションリストページへ進みます。
2. タスクを管理したいアプリケーションを見つけ、アプリケーション名をクリックし、アプリケーション管理ページに進みます。
3. デフォルトでは、**メディア情報管理**>**オーディオビデオ管理**、「アップロード済み」ページへ進みます。
4. 左側のナビゲーションバーで、**ビデオ処理設定**>**テンプレート設定**を選択します。テンプレート設定に組み込まれているテンプレートは、**ビデオトランスコーディングテンプレート**、**超高速HDテンプレート**、**オーディオトランスコーディングテンプレート**、**再カプセル化テンプレート**、**アダプティブストリームトランスコーディングテンプレート**、**ウォーターマークテンプレート**、**スクリーンショットテンプレート**、**アニメーション画像生成テンプレート**、および**ビデオ審査テンプレート**です。各テンプレートは、ビデオの処理設定用にタスクフロー設定に追加できます。


## ビデオトランスコードテンプレート

業務のニーズに応じて新しいビデオトランスコードテンプレートを作成し、カスタマイズ設定を行うことができます。**ビデオトランスコーディングテンプレート**を選択してから、**トランスコーディングテンプレートを作成する**をクリックして、テンプレートのカスタマイズ設定に進みます。
+ テンプレート名：中国語、英語、数字、スペース、アンダーバー(_)、ハイフン(-)、ピリオド(.)の7種類の形式のみサポートし、64文字を超える長さは対応していません
+ コンテナ形式：MP4、FLV、HLS
+ 設定項目：ビデオパラメータ、オーディオパラメータ
+ ビデオパラメータ：
	+ コーデック：H.264、H.265
	+ ビデオビットレート：128kbps～35000kbps
	+ 解像度：ビデオの長辺（ビデオ幅）およびビデオの短辺（ビデオ高さ）は128px～4096px
	+ フレームレート：1～100fps
+ オーディオパラメータ：
	+ コーデック：AAC、MP3
	+ サンプルレート：32000Hz、44100Hz、48000Hzの3種類のデフォルトのサンプルレート
	+ オーディオビットレート：26kbps～256kbps
	+ サウンドチャンネル：シングルサウンドチャンネル、ダブルサウンドチャンネル
+ 共通テンプレート：共通テンプレートに設定するかどうかを指定

作成したテンプレートはテンプレートリストに表示され、共通テンプレートに設定できます。また、テンプレートの表示、編集、削除などの管理操作を行うことができます。

#### プリセットのパラメータテンプレートリスト
詳細パラメータは[プリセットのパラメータテンプレートリスト-プリセットのトランスコードテンプレート](https://intl.cloud.tencent.com/document/product/266/33932#preset-transcoding-templates)をご参照ください。

## TESHDテンプレート

業務のニーズに応じて、新しいクイック高画質テンプレートを作成し、カスタマイズ設定を行うことができます。**超高速HDテンプレート**を選択してから、**トランスコーディングテンプレートを作成する**をクリックして、テンプレートのカスタマイズ設定に進みます。
+ テンプレート名：中国語、英語、数字、スペース、アンダーバー(_)、ハイフン(-)、ピリオド(.)の7種類の形式のみサポートし、64文字を超える長さは対応していません
+ コンテナ形式：MP4
+ 設定項目：ビデオパラメータ、オーディオパラメータ
+ ビデオパラメータ：
	+ コーデック：H.264
	+ 平均ビットレート上限：入力なしまたは0を入力したものはビデオビットレートの上限を設けていないことを示します
	+ 解像度：ビデオの長辺（ビデオ幅）およびビデオの短辺（ビデオ高さ）は0または128px～4096px
	+ フレームレート：0～60fps
+ オーディオパラメータ：
	+ コーデック：AAC、MP3
	+ サンプルレート：32000Hz、44100Hz、48000Hzの3種類のデフォルトのサンプルレート
	+ オーディオビットレート：0または26kbps～256kbps
	+ サウンドチャンネル：シングルサウンドチャンネル、ダブルサウンドチャンネル
+ 共通テンプレート：共通テンプレートに設定するかどうかを指定

作成したテンプレートはテンプレートリストに表示され、共通テンプレートに設定できます。また、テンプレートの表示、編集、削除などの管理操作を行うことができます。
>?[プリセットのパラメータテンプレートリスト - 高速高画質トランスコーディング](https://intl.cloud.tencent.com/document/product/266/33932#preset-teshd-templates)をご参照ください。


## オーディオトランスコードテンプレート[](id:yp)
業務のニーズに応じて、新しいオーディオトランスコードテンプレートを作成して、カスタマイズ設定を行うことができます。**オーディオトランスコーディングテンプレート**を選択してから、**オーディオテンプレートを作成する**をクリックして、テンプレートのカスタマイズ設定に進みます。

+ テンプレート名：中国語、英語、数字、スペース、アンダーバー(_)、ハイフン(-)、ピリオド(.)の7種類の形式のみサポートし、64文字を超える長さは対応していません
+ コンテナ形式：MP3、FLAC、OGG、M4A
+ オーディオパラメータ：
	+ コーデック：コンテナ形式がMP3のとき対応するコーデックはMP3。コンテナ形式がFLAC、OGG のとき対応するコーデックはFLAC。コンテナ形式がM4Aのとき対応するコーデックはMP3、AAC、AC3
	+ サンプルレート：32000Hz、44100Hz、48000Hzの3種類のデフォルトのサンプルレート
	+ オーディオビットレート：0または26kbps～256kbps
	+ サウンドチャンネル：シングルサウンドチャンネル、ダブルサウンドチャンネル
+ 共通テンプレート：共通テンプレートに設定するかどうかを指定

作成したテンプレートはテンプレートリストに表示され、共通テンプレートに設定できます。また、テンプレートの表示、編集、削除などの管理操作を行うことができます。

#### プリセットのパラメータテンプレートリスト
パラメータの詳細については、[プリセットのパラメータテンプレートリスト - オーディオトランスコーディングテンプレート](https://intl.cloud.tencent.com/document/product/266/33932#preset-transcoding-templates)をご参照ください。


## ABSテンプレート

業務のニーズに応じて、システムで事前設定したABSテンプレートを直接使用するか、またはカスタマイズしたテンプレートを作成することができます。
+ **基本情報**
	+ テンプレート名：中国語、英語、数字、スペース、アンダーバー(_)、ハイフン(-)、ピリオド(.)の7種類の形式のみサポートし、64文字を超える長さは対応していません
	+ コンテナ形式：HLS
	+ 暗号化タイプ：暗号化およびSimpleAESは使用しません
	+ 低解像度から高解像度を有効にする：有効または無効
+ **サブストリーム情報**
	+ ビデオコーデック：H.264、H.265
	+ ビデオビットレート：0または128kbps～35000kbps
	+ ビデオ解像度：ビデオの長辺、短辺を0または128px～4096pxに制限
	+ ビデオフレームレート：ビデオフレームレートは0 - 60fpsに制限
	+ オーディオコーデック：AAC、MP3
	+ オーディオサンプルレート：32000Hz、44100Hzおよび48000Hz
	+ オーディオビットレート：0または26kbps～256kbps
	+ サウンドチャンネル：シングルサウンドチャンネル、ダブルサウンドチャンネル

作成したテンプレートはテンプレートリストに表示でき、テンプレートについて表示、編集、削除などの管理操作を行うことができます。
>?
>- テンプレート作成時、1個以上のサブストリーム情報を追加してください。
[プリセットのパラメータテンプレートリスト-ABSテンプレート](https://intl.cloud.tencent.com/document/product/266/33932#preset-adaptive-bitrate-streaming-templates)をご参照ください。

## ウォーターマークテンプレート

業務のニーズに応じて、画像をアップロードすることによりウォーターマークテンプレートを作成し、またウォーターマーク設定やビデオ内の位置をカスタマイズすることができます。

+ テンプレート名：中国語、英語、数字、スペース、アンダーバー(_)、ハイフン(-)、ピリオド(.)の7種類の形式のみサポートし、64文字を超える長さは対応していません
+ ウォーターマークタイプ：画像ウォーターマーク
+ ウォーターマーク画像：PNGおよびAPNG形式の画像をサポートします。ビデオ効果を最もよくするために、画像の透過にはPNG形式；画像サイズは200KB以下、サイズは200px * 200pxの範囲内にすることを推奨します。
+ ウォーターマークの位置：デフォルトでは左上。左下、右上、右下を選ぶことができます。
+ 水平オフセット：水平オフセットのパーセンテージは、ウォーターマークと左上隅の水平距離との水平幅の比率を表します。水平オフセットの百分率を調整することでウォーターマークの水平位置の設定を行います
+ 垂直オフセット：垂直オフセットのパーセンテージは、ウォーターマークと左上隅の垂直距離と垂直高さとの比率を表します。垂直オフセットのパーセンテージを調整することでウォーターマークの垂直位置の設定を行います
+ ウォーターマークのサイズ：パーセンテージ % または画素数 px に従ってサイズ調整を選択でき、単位に%を選んだときは、元のサイズがパーセンテージでズームされます。単位にpxを選んだときは、ウォーターマークは指定値に従ってズームされます

作成し完成したウォーターマークテンプレート管理リストでは、ウォーターマークテンプレート名、ウォーターマークファイルのプレビュー、形式、タイプ、ウォーターマークの位置やサイズなどの情報を表示することができ、またそのウォーターマークテンプレートの表示、編集、削除ができ、デフォルトのテンプレートとして設定することもできます。
>?例えば、水平オフセット：0%、垂直オフセット：0%の場合は、ウォーターマークはビデオ画面の左上隅に付きます。水平オフセット：90%、垂直オフセット：90%の場合は、ウォーターマークはビデオファイルの右下隅に付きます。

## スクリーンキャプチャテンプレート
業務のニーズに応じて、スクリーンキャプチャテンプレートを作成し、アップロードしたビデオに複数の方式のスクリーンキャプチャを行えます。現在コンソールはタイムポイントのスクリーンキャプチャ、サンプルスクリーンキャプチャ、スプライトイメージのスクリーンキャプチャという3種類のスクリーンキャプチャ方式をサポートしています。

テンプレート名、スクリーンキャプチャタイプ、画像サイズがスクリーンキャプチャテンプレートに表示されます。操作バーでテンプレートを表示、編集、削除できます。

### タイムポイントのスクリーンキャプチャ
スクリーンキャプチャからタイムポイントのスクリーンキャプチャを選択して、**サンプルのタイムポイントはスクリーンキャプチャタスク設定で指定する必要があり、テンプレート設定ではスクリーンキャプチャのタイプの設定しかできません**。タイムポイントのスクリーンキャプチャのタスク設定については、 [タスク設定の説明](https://intl.cloud.tencent.com/document/product/266/14058#custom-task-flow)をご参照ください。

- テンプレート名：中国語、英語、数字、スペース、アンダーバー(_)、ハイフン(-)、ピリオド(.)の7種類の形式のみサポートし、64文字を超える長さは対応していません
- 画像形式：JPG
- 画像サイズ：0または128px – 4096px

#### プリセットのパラメータテンプレートリスト
パラメータの詳細については、[プリセットのパラメータテンプレートリスト - 時点のスクリーンショットテンプレート](https://intl.cloud.tencent.com/document/product/266/33932#preset-animated-image-generating-templates)をご参照ください。

### サンプリングスクリーンキャプチャ
スクリーンキャプチャタイプでサンプリングスクリーンキャプチャを選択します。

- テンプレート名：中国語、英語、数字、スペース、アンダーバー(_)、ハイフン(-)、ピリオド(.)の7種類の形式のみサポートし、64文字を超える長さは対応していません
- 画像形式：JPG
- 画像サイズ：0または128px – 4096px
- サンプリング間隔：百分率（最大で100%）、時間(s)

#### プリセットのパラメータテンプレートリスト
パラメータの詳細については、[プリセットのパラメータテンプレートリスト - サンプリングのスクリーンショットテンプレート](https://intl.cloud.tencent.com/document/product/266/33932#preset-time-point-screenshot-templates)をご参照ください。


### スプライトイメージのスクリーンキャプチャ
スクリーンキャプチャタイプでスプライトイメージのスクリーンキャプチャを選択します。

- テンプレート名：中国語、英語、数字、スペース、アンダーバー(_)、ハイフン(-)、ピリオド(.)の7種類の形式のみサポートし、64文字を超える長さは対応していません
- 画像形式：JPG
- 画像サイズ：0または128px – 4096px
- サンプリング間隔：百分率（最大で100%）、時間(s)
- サブ画像の行数：正の整数とし、サブ画像の行数とサブ画像の列数の積は100以下とします
- サブ画像の列数：正の整数とし、サブ画像の行数とサブ画像の列数の積は100以下とします



#### プリセットのパラメータテンプレートリスト
パラメータの詳細については、[プリセットのパラメータテンプレートリスト - スプライトイメージのテンプレート](https://intl.cloud.tencent.com/document/product/266/33932#preset-sampled-screenshot-templates)をご参照ください。

## アニメーション画像生成テンプレート
業務のニーズに応じて、アニメーション画像生成テンプレートを作成し、指定した時間内に必要なアニメーション画像を切り取ることができます。**アニメーション画像生成の時間帯は、タスクフローのアニメーション画像生成タスク設定で指定する必要があります。テンプレート設定ではアニメーション画像生成のタイプの設定しかできません**。アニメーション画像生成のタスク設定については [タスク設定の説明](https://intl.cloud.tencent.com/document/product/266/14058#custom-task-flow)をご参照ください。

- 画像タイプ：WebPおよびGIFをサポート
- フレームレート：1fps～30fps
- 画像品質：1～100
- 画像サイズ：0～1920px

#### プリセットのパラメータテンプレートリスト
パラメータの詳細については、[プリセットのパラメータテンプレートリスト - アニメーション画像生成のテンプレート](https://intl.cloud.tencent.com/document/product/266/33932#preset-remuxing-templates)をご参照ください。



## スマート認識テンプレート
業務のニーズに応じて、インテリジェントビデオ識別の新しいテンプレートを作成し、カスタム設定を行うことができます。**審査テンプレートを作成する**をクリックしてテンプレートのカスタム設定に進みます。

- テンプレート名：中国語、英語、数字、スペース、アンダーバー(\_)、ハイフン(-)、ピリオド(.)のみサポートし、64文字を超える長さは対応していません
- フレーム抽出インターバル：スマート認識ビデオが数秒ごとにフレーム抽出チェックされることを示します。フレーム抽出インターバルの単位は秒で、デフォルト値は1、最小値は0.5です
- スマート認識項目：選択可能なスマート認識項目は、画像認識、音声認識、文字認識となります。選択後、スマート認識サブ項目が右側の選択済の欄に現れます
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th >スマート認識項目</th>
<th align="center" nowrap="nowrap">スマート認識サブ項目</th>
<th align="center">説明</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan = 3 nowrap="nowrap">画像認識</td>
<td align="center">不快にさせる情報</td>
<td align="center">卑猥、低俗、過度な愛情行為、性的なサブ項目のスマート認識が含まれます。</td>
</tr>
<tr>
<td align="center">危険を感じる情報</td>
<td align="center">武装勢力、武器銃器、血生臭いシーン、警察部隊、密集する群衆に対するサブ項目スマート認識が含まれます</td>
</tr>
<tr>
<td align="center">不適切と感じる情報</td>
<td align="center">話題の人物、違法なアイコン、エンターテインメントのスター、スポーツのスターに対するサブ項目スマート認識が含まれます</td>
</tr>
<tr>
<td rowspan = 3>音声識別</td>
<td align="center">不快にさせる情報</td>
<td align="center">音声情報の中の不快感を与える情報キーワードを認識</td>
</tr>
<tr>
<td align="center">不適切と感じる情報</td>
<td align="center">音声情報の中の不適切と感じる情報キーワードを認識</td>
</tr>
<tr>
<td align="center">禁令違反</td>
<td align="center">音声情報の中の罵詈雑言、違法賭博などといった内容のキーワードを識別</td>
</tr>
<tr>
<td rowspan = 4>文字識別</td>
<td align="center">不快にさせる情報</td>
<td align="center">文字情報の中の不快感を与える情報キーワードを認識</td>
</tr>
<tr>
<td align="center">不適切と感じる情報</td>
<td align="center">文字情報の中の不適切と感じる情報キーワードを認識</td>
</tr>
<tr>
<td align="center">危険を感じる情報</td>
<td align="center">文字情報の中の危険を感じる情報キーワードを認識</td>
</tr>
<tr>
<td align="center">禁令違反</td>
<td align="center">文字情報の中の罵詈雑言、違法賭博などの内容のキーワードを識別</td>
</tr>
</tbody></table>

各スマート認識サブ項目はいずれも**信頼確認閾値**および**ダウト閾値**を設定でき、これによりスマート認識の度合いを調整します。入力しない場合は、VODのデフォルト値に従って入力とスマート認識が実行されます。
 - 信頼確認閾値：VODではユーザーがアップロードしたスマート認識ビデオについて計算したうえで、スマート認識スコアを出します。スコアがユーザーの設定値を超えているときは、その項目のスマート認識ステータスは「確認済み」となります。特別な要件がなければ、デフォルト値の範囲（0～100）を使用することをお勧めします。
 - ダウト閾値：VODではユーザーがアップロードしたスマート認識ビデオについて計算したうえで、スマート認識スコアを出します。スコアがユーザーの設定値を超えているときは、その項目のスマート認識ステータスは「危険」となり、ユーザーはビデオスマート認識画面で手動再審査を開始できます。特別な要件がなければ、デフォルト値の範囲（0～100）を使用することをお勧めします。

作成したテンプレートはテンプレートリストに表示でき、テンプレートについて表示、編集、削除などの管理操作を行うことができます。

>?[プリセットのパラメータテンプレートリスト - インテリジェント識別のテンプレート](https://console.cloud.tencent.com/vod/video-process/template/audit)をご参照ください。
