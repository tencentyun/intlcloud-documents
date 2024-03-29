有料ビデオプラットフォームが抱える最大の問題点は、一部の会員ユーザーがさまざまな方法でビデオをダウンロードし、他のプラットフォームに違法に配布して共有または販売することで、著作権者の利益を著しく損なうという点です。このような著作権侵害への対応として最も有効な方法の一つが、不正録画されたビデオを追跡し、他の手段を併用して権益を保護し、不正録画を行う者を震え上がらせ、失われた利益を回収することです。VODのトレーサビリティウォーターマークによって、低コストと高セキュリティを同時に実現できるほか、高いロバスト性、見た目の美しさなどの特徴も備えたトレーサビリティ障壁を簡単に構築することができます。

## 従来のトレーサビリティウォーターマークの欠点

従来のビデオ不正録画防止用のトレーサビリティ方式は、ビデオ画面に視聴者のユーザーIDを表示するものです。主に**一般的な画像・テキストウォーターマーク**と**再生側フローティングウォーターマーク**という2種類の方式があります。

<table>
   <tr>
      <th width="0px" style="text-align:center">一般的な画像・テキストウォーターマーク</td>
      <th width="0px" style="text-align:center">再生側フローティングウォーターマーク</td>
   </tr>
   <tr>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/82766338aee9f4f9715427e337babd25.png" width=500>ビデオトランスコードの際に、ビデオ画面にエンコードされる画像またはテキストウォーターマークです。テキストの内容はユーザーIDです。

</td>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/69dbaf292d144094854efca31e51d922.png" width=500>
			プレーヤーでの再生の際にビデオレイヤー上に表示されるウォーターマークです。通常は電光掲示板形式で画面上を移動します。</td>
   </tr>
</table>
これらの2種類のウォーターマークには、それぞれ次のような特徴があります。

|  | 一般的なテキストウォーターマーク | 再生側フローティングウォーターマーク |
| -- | -- | -- |
| 安全性 | 高い：ウォーターマークはビデオにエンコードされており、除去できません | やや低い：ウォーターマークはプレーヤーのカバーレイヤーに付与され、ビデオ内にはエンコードされていません |
| コスト | 高い：個別のユーザーIDウォーターマークごとに1回ずつトランスコードし、それぞれ保存する必要があります | 低い：VODプレーヤーに内蔵することで実現できます |
| ロバスト性 | 低い：ウォーターマークは固定の位置にあり、トリミングや遮蔽が容易に行えます | やや低い：ウォーターマークが目に見えるため、遮蔽が容易です |
| 視覚効果 | 劣る：ウォーターマークがビデオ上にあるため、視覚に影響します | 劣る：ウォーターマークがビデオ上にあるため、視覚に影響します |


このように、従来の一般的な画像・テキストウォーターマークと再生側フローティングウォーターマークには不十分な点がいくつかあります。

## VODトレーサビリティウォーターマーク

VODトレーサビリティウォーターマークは、低コストと高い安全性を満たすだけでなく、高いロバスト性、見た目の美しさなどの特徴も備えています。

* 低コスト：わずかにトランスコードとストレージコストを追加するだけで、数十億の視聴者のマーキングとトラッキングを実現することができます。
* 高い安全性：ウォーターマークはビデオ画面にエンコードされているため、ビデオを移動させても画面内に付与されたウォーターマークを消すことはできません。
* 高いロバスト性：リサンプリング、圧縮、ジッター、トリミング、ズーム、回転、フィルタリングなどの後処理のような、さまざまな攻撃に耐えることができます。
* 見た目の美しさ：ウォーターマークのエンコード後も画質に影響はなく、肉眼で感知されません。

>! トレーサビリティウォーターマークは現在ベータ版テスト段階です。ご利用の際は次のことをお勧めします。
>1. **30分以上**のビデオのトレーサビリティのみサポートしています。
>2. 現在はブロードキャスト、OTTシーンの**映画、ドラマ、バラエティー番組**で良好なトレーサビリティ効果が得られています。
>3. **教育トレーニング**系ビデオでの抽出効果はまだ改善中です。このシーンでご利用予定のお客様は、機能の正式リリース後にテストとアクセスを行うことをお勧めします。

## 使用方法

### トレーサビリティウォーターマークの付与

[ProcessMeidaインターフェース](https://intl.cloud.tencent.com/document/product/266/34125)を呼び出し、ビデオへのトレーサビリティウォーターマーク付与タスクを開始します。トランスコードまたはアダプティブビットレートストリーミング用トランスコードを選択できます。

#### トランスコード：
* コンテナ形式がHLSのトランスコードテンプレートを選択します。プリセットテンプレート100230の場合は、MediaProcessTask.TranscodeTaskSet.Definition=100230と入力します。
* トレーサビリティウォーターマークを有効化します。MediaProcessTask.TranscodeTaskSet.TraceWatermark.Switch=ONにします。

#### アダプティブビットレートストリーミング用トランスコード：
* コンテナ形式がHLSのアダプティブビットレートストリーミングテンプレートを選択します。プリセットテンプレート10の場合は、MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition=10と入力します。
* トレーサビリティウォーターマークを有効化します。MediaProcessTask.AdaptiveDynamicStreamingTaskSet.TraceWatermark.Switch=ONにします。

### ビデオの再生

すべての有料顧客に、固有の6桁16進数の整数を関連付ける必要があります。これは視聴者のIDを表し、uvと呼びます。これ以降、uvは視聴者へのトレーサビリティの根拠となります。

* VODの[Player SDK](https://intl.cloud.tencent.com/document/product/266/33977)または[サードパーティのプレーヤープラグイン](https://intl.cloud.tencent.com/document/product/266/42095)を使用する場合、業務サーバーは再生リクエスト1回ごとに[プレーヤー署名](https://intl.cloud.tencent.com/document/product/266/38099)を配布する必要があります。[署名パラメータ](https://intl.cloud.tencent.com/document/product/266/38099#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0)のuvには、視聴者のuvを入力します。
* VODのPlayer SDKを使用しない場合は、[Keyリンク不正アクセス防止](https://intl.cloud.tencent.com/document/product/266/33986)の使用ルールに従い、URLの中のQueryStringにuvパラメータを追加する必要があります。パラメータには視聴者のuvを入力します。

### ウォーターマークの抽出

ビデオが不正録画された後、[ExtractTraceWatermarkインターフェース](https://www.tencentcloud.com/document/product/266/50423)を呼び出すと、VODが不正録画されたビデオから視聴者のuvを抽出し、トレーサビリティを実現します。

## 操作手順
トレーサビリティウォーターマークの付与と視聴者ID抽出の流れについて、以下の簡単な5つのステップでご説明します。

[](id:step1)
### ステップ1：ビデオのアップロード

1. VODコンソールのナビゲーションバーで、**メディア資産管理**>**オーディオビデオ管理**を選択し、**オーディオビデオのアップロード**をクリックし、ビデオをアップロードします。
2. ビデオのアップロード完了後、アップロードしたビデオのIDを記録します。

[](id:step2)
### ステップ2：トレーサビリティウォーターマークの付与

1. ビデオ処理の[インターフェースドキュメント](https://intl.cloud.tencent.com/document/product/266/34125)を参照し、[API Explorer](https://console.cloud.tencent.com/api/explorer)によってアダプティブビットレートストリーミングタスクを開始します。このうち、
 * FileIdには**[ステップ1](#step1)**でアップロードしたビデオのビデオIDを入力します。
 * MediaProcessTask.AdaptiveDynamicStreamingTaskSet.0.Definitionに10を入力します。これは10仕様のアダプティブビットレートストリーミングへのトランスコードであることを表します。
 * MediaProcessTask.AdaptiveDynamicStreamingTaskSet.0.TraceWatermark.SwitchにONと入力します。
2. タスクの実行完了後、コンソールのナビゲーションバーから**メディア資産管理**>**オーディオビデオ管理**と進み、ビデオを見つけて**管理**をクリックし、**ABS生成テンプレートリスト**から10テンプレートのアダプティブビットレートストリーミングを見つけ、**アドレスをコピー**をクリックし、再生URLを記録します。

[](id:step3)
### ステップ3：再生体験

1. **[ステップ2](#step2)**で取得した再生URLにQueryStringを追加します。パラメータ名はuvとし、パラメータは任意の6桁の16進数の整数（例えば12abcd）とします。`http://xxx.vod2.myqcloud.com/xxx/xxx/xxx.m3u8?uv=12abcd`のようなURLを取得し、リンクをブラウザのアドレスに貼り付けて再生すると、トレーサビリティウォーターマーク追加後の再生効果が体験できます。

[](id:step4)
### ステップ4：ビデオ不正録画のシミュレーション

1. VODコンソールのナビゲーションバーで、**メディア資産管理**>**オーディオビデオ管理**を選択し、**オーディオビデオのアップロード**>**ビデオのプル**をクリックし、ビデオリソースURLの入力にはステップ3のuv追加後のURLを入力し、クリックしてビデオをプルします。
2. ビデオのプルに成功後、コンソールのナビゲーションバーから**メディア資産管理**>**オーディオビデオ管理**と進み、ビデオを見つけて**管理**をクリックし、**基本情報**>**操作**から**アドレスをコピー**をクリックし、再生URLを記録します。

[](id:step5)
### ステップ5：トレーサビリティウォーターマークの抽出

1. トレーサビリティウォーターマーク抽出の[インターフェースドキュメント](https://www.tencentcloud.com/document/product/266/50423)を参照し、[API Explorer](https://console.cloud.tencent.com/api/explorer)によってトレーサビリティウォーターマーク抽出タスクを開始します。ここで、URLには**[ステップ4](#step4)**で記録したビデオ再生URLを入力します。
2. トレーサビリティウォーターマーク抽出タスクが完了してから、タスク詳細確認の[インターフェースドキュメント](https://console.cloud.tencent.com/workorder/category)を参照し、[API Explorer](https://console.cloud.tencent.com/api/explorer)によってタスクの詳細確認を開始します。タスクの出力から**[ステップ3](#step3)**の再生体験時に追加した視聴者IDが取得できた場合は、著作権侵害者の追跡が実現できています。

## 料金関連

トレーサビリティウォーターマークを使用すると、主に次の料金が発生します。

* トランスコード料金：ビデオにトレーサビリティウォーターマークを付与する際は、トランスコードまたはアダプティブビットレートストリーミングへのトランスコードが必要なため、トランスコード料金が発生します。
* トレーサビリティウォーターマーク付与料金：ビデオにトレーサビリティウォーターマークを付与するため、トレーサビリティウォーターマーク付与料金が発生します。
* ストレージ料金：トランスコードまたはアダプティブビットレートストリーミングへのトランスコード出力を行うと、ストレージスペースを占有するため、ストレージ料金が発生します。
* 抽出料金：著作権侵害が発生すると、トレーサビリティウォーターマーク抽出処理を開始する必要があるため、抽出料金が発生します。

上記の料金の具体的な価格については、[購入ガイド](https://intl.cloud.tencent.com/document/product/266/14666)をご参照ください。
