
## シナリオ

ストリーム切断診断により、迅速にライブストリーミングのプッシュストリーム切断の記録を確認し、ストリーム切断の原因を特定できます。

## 前提条件
-  [CSSコンソール](https://console.cloud.tencent.com/live)にログイン済みであること。
- 現在Tencent Cloudアカウントにおいて、ライブストリーミングのプッシュに中断が発生していること。

## 操作手順

ライブストリーミングのプッシュ中断後、左側メニューバーから【イベントセンター】>【[ストリーム切断記録](https://console.cloud.tencent.com/live/tools/streamevent)】を選択し、ストリーム切断診断に入ります。
![](https://main.qcloudimg.com/raw/169c385baadcf5d7c4e6f3c9edc06722.png)


そのうち：
- **パス**：プッシュアドレスの中のAppName。
- **ストリーム名**：プッシュアドレスの中のStreamName。

**ストリーム切断エラーコードおよび対応するエラー原因は下表をご参照ください。**：

<table border='0' >
 <col >
 <col >
 <tr >
<th colspan='2' >エラーコード</td>
<th >エラー原因</td>
 </tr>
 <tr >
<td colspan='2' >0</td>
<td >不明なエラー。</td>
 </tr>
 <tr >
<td colspan='2' >1</td>
<td >プッシュクライアントが自動的にストリームを切断しました。</td>
 </tr>
 <tr >
<td colspan='2' >2</td>
<td >プッシュクライアントが自動的にストリームを切断しました。</td>
 </tr>
 <tr >
<td colspan='2' >3</td>
<td>プッシュクライアントが自動的にストリームを切断しました。</td>
 </tr>
 <tr >
<td colspan='2' >4</td>
<td >プッシュクライアントが自動的にストリームを切断しました。</td>
 </tr>
 <tr>
<td colspan='2' >5</td>
<td >CSSシステム内部エラー。</td>
 </tr>
 <tr >
<td colspan='2' >6</td>
<td >RTMPプロトコルコンテンツ異常。</td>
 </tr>
 <tr >
<td colspan='2' >7</td>
<td >RTMP単独のフレームサイズが設定で許可する最大値を超えています。</td>
 </tr>
 <tr >
<td colspan='2' >8</td>
<td >システムが長時間データのないプッシュを自動的に切断しました。</td>
 </tr>
 <tr>
<td colspan='2' >9</td>
<td  >CSSシステム内部エラー。</td>
 </tr>
 <tr >
<td colspan='2'  >10</td>
<td  >プロキシレイヤーがストリーム切断のコマンドを受信しました。</td>
 </tr>
 <tr >
<td colspan='2'  >11</td>
<td  >CSSシステム内部エラー。</td>
 </tr>
 <tr >
<td colspan='2'  >12</td>
<td  >プッシュ接続ネットワークの異常。</td>
 </tr>
 <tr  >
<td colspan='2'  >13</td>
<td  >プッシュ接続ネットワークの異常。</td>
 </tr>
 <tr >
<td colspan='2'  >14</td>
<td  >プッシュ接続ネットワークの異常。</td>
 </tr>
 <tr >
<td colspan='2'  >15</td>
<td  >プッシュ接続ネットワークの異常。</td>
 </tr>
 <tr  >
<td colspan='2'  >16</td>
<td  >CSSシステム内部エラー</td>
 </tr>
 <tr >
<td colspan='2'  >17</td>
<td  >プッシュ接続ネットワークの異常。</td>
 </tr>
 <tr  >
<td rowspan='27'>18</td>
<td>100</td>
<td  >CSSシステム内部エラー。</td>
 </tr>
 <tr >
<td >101</td>
<td  >CSSシステム内部エラー。</td>
 </tr>
 <tr  >
<td >102</td>
<td  >CSSシステム内部エラー。</td>
 </tr>
 <tr  >
<td >103</td>
<td  >CSSシステム内部エラー</td>
 </tr>
 <tr >
<td >104</td>
<td  >CSSシステム内部エラー。</td>
 </tr>
 <tr >
<td >200</td>
<td  >プッシュ接続先に対応するクライアント情報の取得に失敗しました。</td>
 </tr>
 <tr >
<td >201</td>
<td  >あなたのCSSサービスは停止されています。</td>
 </tr>
 <tr  >
<td>202</td>
<td  >アカウントの支払い延滞により、あなたのCSSサービスは一時停止されています。速やかにチャージしてください。</td>
 </tr>
 <tr>
<td >203</td>
<td  >あなたのCSSサービスは強制的に停止されました。</td>
 </tr>
 <tr>
<td >300</td>
<td  >IPアドレスを直接使用したプッシュは許可されていません。</td>
 </tr>
 <tr >
<td >301</td>
<td  >プッシュドメイン名を識別できません。</td>
 </tr>
 <tr >
<td >302</td>
<td  >不正なプッシュドメイン名です。</td>
 </tr>
 <tr >
<td >303</td>
<td  >プッシュドメイン名の使用が禁止されています。</td>
 </tr>
 <tr >
<td >304</td>
<td  >プッシュアプリケーション名の使用が禁止されています。</td>
 </tr>
 <tr>
<td >305</td>
<td  >プッシュストリーム名が再生禁止の状態です。</td>
 </tr>
 <tr >
<td>306</td>
<td  >アクセスモードはチャネルモードですが、対応するプッシュチャネルが作成されていません。</td>
 </tr>
 <tr >
<td >307</td>
<td  >アクセスモードはチャネルモードですが、プッシュチャネルが現在無効になっています。</td>
 </tr>
 <tr >
<td >308</td>
<td  >プッシュストリーム名に不正な文字が含まれています。</td>
 </tr>
 <tr >
<td>309</td>
<td  >プッシュアプリケーション名に不正な文字が含まれています。</td>
 </tr>
 <tr  >
<td >400</td>
<td  >プッシュクライアント IP がブラックリストに掲載されています。</td>
 </tr>
 <tr >
<td >401</td>
<td  >プッシュクライアント IPがホワイトリストに掲載されていません。</td>
 </tr>
 <tr  >
<td>500</td>
<td  >プッシュに期限切れ時間のパラメータがついていません。</td>
 </tr>
 <tr >
<td >501</td>
<td  >期限切れ時間のパラメータの期限が過ぎています。</td>
 </tr>
 <tr  >
<td>502</td>
<td  >プッシュに認証パラメータがついていません。</td>
 </tr>
 <tr  >
<td >503</td>
<td  >認証パラメータの検証に失敗しました。</td>
 </tr>
 <tr  >
<td>600</td>
<td  >現在のプッシュ数が設定で許可する最大値を超えています。</td>
 </tr>
 <tr >
<td >601</td>
<td  >現在のストリーム名に対応するプッシュ数が設定で許可する最大値を超えています。</td>
 </tr>
 <tr >
<td colspan='2'  >19</td>
<td  >第三者認証に失敗しました。</td>
 </tr>
 <tr >
<td colspan='2'  >20</td>
<td  >システムが長時間データのないプッシュを自動的に切断しました。</td>
 </tr>
 <tr >
<td rowspan='3'>21</td>
<td >100</td>
<td  >クライアントが呼び出したストリーム切断のリクエストを受信しました。</td>
 </tr>
 <tr >
<td>101</td>
<td  >クライアントが呼び出した配信禁止のリクエストを受信しました。</td>
 </tr>
 <tr >
<td >102</td>
<td  >新規プッシュ接続を受信し、現在のプッシュと置き換えます。</td>
 </tr>
 <tr  >
<td colspan='2'  >22</td>
<td  >原因不明。</td>
 </tr>
 <tr >
<td colspan='2'  >23</td>
<td  >RTMPのプロトコルコンテンツ異常。</td>
 </tr>
 <tr >
<td colspan='2'  >24</td>
<td  >CSSシステム内部エラー。</td>
 </tr>
 <tr >
<td colspan='2'  >25</td>
<td  >原因不明。</td>
 </tr>
 <tr >
<td colspan='2'  >26</td>
<td  >原因不明。</td>
 </tr>
 <tr >
<td colspan='2'  >27</td>
<td  >原因不明。</td>
 </tr>
 <tr  >
<td colspan='2'  >28</td>
<td  >原因不明。</td>
 </tr>
 <tr >
<td colspan='2'  >29</td>
<td  >原因不明。</td>
 </tr>
 <tr  >
<td colspan='2'  >30</td>
<td  >原因不明。</td>
 </tr>
 <tr>
<td colspan='2'  >31</td>
<td  >原因不明。</td>
 </tr>
 <tr>
<td colspan='2'  >32</td>
<td  >原因不明。</td>
 </tr>
 <tr  >
<td colspan='2'  >33</td>
<td  >RTMP AMF データ異常。</td>
 </tr>
 <tr>
<td colspan='2'  >34</td>
<td  >原因不明。</td>
 </tr>
 <tr >
<td colspan='2'  >35</td>
<td  >プッシュクライアントが自動的にストリームを切断しました。</td>
 </tr>
</table>

CSSでは、クエリーを行うAPIインターフェースも提供しています。詳細については、[プッシュストリーム切断イベントのクエリー](https://intl.cloud.tencent.com/document/product/267/30800)をご参照ください。

