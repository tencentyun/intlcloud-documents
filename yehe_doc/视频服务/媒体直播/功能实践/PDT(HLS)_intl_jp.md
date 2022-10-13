HLS出力のMedia ManifestにEXT-X-PROGRAM-DATE-TIMEタグを設定し、絶対日付または時刻を有するメディアセグメントの最初のサンプルにバインドすることができます。具体的な形式は次のとおりです。

```
1  #EXT-X-PROGRAM-DATE-TIME:<date-time-msec>
```

このdate-time-msecはISO/IEC 8601:2004 [ISO_8601]日付/時刻であり、例えば、YYYY-MM-DDThh:mm:ss.SSSZのように表します。 タイムゾーンおよび秒の小数部分を明記し、ミリ秒単位まで正確にしなければなりません。

HLS出力にPDTを挿入します。初めに変更したい**Channel**を選択し、**Output Group Setting**編集ページに進みます。**Output Group Type**がHLS、HLS_ARCHIVE、HLS_STREAM_PACKAGEの場合のみ設定が可能となります。
下図のように、**Segment Infomation**の選択で、**PdtInsertion**スイッチを見つけてオンにし、挿入間隔を設定します。単位は秒です。
![](https://qcloudimg.tencent-cloud.cn/raw/0863a6dc3e189d25d7c37c6e18d2af4d.png)
編集が完了したら、チャネルを起動します。入力があると、出力されるM3u8でPDTタグを確認できるようになります。600秒に1回挿入されます。





