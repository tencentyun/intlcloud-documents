Tencent Cloud LVBでは、セルフチェックツールを提供しています。このツールによってセルフチェックを行い、よくあるLVB プッシュ/再生の問題を素早く診断することができ、これにはユーザー、URL、ドメイン名、ストリームなどの診断項目が含まれ、解決策のアドバイスも受けられます。現在は、パブリックテストの段階となり、診断結果は参考としてのみ提供されています。

## 前提条件
- [自身でのURL合成](https://intl.cloud.tencent.com/document/product/267/38393) または [アドレスジェネレーターによる生成](https://intl.cloud.tencent.com/document/product/267/31084) の方式によって、プッシュ/再生アドレスを生成済みであること。
- プッシュアドレスが、オンラインで[LVBプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)をすでに行っていること。


## チェックの手順

あるLVBプッシュ/再生に異常が発生したことを見つけた時に、故障診断によって検査を起動することができます。手順は次のとおりです。

1. LVBコンソールにログインし、左側メニューバーから、[【セルフチェック】](https://console.cloud.tencent.com/live/tools/selfcheck)を選択します。
2. 診断したいアドレスタイプを選択します。**プッシュアドレス**または**再生アドレス**を選択できます。
3. 完全なURLアドレスを入力して、【チェックの実行】をクリックすれば、チェックの結果が生成されます。

![](https://main.qcloudimg.com/raw/90fc6fce80283550af50214782c25b3c.png)

## チェック結果

チェック完了後、下側にチェックの結果が生成されますので、アドバイスを参考に異常を処理することができます。チェック項目は次のとおりです。

<table>
<tr><th>チェック項目名</th><th>チェックのタイプ</th><th>説明</th>
</tr><tr>
<td>ユーザー</td>
<td>状態</td>
<td>ユーザーアカウントの状態</td>
</tr><tr>
<td rowspan="5">URL</td>
<td>AppName</td>
<td>URLパスパラメータ</td>
</tr><tr>
<td>認証するStreamName</td>
<td>txSecretの認証情報の計算に用いるStreamName</td>
</tr><tr>
<td>StreamName</td>
<td>ストリーム名</td>
</tr><tr>
<td>txSecret</td>
<td>プッシュ認証を有効にした後に生成される認証文字列</td>
</tr><tr>
<td>txTime</td>
<td>プッシュアドレス設定のタイムスタンプ</td>
</tr><tr>
<td rowspan="6">ドメイン名</td>
<td>ドメイン名の状態</td>
<td>接続状態</td>
</tr><tr>
<td>ドメイン名タイプ</td>
<td>プッシュ/再生ドメイン名</td>
</tr><tr>
<td>プッシュ認証</td>
<td>プッシュドメイン名認証状態</td>
</tr><tr>
<td>プッシュ認証</td>
<td>グローバル認証の状態</td>
</tr><tr>
<td>URLの実際の期限切れ時間</td>
<td>プッシュ/再生URLの実際の期限切れ時間</td>
</tr><tr>
<td>CNAME</td>
<td>CNAME解決状況</td>
</tr><tr>
<td>ストリーム</td>
<td>状態</td>
<td>ストリーム状態</td>
</tr></table>

>? チェック報告で問題を解決できない場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)か、あるいはTencent Cloudの技術者にお問い合わせの上、問題を特定することをお勧めします。
