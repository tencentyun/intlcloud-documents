CSSはタイムシフトを全面的にアップグレードしました。コンソールでタイムシフトのテンプレートを作成することで、新しいバージョンのCSSタイムシフト機能を簡単にアクティブ化できるようになりました。組立ルールに従って、CSSタイムシフトの再生アドレスを組み立てれば、ライブストリーミング中に、ライブストリーミングの内容をプレイバックできます。また、CSSタイムシフト機能はAPI3.0に取り込まれています。詳細については、[新しいバージョンのCSSタイムシフトに関するインターフェース](https://intl.cloud.tencent.com/document/product/267/30760)をご参照ください。本書では、新しいバージョンのCSSタイムシフトの仕組みと再生のリクエスト方法を説明します。

## 注意
- 現在、新しいバージョンのCSSタイムシフトは、3万人の同時視聴をサポートします。タイムシフトでの再生に対して、これ以上の同時視聴者数を要求する場合、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してご連絡ください。
- 再生ドメイン名に再生認証と有効期限が設定されている場合、認証の有効期限が切れると、タイムシフトの再生アドレスが無効になります。
- 既存の、VODドメイン名でタイムシフトを取得する方法は、チケットを介して評価する必要があります。関連ドキュメントについては、[古いバージョンのCSSタイムシフト](https://intl.cloud.tencent.com/document/product/267/31565)をご参照ください。タイムシフトをより良く楽しむために、現在のCSSタイムシフトソリューションを使用することをお勧めします。

## タイムシフトの仕組み
CSSタイムシフトはライブストリーミング中に、メディアストリームをTSに変換して保存すると同時に、クラウド側でTSとライブストリームのリアルタイムとの対応関係を作成することで、ライブストリーミングをプレイバックする機能を実装します。この機能は、テレビ局の再生や試合のハイライト再生などによく使用されます。クライアントでHLSプロトコルを通して配信し、M3U8リクエストのパラメータで再生する時間帯(パラメータの詳細は、[再生リクエスト](#play)を参照)を指定します。

[](id:play)
## 再生リクエスト
CSSタイムシフトの再生アドレスの形式は`http://domain/appname/stream.m3u8`です。以下の2種類のタイムシフト再生をサポートします。
- 指定した時間帯の再生：試合のハイライトシーンを再生することに使用できます。視聴内容は指定した時間まで再生されます。
- 現在の時間に対するオフセットの再生:ライブシトリーミングを遅延させるシーンに使用できます。視聴内容はライブストリーミングが終了するまで再生されます。

### 指定した時間帯を再生するパラメータ
<table id="setmess">
<tr><th width="14%">フィールド名</th><th>意味</th><th>必須か</th><th>例</th>
</tr><tr>
<td>txTimeshift</td>
<td>値がonの場合、新しいバージョンのCSSタイムシフトを有効にする</td>
<td>はい</td>
<td>txTimeshift=on</td>
</tr><tr>
<td>tsStart</td>
<td>タイムシフトの開始時間</td>
<td>はい</td>
<td>tsStart=20121010010101</td>
</tr><tr>
<td>tsEnd</td>
<td>タイムシフトの終了時間</td>
<td>はい</td>
<td>td>tsEnd=20121010010102</td>
</tr><tr>
<td>tsFormat</td>
<td><ul style="margin:0">
<li>tsStartとtsEndの形式。値の形式は<code>{timeformat}_{unit}_{zone}</code>とする</li>
<li>timeformatの値：<ul>
<li/>UNIX - UNIXタイムスタンプ。UNIXを選択した場合、後続のzoneを省略できる
<li/>human - 人間が分かる時間20121010010101</ul></li>
<li>unit：s|ms</li>
<li>単位はsとms。</li>
  <li>zone：タイムゾーンは東側と西側に分かれている。<ul style="margin:0"><li>東側の値の範囲は1～12、<li>西側の値の範囲は -12～-1とする。</ul></li>
</ul></td>
<td>はい</td>
<td>tsFormat=unix_s
tsFormat=human_s_8</td>
</tr><tr>
<td>tsCodecname</td>
<td>トランスコーディングストリームは、テンプレート名を指定する必要がある。オリジナルストリームとウォーターマークストリームには、このフィールドがない</td>
<td>いいえ</td>
<td>tsCodecname=hd</td>
</tr></table>



#### リクエスト例1（U形式の時間）
```
http://example.domain.com/live/stream.m3u8?txTimeshift=on&tsFormat=unix_s&tsStart=1675302995&tsEnd=1675303025&tsCodecname=test
```
#### リクエスト例2（human形式の時間）
```
http://example.domain.com/live/stream.m3u8?txTimeshift=on&tsFormat=unix_s_8&tsStart=20230202095635&tsEnd=20230202095705&tsCodecname=test
```

### 現在の時間に対するオフセットを再生するパラメータ

| フィールド名    | 意味                    | 必須か | 例                                |
| ----------- | ----------------------- | ---------- | ----------------------------------- |
| txTimeshift | 値がonの場合、新しいバージョンのCSSタイムシフトを有効にする | はい         | txTimeshift=on                      |
| tsDelay     | 現在の時間より前の秒数    | はい         | tsDelay=30 現在の時間より30秒前の内容を再生する |
| tsCodecname | トランスコーディングストリームは、テンプレート名を指定する必要がある。  | いいえ         | tsCodecname=2000                    |

#### リクエスト例
```
http:://example.domain.com/live/stream.m3u8?txTimeshift=on&tsDelay=30&tsCodecname=test
```
### タイムシフトを認証するパラメータ
タイムシフトはCSS認証のパラメータと一致します。詳細については、[参考ドキュメント](https://intl.cloud.tencent.com/document/product/267/31060)をご参照ください（公式サイトで生成したHLSアドレスの有効期限は1日で、1日が経つと、再生成する必要があります）。

### タイムシフトインデックスの検索
コンソールのCSSタイムシフト－インデックスの情報で、ある時間帯におけるタイムシフトストリームリストを検索できます。詳細をクリックすると、ストリームの詳細情報を個別に確認できます。
TencentCloud APIでもタイムシフトストリームリストと個別のストリームの詳細を確認できます。詳細については、以下のドキュメントをご参照ください：
- [CSS タイムシフトリストの確認-APIドキュメント-ドキュメントセンター-Tencent Cloud](https://www.tencentcloud.com/document/product/267/53719)
- [CSS タイムシフトストリームレコーディング詳細の確認-APIドキュメント-ドキュメントセンター-Tencent Cloud](https://www.tencentcloud.com/document/product/267/53720)