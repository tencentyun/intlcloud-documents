 Tencent Cloud CSSでは、セルフチェックツールを提供しています。このツールによってセルフチェックを行い、よくあるCSS プッシュ/再生の問題を素早く診断することができ、これにはユーザー、URL、ドメイン名、ストリームなどの診断項目が含まれ、解決策のアドバイスも受けられます。現在は、パブリックテストの段階となり、診断結果は参考としてのみ提供されています。

##  前提条件
- [自身でのURL合成](https://intl.cloud.tencent.com/document/product/267/38393) または [アドレスジェネレーターによる生成](https://intl.cloud.tencent.com/document/product/267/31084) の方式によって、プッシュ/再生アドレスを生成済みであること。
- プッシュアドレスが、オンラインで[CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)をすでに行っていること。


## チェックの手順
あるCSSプッシュ/再生に異常が発生したことを見つけた時に、故障診断によって検査を起動することができます。手順は次のとおりです。
1. CSSコンソールにログインし、左側メニューバーから、[**セルフチェック**](https://console.cloud.tencent.com/live/tools/selfcheck)を選択します。
2. チェックしたいプッシュアドレスまたは再生アドレスを入力してください。
3. **チェックの実行**をクリックすると、チェックの結果が発行されます。

![](https://main.qcloudimg.com/raw/90fc6fce80283550af50214782c25b3c.png)

## チェック結果
チェック完了後、下側にチェックの結果が生成されますので、アドバイスを参考に異常を処理することができます。チェック項目は次のとおりです。

<table>
<thead><tr><th width=15%>チェック項目</th><th width=15%>チェックタイプ</th><th>説明</th></tr></thead>
<tbody><tr>
<td rowspan=2>顧客情報取得</td>
<td>APPID</td>
<td>ユーザーアカウントAPPID</td>
</tr><tr>
<td>状態</td>
<td>ユーザーアカウントの状態</td>
</tr><tr>
<td rowspan=3>ドメイン名チェック</td>
<td>ドメイン名</td>
<td>ドメイン名</td>
</tr><tr>
<td>ドメイン名タイプ</td>
<td>プッシュ/再生ドメイン名</td>
</tr><tr>
<td>CNAME</td>
<td>CNAME解決状況</td>
</tr><tr>
<td rowspan=2>ストリームステータスチェック</td>
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
<td>認証マスターkey</td>
</tr><tr>
<td>認証スレーブkey</td>
</tr><tr>
<td rowspan=6>プッシュ/再生認証</td>
<td>認証に成功/認証に失敗</td>
</tr><tr>
<td>失敗の原因</td>
</tr><tr>
<td>認証するStreamnNme</td>
</tr><tr>
<td>txSecret：プッシュ認証を有効にした後に発行される認証文字列</td>
</tr><tr>
<td>txTime：プッシュアドレス設定のタイムスタンプ</td>
</tr><tr>
<td>URLの実際の期限</td>
</tr><tr>
<td rowspan=4>帯域幅チェックにアクセス</td>
<td rowspan=2>ネットワーク帯域幅の制限の設定</td>
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
<li/>モバイルプッシュ： <a href="https://intl.cloud.tencent.com/document/product/1071/38147">TCToolkit App</a> をダウンロードしてインストールし，RTMPプッシュを選択してください
<li/>モバイル端末再生： <a href="https://intl.cloud.tencent.com/document/product/1071/38147">TCToolkit App</a>をダウンロードしてインストールし ，標準ライブストリーミング再生を選択してください</td>
</tr><tr>
<td>IP制限セルフチェック </td>
<td>IPブラックリスト/ホワイトリスト、IPリージョン制限をチェックし、IP制限による異常を排除します</td>
</tr><tr>
<td>ストリームデータの監視</td>
<td>CSSストリームのリアルタイムモニタリングデータを分析し，ネットワークの輻輳やジッター等の現象による異常があるかどうかの判断を <a href="https://console.cloud.tencent.com/live/analysis/stream">ストリームデータ</a>で確認します。</td>
</tr>
</tbody></table>


>? チェック報告で問題を解決できない場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)か、あるいはTencent Cloudの技術者にお問い合わせの上、問題を特定することをお勧めします。
