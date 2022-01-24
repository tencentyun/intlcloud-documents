Tencent Cloud CSSは、ストリーム切断診断により、CSSのプッシュ切断ストリームの記録を迅速に確認し、ストリーム切断の原因を特定します。

## 前提条件
- [CSSコンソール](https://console.cloud.tencent.com/live)にログイン済みであること。
- 現在Tencent Cloudアカウントにおいて、CSSストリームのプッシュに中断が発生していること。

## 操作手順

CSSプッシュの中断後、左側のメニューバーの【イベントセンター】>【[ストリーム切断記録](https://console.cloud.tencent.com/live/tools/streamevent
)】を選択して、ストリーム切断診断に進みます。
![](https://qcloudimg.tencent-cloud.cn/raw/7109f254ed3f4c892bd93632d9f04629.png)

そのうち：
- **パス**：プッシュアドレスの中のAppName。
- **ストリーム名**：プッシュアドレスの中のStreamName。

[](id:erro_code)
## ストリーム切断エラーコード
ストリーム切断エラーコードおよび対応するエラー原因は下表をご参照ください。 

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
<td >ライブストリーミングシステム内部のエラー。</td>
 </tr>
 <tr >
<td colspan='2' >6</td>
<td >RTMPプロトコルのコンテンツ異常。</td>
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
<td  >ライブストリーミングシステム内部のエラー。</td>
 </tr>
 <tr >
<td colspan='2'  >10</td>
<td  >プロキシレイヤーがストリーム切断のコマンドを受信しました。</td>
 </tr>
 <tr >
<td colspan='2'  >11</td>
<td  >ライブストリーミングシステム内部のエラー。</td>
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
<td  >ライブストリーミングシステム内部のエラー</td>
 </tr>
 <tr >
<td colspan='2'  >17</td>
<td  >プッシュ接続ネットワークの異常。</td>
 </tr>
 <tr  >
<td rowspan='27'>18</td>
<td>100</td>
<td  >ライブストリーミングシステム内部のエラー。</td>
 </tr>
 <tr >
<td >101</td>
<td  >ライブストリーミングシステム内部のエラー。</td>
 </tr>
 <tr  >
<td >102</td>
<td  >ライブストリーミングシステム内部のエラー。</td>
 </tr>
 <tr  >
<td >103</td>
<td  >ライブストリーミングシステム内部のエラー</td>
 </tr>
 <tr >
<td >104</td>
<td  >ライブストリーミングシステム内部のエラー。</td>
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
<td  >あなたのCSSサービスは強制的に停止されています。</td>
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
<td  >プッシュドメイン名が合法ではありません。</td>
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
<td  >アクセスモードはチャネルモードですが、現在プッシュチャネルはすでに停止されています。</td>
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
<td  >プッシュクライアントIPがブラックリストに掲載されています。</td>
 </tr>
 <tr >
<td >401</td>
<td  >プッシュクライアントIPがホワイトリストに掲載されていません。</td>
 </tr>
 <tr  >
<td>500</td>
<td  >プッシュは有効期限パラメータを有していません。</td>
 </tr>
 <tr >
<td >501</td>
<td  >有効期限パラメータ値がすでに期限切れです。</td>
 </tr>
 <tr  >
<td>502</td>
<td  >プッシュは認証パラメータを有していません。</td>
 </tr>
 <tr  >
<td >503</td>
<td  >認証パラメータの検証をパスしていません。</td>
 </tr>
 <tr  >
<td>600</td>
<td  >現在のプッシュ数が設定で許される最大値を超えています。</td>
 </tr>
 <tr >
<td >601</td>
<td  >現在のストリーム名に対応するプッシュ数が設定で許される最大値を超えています。</td>
 </tr>
 <tr >
<td colspan='2'  >19</td>
<td  >サードパーティ認証のエラー。</td>
 </tr>
 <tr >
<td colspan='2'  >20</td>
<td  >システムが長時間データのないプッシュを自動的に切断しました。</td>
 </tr>
 <tr >
<td rowspan='3'>21</td>
<td >100</td>
<td  >顧客が呼び出したストリーム切断リクエストを受信しました。</td>
 </tr>
 <tr >
<td>101</td>
<td  >顧客が呼び出した再生禁止リクエストを受信しました。</td>
 </tr>
 <tr >
<td >102</td>
<td  >新しいプッシュを受信し、現在のプッシュに切り替え接続しました。</td>
 </tr>
 <tr  >
<td colspan='2'  >22</td>
<td  >原因不明。</td>
 </tr>
 <tr >
<td colspan='2'  >23</td>
<td  >RTMPプロトコルのコンテンツ異常。</td>
 </tr>
 <tr >
<td colspan='2'  >24</td>
<td  >ライブストリーミングシステム内部のエラー。</td>
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

CSSではクエリー用のAPIインターフェースも用意しています。詳細は[プッシュストリーム切断イベントのクエリー](https://intl.cloud.tencent.com/document/product/267/30800)をご参照ください。
