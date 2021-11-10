VODコンソールによって、ビデオリストに表示するフィールドをカスタマイズし、ビデオファイルをエクスポートすることができます。ここでは、リストフィールドのカスタマイズおよびビデオファイルのエクスポートの操作方法をご紹介します。

## リストフィールドのカスタマイズ


1. VODコンソールにログインし、【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)を選択して、デフォルトで「アップロード済み」画面に進みます。
2. リスト右上方の![](https://main.qcloudimg.com/raw/f4d3608e1d8319051883e90226a86f50.png)をクリックして、表示したいリストフィールドにチェックを入れてから、【OK】をクリックします。最大14件のフィールドを選択できます。ビデオ名/IDおよび操作は、デフォルトでフィールドにチェックが入っています。
![](https://qcloudimg.tencent-cloud.cn/raw/473896085055dc9a382e363cec4db9dc.png)



## ビデオファイルのエクスポート

1. VODコンソールにログインし、【メディア資産管理】>[【ビデオ管理】](https://console.cloud.tencent.com/vod/media)を選択すると、デフォルトで「アップロード済み」のページに進みます。メディア資産にチェックを入れてからエクスポートを行うと、チェックを入れたメディア資産の情報がエクスポートされます。
2. リスト右上方の![](https://main.qcloudimg.com/raw/e530c6f8adeb603d98e1bc7e0ae8e255.png)をクリックし、【エクスポート形式】および【エクスポートデータ】を選択してから、【OK】をクリックします。チェックを入れない場合は、すべてのVODメディア資産の情報がエクスポートされます。
![](https://qcloudimg.tencent-cloud.cn/raw/c390702b9e17fb783cae7e8047873e22.png)
3. VODでは、CSVとJSONLINES形式のファイルのエクスポートをサポートしています。チェックを入れたファイルの情報をエクスポートするか、またはすべてのファイルの情報をエクスポートするかを選択することができます。
 1. CSVフォーマットファイルは値を文字で区切ったファイルであり、このファイルではテキストのみの形式で表データを格納します。ファイル内容のプレビューは次のとおりです。
 ![](https://qcloudimg.tencent-cloud.cn/raw/858c2dac0136337f560d52833921ff00.png)
<table>
   <tr>
      <th width="120px" style="text-align:center">ファイルフォーマット</td>
      <th width="0px" style="text-align:center">フィールド名（次の順に表示）</td>
   </tr>
   <tr>
      <td>CSV フォーマット</td>
      <td>メディアファイル名、作成時間、更新時間、有効期限、メディアファイルカテゴリーID、メディアファイルカテゴリー名、メディアファイルカテゴリーパス、カバー画像のアドレス、メディアファイルソース、メディアファイルストレージ、メディアファイルタグ、ライブストリーミングトランスレコーディングファイル(VID)、ビデオアドレス、ファイルID、ファイルの大きさ、時間</td>
   </tr>
</table>
 2. JSONLINESフォーマットは一度に1行のレコードを処理できる構造化データを格納するために用いられます。ビデオからエクスポートされたJSONLINESフォーマットファイルには次のフィールドが含まれます。
 <table>
   <tr>
      <th width="120px" style="text-align:center">ファイルフォーマット</td>
      <th width="0px" style="text-align:center">フィールド名</td>
      <th width="0px"  style="text-align:center">説明</td>
   </tr>
   <tr>
      <td rowspan='12'>JSONLINES フォーマット</td>
      <td>BasicInfo</td>
      <td>基本情報。ビデオ名、カテゴリー、再生アドレス、カバー画像などが含まれます。</td>
   </tr>
   <tr>
      <td>MetaData</td>
      <td>メタ情報。大きさ、長さ、ビデオストリーム情報、オーディオストリーム情報などが含まれます。</td>
   </tr>
   <tr>
      <td>TranscodeInfo</td>
      <td>トランスコード結果の情報。このビデオトランスコードによって生成された各種ビットレートのビデオのアドレス、規格、ビットレート、解像度などが含まれます。</td>
   </tr>
   <tr>
      <td>AnimatedGraphicsInfo</td>
      <td>アニメーション画像生成結果の情報。</td>
   </tr>
   <tr>
      <td>SampleSnapshotInfo</td>
      <td>サンプルスクリーンキャプチャの情報。</td>
   </tr>
   <tr>
      <td>ImageSpriteInfo</td>
      <td>スプライトイメージの情報。</td>
   </tr>
   <tr>
      <td>SnapshotByTimeOffsetInfo</td>
      <td>指定した時点のスクリーンキャプチャの情報。</td>
   </tr>
   <tr>
      <td>KeyFrameDescInfo</td>
      <td>ビデオのキーモーメント情報。</td>
   </tr>
   <tr>
      <td>AdaptiveDynamicStreamingInfo</td>
      <td>アダプティブビットレートストリーミング用トランスコードの情報。</td>
   </tr>
   <tr>
      <td>SubtitleInfo</td>
      <td>字幕情報。</td>
   </tr>
   <tr>
      <td>FileId</td>
      <td>メディアファイルの固有識別ID。</td>
   </tr>
</table>

