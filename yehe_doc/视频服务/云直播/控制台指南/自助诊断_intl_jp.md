 Tencent Cloud CSSでは、セルフ診断ツールを提供しています。このツールによってセルフチェックを行い、ユーザー、URL、ドメイン名、ストリームなどの診断項目が含まれたよくあるCSSプッシュ/再生の問題を素早く診断し、解決策のアドバイスも受けられます。現在は、パブリックベターテストの段階となり、診断結果は参考としてのみ提供されています。

##  前提条件
- [自身でのURL合成](https://intl.cloud.tencent.com/document/product/267/38393)または[アドレスジェネレーターによる生成](https://intl.cloud.tencent.com/document/product/267/31084)の方式によって、プッシュ/再生アドレスを生成済みであること。
- プッシュアドレスが、オンラインで[CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)をすでに行っていること。


## 診断の手順
異常のCSSプッシュ/再生を見つけた時に、故障診断によって検査を開始することができます。手順は次のとおりです：
1. CSSコンソールにログインし、左側メニューバーから、[**セルフ診断**](https://console.cloud.tencent.com/live/tools/selfcheck)を選択します。
2. 診断を必要とするプッシュアドレスまたは再生アドレスを入力します。
3. **診断の実行**をクリックすると、診断結果が発行されます。

![](https://main.qcloudimg.com/raw/90fc6fce80283550af50214782c25b3c.png)

## 診断結果
診断完了後、下側に診断結果が生成されますので、診断アドバイスを参考に異常を処理することができます。診断項目は次のとおりです：

<table>
<thead><tr><th width=15%>診断項目</th><th width=15%>診断タイプ</th><th>説明</th></tr></thead>
<tbody><tr>
<td rowspan=2>顧客情報取得</td>
<td>APPID</td>
<td>ユーザーアカウントのAPPID</td>
</tr><tr>
<td>状態</td>
<td>ユーザーアカウントの状態</td>
</tr><tr>
<td rowspan=3>ドメイン名のチェック</td>
<td>ドメイン名</td>
<td>ドメイン名</td>
</tr><tr>
<td>ドメイン名のタイプ</td>
<td>プッシュ/再生ドメイン名</td>
</tr><tr>
<td>CNAME</td>
<td>CNAME解析状況</td>
</tr><tr>
<td rowspan=2>ストリームステータスのチェック</td>
<td>ストリーム</td>
<td>ストリームID</td>
</tr><tr>
<td>状態</td>
<td>ストリーム状態</td>
</tr><tr>
<td rowspan=12>URLチェック</td>
<td>URL</td>
<td>プッシュ/再生アドレス</td>
</tr><tr>
<td>AppName</td>
<td>URLパスパラメータ</td>
</tr><tr>
<td>StreamName</td>
<td>txSecretの認証情報の計算に用いるStreamName</td>
</tr><tr>
<td rowspan=3>認証設定</td>
<td>オン/オフ状態</td>
</tr><tr>
<td>プライマリーキーの認証</td>
</tr><tr>
<td>バックアップキーの認証</td>
</tr><tr>
<td rowspan=6>プッシュ/再生の認証</td>
<td>認証に成功/認証に失敗</td>
</tr><tr>
<td>失敗の原因</td>
</tr><tr>
<td>StreamnNmeの認証</td>
</tr><tr>
<td>txSecret：プッシュ/再生の認証を有効にした後に発行される認証文字列</td>
</tr><tr>
<td>txTime：プッシュ/再生アドレスで設定されるタイムスタンプ</td>
</tr><tr>
<td>URLの実際の期限切れ時間</td>
</tr><tr>
<td rowspan=4>帯域幅チェックにアクセス</td>
<td rowspan=2>帯域幅キャッピング構成</td>
<td>オン/オフ</td>
</tr><tr>
<td>アクセラレーションリージョン</td>
</tr><tr>
<td rowspan=2>アクセス状況</td>
<td>状態</td>
</tr><tr>
<td>現在の帯域幅</td>
</tr><tr>
<td rowspan=6>サービスセルフチェック</td>
<td rowspan=3>クライアントセルフチェック</td>
<td>
<li/>PC端末プッシュ：<a href="https://intl.cloud.tencent.com/document/product/267/31569">OBSプッシュ</a>を使用することをお勧めします
 <li/>PC端末再生：<a href="https://intl.cloud.tencent.com/document/product/267/32483">VLCプレーヤー</a>を使用することをお勧めします</td>
</tr><tr>
<td>
<li/>Web端末プッシュ：<a href="https://console.cloud.tencent.com/live/tools/webpush">Webプッシュ</a>を使用することをお勧めします</td>
</tr><tr>
<td>
<li/>モバイル端末プッシュ：<a href="https://intl.cloud.tencent.com/document/product/1071/38147">TCToolkit App</a>をダウンロードしてインストールし、RTMPプッシュを選択してください
<li/>モバイル端末再生：<a href="https://intl.cloud.tencent.com/document/product/1071/38147">TCToolkit App</a>をダウンロードしてインストールし、標準ライブストリーミング再生を選択してください</td>
</tr><tr>
<td>IP制限セルフチェック</td>
<td>IPブラックリスト/ホワイトリスト、IPリージョン制限をチェックし、IP制限による異常を排除します</td>
</tr><tr>
<td>ストリームデータの監視</td>
<td>CSSストリームのリアルタイムモニタリングデータを分析し、<a href="https://console.cloud.tencent.com/live/analysis/stream">ストリーミングデータ</a>を確認することで、ネットワーク輻輳やジッターなどの現象による異常があるかどうかを判断します。</td>
</tr>
</tbody></table>


>? 診断報告で問題を解決できない場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)するか、あるいはTencent Cloudの技術者にお問い合わせの上、問題を特定することをお勧めします。
