## 2022年08月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="44%">ダイナミック説明</th><th width="15%">リリース時期</th><th width="21%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 6.6.3002拡張版をリリース</td>
    <td><ul style="margin:0">
    <li> ライブストリーミンググループのメンバーをタグ付けすることをサポートします </li>
    <li> ライブストリーミンググループからメンバーを追放することをサポートします </li>
    <li> Androidトピック更新のコールバックでたまに発生するクラッシュの問題を修正しました </li>
    <li> グループ参加オプション変更の通知列挙値が正しくない問題を修正しました </li> 
    <li> トピックにカスタムフィールドが設定された後、onTopicInfoChangedのリッスンコールバックが受信されない問題を修正しました </li>     
    <li> AndroidでネットワークIPを何度も取得する問題を最適化しました </li>
    <li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>    
        </ul></td>
    <td> 2022-08-18 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr> 
<tr>
    <td> SDK 2.22.0をリリースしました（ミニプログラムとWeb端末）</td>
<td data-sheets-value="" ><li>uni-appでnative appへのパッケージ化時にオフライン配信を使用することをサポートします。<a  target="_blank" href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#registerPlugin">registerPlugin</a>をご参照ください。<br>
<li>ライブストリーミンググループのオンラインメンバーリストを取得することをサポートします。<a  target="_blank" href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getGroupMemberList">getGroupMemberList </a>（Ultimate Editionが必要）をご参照ください。<br>
<li>ライブストリーミンググループのメンバーブロックをサポートします。<a  target="_blank" href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#deleteGroupMember">deleteGroupMember</a>（Ultimate Editionが必要）をご参照ください。<br>
<a  target="_blank" href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setConversationCustomData"><li>setConversationCustomData</a>でセッションカスタムデータを設定します。<li>他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34281">更新ログ</a>をご参照ください</td></td>
    <td> 2022-08-18 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
<tr>
    <td> SDK 2.21.1をリリースしました（ミニプログラムとWeb端末）</td>
    <td>
<li><a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#resendMessage">resendMessage</a>、発生する可能性があるメッセージ重複問題。</li>
<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34281">更新ログ</a>をご参照ください</td>
    <td> 2022-08-03 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
</table>

## 2022年07月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="44%">ダイナミック説明</th><th width="15%">リリース時間</th><th width="21%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 6.5.2816拡張版をリリース</td>
    <td><ul style="margin:0">
    <li> インドサイトのルート選択ポリシーを最適化しました </li>
    <li> リッチ・メディア・メッセージのアップロード/ダウンロード進行状態のコールバックを最適化しました </li>
    <li> Android端末でデバイスのプロセス情報を取得するときのコンプライアンス問題を最適化します </li>
    <li> トピックを連続して作成するときのcrashの問題を修正しました </li> 
    <li> Windowsでパケットを送信するときのcrash問題を修正しました </li>     
    <li> Android v7aアーキテクチャーで友達をブラックリストに追加して、もう一度ブラックリストに載っている友達を登録するときのcrash問題を修正しました </li>
    <li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>    
        </ul></td>
    <td> 2022-07-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr> 
<tr>
    <td> SDK 2.21.0をリリースしました（ミニプログラムとWeb端末）</td>
    <td>
<li><a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setSelfStatus">setSelfStatus</a>で、自分のカスタマイズ状態を設定します</li>
<li><a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getUserStatus">getUserStatus</a>でユーザー状態を問い合わせます</li>
<li><a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#subscribeUserStatus">subscribeUserStatus</a>、サブスクリプションユーザー状態</li>
<li><a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#unsubscribeUserStatus">unsubscribeUserStatus</a>でサブスクリプションユーザー状態を取り消します</li>
<li><a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setMessageRemindType">setMessageRemindType</a>がグループメッセージやトピックメッセージの着信通知なし設定の多端末、多インスタンス同期をサポートします</li>
<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34281">更新ログ</a>をご参照ください</td>
    <td>	2022/07/28	</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
<tr>
    <td> SDK 6.5.2803拡張版をリリース</td>
    <td><ul style="margin:0">
	<li><a href="https://intl.cloud.tencent.com/document/product/1047/48853">セッションタグ</a>へのサポートを追加しました
	<li><a href="https://intl.cloud.tencent.com/document/product/1047/48854">セッショングループ化</a>へのサポートを追加しました
	<li> セッションのカスタムフィールドへのサポートを追加しました </li>
	<li><a href="https://cloud.tencent.com/document/product/269/75366#.E8.8E.B7.E5.8F.96.E4.BC.9A.E8.AF.9D.E5.88.97.E8.A1.A8.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3">セッションプル用ハイレベルインターフェースを追加しました</a>    
	<li> ライブストリーミンググループメッセージ受信をサポートします </li> 
	<li> グループ参加オプション変更の通知送信をサポートします </li>     
	<li> グループメッセージ受信オプション変更の多端末同期をサポートします </li>
	<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>    
    </ul></td>
    <td> 2022-07-15 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>
</table>



## 2022年06月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="44%">ダイナミック説明</th><th width="15%">リリース時間</th><th width="21%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 6.3.2619拡張版をリリース</td>
    <td><ul style="margin:0">
	<li>トピックリストを取得するときにクラッシュが偶発的に発生するという問題を修正しました</li>
	<li>トピック削除後のセッションリストの取得エラーを修正しました</li>
    </ul></td>
    <td> 2022-06-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>
<tr>
    <td>SDK 2.20.1をリリースしました（Web端末）</td>
    <td><li>非ライブ配信グループを終了するか非ライブ配信グループから削除される、または非ライブ配信グループが解散されると、グループ履歴のみが削除され、対応するグループセッションは削除されません。nativeに合わせて同じような体験が提供されます。</li><li><a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage">deleteMessage</a>は、グループシステム通知の削除をサポートしていません。また、具体的なエラーメッセージが返されます。</li><li>プライベートにデプロイされたリッチメディアメッセージはHTTPプロトコルをサポートします</li><li>C2CセッションlastMessageが異常に更新されるという問題を修正しました</li></td>
    <td> 2022-06-27 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
<tr>
    <td> SDK 6.3.2609拡張版をリリース</td>
    <td><ul style="margin:0">
	<li>オンラインステータスとカスタムステータスを追加しました</li>
	<li>ライブ配信グループは、グループメンバー（最大1000人まで）リストのプルをサポートするようになりました</li>
	<li>トピックはat allメッセージをサポートするようになりました</li>
	<li>クロスプラットフォームバージョンのsql実行エラーを修正しました</li> 
	<li>クロスプラットフォームSDKの、コミュニティトピック関連のインターフェースを追加しました</li>
	<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>
    </ul></td>
    <td>2022/06/16</td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>
<tr>
    <td>SDK 2.20.0をリリースしました（Web端末）</td>
    <td><ul style="margin:0">
<li><a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#modifyMessage">modifyMessage</a>は、メッセージの変更をサポートするようになりました
<li><a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageListHopping">getMessageListHopping</a>は、指定されたメッセージsequenceまたはメッセージ時間によってセッションのメッセージリストをプルすることをサポートするようになりました
<li>単一または複数のC2Cメッセージの開封確認の送信をサポートするようになりました（Ultimate Editionを有効にしてください）
<li>C2CセッションlastMessageで、対向側がメッセージを開封したかどうかを識別するために使用されるフィールドisPeerReadを追加しました<li>更新内容の詳細については、<a href="https://cloud.tencent.com/document/product/269/38492">変更ログ</a></li>をご参照ください
    </ul></td>
    <td> 2022-06-09 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
</table>


## 2022年05月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="44%">ダイナミック説明</th><th width="15%">リリース時間</th><th width="21%">関連ドキュメント</th>
</tr> 
<tr>
    <td>SDK 2.19.0をリリースしました（Web端末）</td>
    <td><ul style="margin:0">
<li><a href="https://intl.cloud.tencent.com/document/product/1047/33529">コミュニティ（Community）</a>の下でのトピックの作成をサポートし、よりインタラクティブなシナリオをサポートできるようになりました</li>
<li><a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getJoinedCommunityList">getJoinedCommunityList</a>では、トピックをサポートするコミュニティのリストを取得できるようになりました</li>
<li><a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTopicInCommunity">createTopicInCommunity</a>では、トピックを作成できるようになりました</li>
<li><a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteTopicFromCommunity">deleteTopicFromCommunity</a>では、トピックを削除できるようになりました</li>
<li><a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateTopicProfile">updateTopicProfile</a>では、トピックデータを設定できるようになりました</li>
<li><a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTopicList">getTopicList</a>では、トピックリストを取得できるようになりました</li>
<li><a href="https://web.sdk.qcloud.com/im/doc/en/Topic.html">Topic</a>：コミュニティのトピック対象であり、名称、お知らせ、概要、未読数などの情報を含むトピックのプロパティを説明するためのものです</li>
<li>イベント<a href="https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_CREATED">TIM.EVENT.TOPIC_CREATED</a>は、トピックの作成時にトリガーされます</li>
<li>イベント<a href="https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_DELETED">TIM.EVENT.TOPIC_DELETED</a>は、トピックの削除時にトリガーされます</li>
<li>イベント<a href="https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_UPDATED">TIM.EVENT.TOPIC_UPDATED</a>は、トピックデータの更新時にトリガーされます</li></li>
    </ul></td>
    <td> 2022-05-07 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
</table>

## 2022年04月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="44%">ダイナミック説明</th><th width="15%">リリース時間</th><th width="21%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 6.2.2363拡張版をリリース</td>
    <td><ul style="margin:0">
	<li>コミュニティトピック機能を追加しました</li>
	<li>メッセージ編集インターフェースを追加しました</li>
	<li>C2Cメッセージの開封確認をサポートするようになりました</li>
	<li>国際サイトのネットワーク品質を最適化しました</li> 
	<li>メッセージ既読後、アンインストールして再インストールし、当該メッセージをプルすると、既読ステータスが未読になるという問題を修正しました</li>
	<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>
    </ul></td>
    <td> 2022-04-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>
<tr>
    <td> SDK 2.18.2をリリースしました（ミニプログラムとWeb端末）</td>
    <td><ul style="margin:0">
<li>ライブ配信グループのユーザー体験を最適化しました</li><li>一部のシナリオにおける不正確な統計の問題を修正しました</li><li>呼び出しインターフェース<a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList">getGroupMessageReadMemberList</a>が不正確な結果を戻す問題を修正しました<li>更新内容の詳細については、<a href="https://intl.cloud.tencent.com/document/product/1047/34281">更新ログ</a></li>をご参照ください
    </ul></td>
    <td> 2022-04-22 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
<td>Flutter SDK 3.9.3</td>
<td><ul style="margin:0">
  <li>発言禁止のグループのtips boolValueが失われたという問題を修正しました
    <ul>
      <li>現在、グループ情報変更のコールバックによって返されるデータは、key(string)-value(string)の形式であり、key(string)-boolValue(bool)の形式が新しく追加されています</li>
    </ul>
  </li>
  <li>セッションインスタンスでnameCardフィールドが解析されていないという問題を修正しました
  <li>グループ開封確認関連のインターフェースを追加しました
    <ul>
      <li><a href="https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html">sendMessageReadReceptes</a>では、グループメッセージの開封確認を送信できるようになりました</li>
      <li><a href="https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html">getMessageReadReceptes</a>では、自分から送信したメッセージの開封確認を取得できるようになりました</li>
      <li><a href="https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html">getgroupMessageReadMemeberList</a>では、自分から送信したグループメッセージの既読（未読）グループメンバーリストを取得できるようになりました</li>
    </ul>
  </li>
  <li>Flutter for Webを最適化しました
</ul>
</td>
<td>2022-04-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
<tr>
    <td> SDK 2.18.0をリリースしました（ミニプログラムとWeb端末）</td>
    <td><ul style="margin:0">
<li>グループメッセージの開封確認を送信するための<a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessageReadReceipt">sendMessageReadReceptes</a>を追加しました</li>
<li>グループメッセージの開封確認リストをプルするための<a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageReadReceiptList">getMessageReadReceiptList</a>を追加しました</li>
<li>グループメッセージの既読（未読）グループメンバーリストをプルするための<a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList">getGroupMessageReadMemberList</a>を追加しました</li>
<li>messageIDに基づいてセッションのローカルメッセージを検索するための<a href="https://web.sdk.qcloud.com/im/doc/en/SDK.html#findMessage">findMessage</a>を追加しました。
メッセージが取り消された後、NativeIMに合わせて同じようなセッション未読数の変更体験が提供される機能を追加しました</li><li>更新内容の詳細については、<a href="https://intl.cloud.tencent.com/document/product/1047/34281">更新ログ</a></li>をご参照ください
    </ul></td>
    <td> 2022-04-08 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>



<tr>
    <td> SDK 6.1.2166拡張版をリリース</td>
    <td><ul style="margin:0">
	<li> ローカルメッセージを検索し、senderUserIDListを2つ以上渡す場合にデータが見つからないという問題を修正しました</li>
	<li> rest apiで一度に複数のメッセージを取り消したが、Android sdkで1件だけコールバックしたという問題を修正しました</li>
	<li> Windowsで未読のクイッククリア時の偶発クラッシュ問題を修正しました</li>
	<li> 国際版体験Demoをリリースしました</li>
	<li> Demoのオフラインプッシュをメーカーコネクションに切り替えました</li>
	<li> Demoの携帯電話番号登録がaPaasに切り替わりました</li>
	<li> オーディオビデオ通話の複数端末同期の問題を修正しました</li>
    </ul></td>
    <td> 2022-04-02 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>
</table>



## 2022年03月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="44%">ダイナミック説明</th><th width="15%">リリース時間</th><th width="21%">関連ドキュメント</th>
</tr> 
<tr>
<td>Flutter SDK 3.9.1</td>
<td><ul style="margin:0;">
<li>下層データベースを6.1.2155にアップグレードしました
</ul></td>
<td>2022-03-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.9.0</td>
<td><ul style="margin:0;">
<li>grouplistenerの修正
</ul></td>
<td>2022-03-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.8.9</td>
<td><ul style="margin:0;">
<li>リスニング登録問題の修正
</ul></td>
<td>2022-03-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.8.4</td>
<td><ul style="margin:0;">
<li>interfaceの更新
</ul></td>
<td>2022-03-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
    <td> SDK 6.1.2155拡張版をリリース</td>
    <td><ul style="margin:0">
        <li> グループメッセージの開封確認（<a href="https://intl.cloud.tencent.com/document/product/1047/36360#.E7.BE.A4.E6.B6.88.E6.81.AF.E5.B7.B2.E8.AF.BB.E5.9B.9E.E6.89.A7">iOSドキュメント</a>、<a href="https://intl.cloud.tencent.com/document/product/1047/36359#.E7.BE.A4.E6.B6.88.E6.81.AF.E5.B7.B2.E8.AF.BB.E5.9B.9E.E6.89.A7">Androidドキュメント</a>）をサポートしました </li>
	<li> Androidオフラインプッシュで音声通知設定をサポートしました</li>
	<li> モバイル側SDKでネットワークプロキシーを設定するためのインターフェースを提供します</li>
	<li> C/C++プラットフォームでオフラインプッシュのインターフェースを補完しました</li>
	<li> ログイン後のグループ内シグナリングメッセージの自動同期をサポートしました</li>
	<li> 友達のカスタムフィールドの変更通知を受信した後、完全なカスタムフィールドを取得できない問題を修正しました</li>
	<li> 脆弱なネットワークでセッションリストをドロップダウンするときの偶発的な応答不可フラグ返しエラーの問題を修正しました</li>
	<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>
    </ul></td>
    <td> 2022-03-18 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>
<tr>
<td>Flutter SDK 3.8.4</td>
<td><ul style="margin:0;">
<li>interfaceの更新
</ul></td>
<td>2022-03-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
    <td> SDK 2.17.0をリリースしました（ミニプログラムとWeb端末）</td>
    <td><ul style="margin:0">
       <li>コミュニティ<a href="https://intl.cloud.tencent.com/document/product/1047/33529">がサポートされました</a></li>
<li>最近使用した連絡先`Conversation.lastMessage`はグループ通知メッセージをサポートしました</li>
<li>`Message.payload.memberList`はグループ参加またはグループ退出を行うグループメンバーのニックネーム、プロファイルフォトなどの情報の取得をサポートしました</li>
<li>画像メッセージの送信にはwebp形式の画像がサポートされます</li><li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34281">更新ログ</a>をご参照ください</li>
    </ul></td>
    <td> 2022-03-02 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
</tr> 
<tr>
<td>Flutter SDK 3.8.3</td>
<td><ul style="margin:0;">
<li>環境によってtokenコードを切り替えます
</ul></td>
<td>2022-03-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
</table>

## 2022年02月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="44%">ダイナミック説明</th><th width="15%">リリース時間</th><th width="21%">関連ドキュメント</th>
</tr>
<tr>
<td>Flutter SDK 3.8.2</td>
<td><ul style="margin:0;">
<li>グループメンバーパラメータの制約を更新しました
</ul></td>
<td>2022-02-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.8.0</td>
<td><ul style="margin:0;">
<li>下層データベースのinterface依存関係を更新しました
</ul></td>
<td>2022-02-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.7.8</td>
<td><ul style="margin:0;">
<li>強制解凍による異常を修正しました
</ul></td>
<td>2022-02-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
    <td> SDK 2.16.3をリリースしました（ミニプログラムとWeb端末）</td>
    <td><ul style="margin:0">
        <li> WindowsのWeChatアクセス用ミニプログラムとuni-appでAndroid app（一部デバイス）をパッケージ化した後にログインできない問題を修正しました
    </ul></td>
    <td> 2022-02-11 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
</tr> 
<tr>
    <td> SDK 2.16.2をリリースしました（ミニプログラムとWeb端末）</td>
    <td><ul style="margin:0">
        <li> uni-appでnative appをパッケージ化した後にファイルメッセージを送信することがサポートされるようになりました</li>
        <li> インドインターナショナルステーションをサポートしました</li>
				        <li>一部のemoji絵文字のレンダリング問題を修正しました</li>
    </ul></td>
    <td> 2022-02-10 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.7.7</td>
<td><ul style="margin:0;">
<li>Swiftコードのwarningを修正しました                        </li><li>Swiftの強制解凍コードを上書きしました                          </li><li>sendMessageインターフェースから返されたmessageインスタンスにidフィールドを追加しました  </li>
</ul></td>
<td>2022-02-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
    <td> SDK 6.0.1992拡張版をリリースしました</td>
    <td><ul style="margin:0">
        <li> 解散したグループまたは存在しないグループに2回連続してメッセージを送信するときの偶発的なcrash問題を修正しました</li>
    </ul></td>
    <td> 2022-02-09 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>
</table>

## 2022年01月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="44%">ダイナミック説明</th><th width="15%">リリース時間</th><th width="21%">関連ドキュメント</th>
</tr> 
<tr>
    <td> TUIKit 6.0.1992の拡張版をリリースしました</td>
    <td><ul style="margin:0">
        <li> スキン設定機能を新たに追加しました</li>
    	<li> 言語設定機能を新たに追加しました</li>
	<li> グループプロファイルカードのグループ管理機能を新たに追加しました</li>
	<li> ファイルメッセージにアップロードとダウンロードのアニメーションを追加しました</li>
        <li> 履歴メッセージを閲覧する際に、「新しいメッセージをX件受信した」という小さな舌のリダイレクトを追加しました</li>
	<li> 履歴メッセージを閲覧する際に、「最新の位置に戻る」という小さな舌のリダイレクトを追加しました</li>
	<li> グループ内の@メッセージをクイックリダイレクトするという小さな舌のリダイレクトを追加しました</li>
	<li> セッションリストの最後のメッセージの表示スタイルを最適化しました</li>
    <li> テキストメッセージの選択済み状態を追加しました</li>
	<li> A2、D2エラー通知の説明を最適化しました</li>
	<li> iOS 15システムのUI対応</li>
    </ul></td>
    <td> 2022-01-25 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>
<tr>
<td>Flutter SDK 3.7.5</td>
<td><ul style="margin:0;">
<li> 下層データベースを6.0.1975にアップグレードしました
<li> オフラインプッシュの設定でTPNS TOKENをサポートしました
</ul></td>
<td>2022-01-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
    <td> SDK 6.0.1975拡張版をリリースしました</td>
    <td><ul style="margin:0">
        <li> 全プラットフォームC++インターフェース版SDKをリリースしました</li>
    	<li> オフラインプッシュでTPNSコネクションへのアクセスをサポートしました</li>
	<li> パーソナルプロファイルカスタムフィールドの変更通知を追加しました</li>
	<li> フレンドノート取得時に偶発的にブランクになる問題を修正しました</li>
        <li> ネットワークタイプのログプリントを最適化しました</li>
	<li> iOSバージョンのメッセージオブジェクトにメッセージ優先度priorityフィールドを補完しました</li>
	<li> Cインターフェースバージョンのローカルメッセージを挿入するコールバックが完全なメッセージオブジェクトを返さない問題を修正しました</li>
	<li> 公式TUIKitオープンソースDemoのオフラインプッシュをTPNSコネクションに切り替えました</li>
    </ul></td>
    <td> 2022-01-14 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>

<tr>
<td> SDK 2.16.1をリリースしました（ミニプログラムとWeb端末）</td>
<td><ul style="margin:0;">
<li>Alipayミニプログラムによる.imageサフィックスの画像の送信がサポートされるようになりました                                                                                </li>
<li>セッション削除の同時に履歴メッセージも削除される<a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#deleteConversation">deleteConversation</a>を追加しました   </li>
<li>ダウンリンクメッセージ`fileName`が空白の文字列である場合にエラーが発生する問題を修正しました                                                                          </li>
<li>グループ属性インターフェースを呼び出すときに発生した問題を修正しました                                                                                          </li>
<li>uni-appで百度ミニプログラムなどのプラットフォームにパッケージ化されるときに発生した`__wxConfig is not defined`問題を修正しました                                               </li>
</ul></td>
<td>2022-01-14</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
<tr>
<td>Unity SDK 1.6.4</td>
<td><ul style="margin:0;">
<li>SDKへのpackage manager導入をサポートしました
<li>iOSコンパイル後の依存関係追加を追加しました
</ul></td>
<td>2022-01-13</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.7.1</td>
<td><ul style="margin:0;">
<li> メッセージ送信プログレスイベントで作成したメッセージのidを戻すようにしました
<li> コールバック部分を最適化し、サービス側にコールバックのエラーがSDK中でcatchされ、サービス側に修正の必要があることを通知するようにしました
</ul></td>
<td>2022-01-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.7.0</td>
<td><ul style="margin:0;">
- CloudCustomData解凍を最適化しました
</ul></td>
<td>2022-01-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>

<tr>
<td>Flutter SDK 3.6.9</td>
<td><ul style="margin:0;">
<li>返信メッセージパラメータを最適化しました
</ul></td>
<td>2022-01-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.8</td>
<td><ul style="margin:0;">
<li>返信メッセージインターフェースを最適化しました
</ul></td>
<td>2022-01-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td> SDK 2.16.0をリリースしました（ミニプログラムとWeb端末）</td>
<td><ul style="margin:0;">
<li><a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setMessageRemindType">setMessageRemindType</a>を追加し、C2Cセッションメッセージの応答不可設定をサポートしました             </li>
<li><a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setAllMessageRead">setAllMessageRead</a>を追加し、すべての未読セッションをクイッククリアすることをサポートしました                      </li>
<li><a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#sendMessage">sendMessage</a>を追加し、未読セッションに取り入れず、セッション`lastMessage`を更新しないメッセージを送信することをサポートしました   </li>
<li>ライブブロードキャストグループの新規メンバーがグループに参加する前の履歴メッセージを閲覧することがサポートされるようになりました（フラッグシップ版が必要）                                                                                                 </li>
<li><a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode">厳格なモードを使用するようにSDKを変更しました</a>                                      </li>
<li>削除されたアカウントとのセッションがフィルタリングされるようにセッションリストを変更しました                                                                                                                 </li>
<li>ローミングメッセージを最適化するための`nick`と`avatar`の更新タイミングを変更しました                                                                                                       </li>
<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34281">更新ログ</a>をご参照ください</li>
</ul></td>
<td>2022-01-05</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996#web">Web SDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.7</td>
<td><ul style="margin:0;">
<li>iOSコンパイル環境を8.0から9.0にアップデートしました
</ul></td>
<td>2022-01-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
</table>


## 2021年12月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="44%">ダイナミック説明</th><th width="15%">リリース時間</th><th width="21%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 5.9.1886拡張版をリリースしました</td>
    <td><ul style="margin:0">
        <li> ログインしC2C未読メッセージを同期した後にコールバックされる未読メッセージが不完全であるという問題を修正しました</li>
    	<li> ローカルメッセージのプルが不完全に返される問題を修正しました</li>
	<li> LinuxプラットフォームでのHTTPSリクエストエラーの問題を解決しました</li>
	<li> Cインターフェースバージョンでのフレンドカスタムフィールドを照会できない問題を解決しました</li>
        <li> ネットワーク層のエラーコードの説明を最適化しました</li>
	<li> TUIKit画像ビデオメッセージの表示の左右スライド表示をサポートしました</li>
	<li> TUIKitメッセージの取り消しの再編集をサポートしました</li>
	<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>
    </ul></td>
    <td> 2021-12-31 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>
<tr>
<td>Flutter SDK 3.6.6</td>
<td><ul style="margin:0;">
<li>メッセージに返信インターフェースを追加しました
<li>Web端末のrelease modeでのエラー問題を修正しました
</ul></td>
<td>2021-12-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Unity SDK 1.6.0</td>
<td><li>最下層のクロスプラットフォームcインターフェースを切り替えました</li><li>Windows、macOS、Android、iOSのプラットフォームをサポートし、かつこの四つ端末のインターフェースが一致します</li><li>注意：1.6.0は以前のバーションと互換性がありません</li></td>
<td>	2021/12/21	</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr> 
<tr>
    <td> SDK 5.9.1872拡張版をリリースしました</td>
    <td><ul style="margin:0">
        <li> グループ内のダイレクトメッセージ送信をサポートしました</li>
    	<li> cosダウンロード認証をサポートしました</li>
	<li> 長時間接続暗号化コネクションにAESサポートを追加しました</li>
	<li> ネットワーク接続ロジックにアクセスポイントサイロ化解消のサポートを追加しました</li>
        <li> cosファイルのアップロード/ダウンロード同時実行数のバックグランド設定をサポートしました</li>
	<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>
    </ul></td>
    <td> 2021-12-20 </td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.5</td>
<td><ul style="margin:0;">
<li>java文法エラーを修正しました
</ul></td>
<td>2021-12-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.4</td>
<td><ul style="margin:0;">
<li>Androidの非同期登録イベントが何も返されないbugを修正しました
<li>ベースリスニングイベントが削除されるとエラーが発生する問題を修正しました
<li>メッセージプログレスイベントに送信中のメッセージのuuidを追加しました
</ul></td>
<td>2021-12-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>

<tr>
    <td> SDK 5.8.1696拡張版をリリースしました</td>
    <td><ul style="margin:0">
        <li> ローカルに解散したグループセッションまたは退出したグループセッションの未読数が含まれる場合に、未読メッセージのクイッククリアに失敗する問題を修復しました</li>
    	<li> TUIKitメッセージ返信機能の追加をサポートしました</li>
	<li> TUIKit デフォルトのスキンを更新、インターフェースロジックを最適化しました</li>
	<li> iOSがリソースファイルのロードに偶発的に失敗する問題を修正</li>
    </ul></td>
    <td> 2021-12-10 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">端末SDKのダウンロード</a> </td>
</tr>
<tr>
<td>Flutter SDK 3.6.3</td>
<td><ul style="margin:0;">
<li>addFriendインターフェースの最適化：addTypeをintからFriendTypeEnumに変更しました
<li>acceptFriendApplicationインターフェースの最適化：acceptTypeをintからFriendResponseTypeEnumに変更しました
<li>getHistoryMessageListインターフェースの最適化：typeをintからHistoryMsgGetTypeEnumに変更しました
	<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/45915">更新ログ</a>をご参照ください</li>
</ul></td>
<td>2021-12-9</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.2</td>
<td><ul style="margin:0;">
<li>高度なメッセージが削除されuuidが渡されないエラーを修正しました
</ul></td>
<td>2021-12-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.1</td>
<td><ul style="margin:0;">
<li>ファイルのプログレスイベントが消失する問題を修正しました
</ul></td>
<td>2021-12-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>
<tr>
<td>Flutter SDK 3.6.0</td>
<td><ul style="margin:0;">
<li>各モジュールでlistenerの複数登録および複数コールバックをサポートしました
<li>すべてのセッションを既読に設定するapiのmarkAllMessageAsReadを追加しました
<li>組み合わせメッセージ解析を追加しました
<li>nativeのバージョンを5.8.1668にアップデートしました
</ul></td>
<td>2021-12-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996#opensource">フレームワークSDKのダウンロード</a></td>
</tr>

</table>

## 2021年12月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 5.8.1696拡張版をリリース</td>
    <td><ul style="margin:0">
        <li> ローカルに解散したグループセッションまたは退出したグループセッションの未読数が含まれる場合に、未読メッセージのクイッククリアに失敗する問題を修復</li>
    	<li> TUIKitメッセージ返信機能の追加をサポート</li>
	<li> TUIKit デフォルトのスキンを更新、インターフェースロジックを最適化</li>
	<li> iOSがリソースファイルのロードに偶発的に失敗する問題を修正</li>
    </ul></td>
    <td> 2021-12-10 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>

## 2021年11月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 5.8.1672拡張版をリリース</td>
    <td><ul style="margin:0">
        <li> コンプライアンス要件を満たすためデバイス情報取得ロジックを最適化</li>
    	<li> 未読数クイッククリア機能の特定条件下での崩壊問題を修復</li>
    </ul></td>
    <td> 2021-11-30 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.8.1668拡張版をリリース</td>
    <td><ul style="margin:0">
        <li> 全セッションの未読メッセージクイッククリア機能を追加</li>
    	<li> Communityコミュニティのサポートを追加、コミュニティは最大10万人をサポート、フラッグシップ版パッケージをアクティブ化する必要あり</li>
    	<li> AVChatRoomライブストリーミンググループへの参加時、グループ参加前の20通のメッセージへのリターンをサポート、フラッグシップ版パッケージをアクティブ化する必要あり</li>
    	<li> セッション未読総数を取得し、メッセージ受信オプションが「受信を通知しない」と「メッセージを受信しない」になっているセッションを自動的に削除</li>
    	<li> 長時間接続暗号化チャネルへの国家機密の追加をサポート</li>
    	<li> グループメッセージ履歴をプルする場合の偶発的な終了タグの判断エラー問題を修正</li>
    	<li> ベーシック版から拡張版にアップグレードする場合に、以前に参加したライブストリーミンググループの未読数がある場合の問題を修正</li>
    	<li> 特殊な形式のアカウントに対する既読レポート設定にエラーが発生する問題を修正</li>
    	<li> プライベート環境でネットワークが頻繁に切断および再接続される場合に、偶発的に出現する接続サーバーが正しくない問題を修正</li>
	<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>
    </ul></td>
    <td> 2021-11-19 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>

## 2021年09月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 5.7.1435拡張版をリリース</td>
    <td><ul style="margin:0">
        <li> グループ情報のカスタムフィールドが変更された後、ローカルデータが時間内に更新されない問題を修正しました</li>
    	<li> 最上部に置かれるセッションが多すぎる場合の同期の問題を修正しました</li>
    	<li> Android側のタイムアウトシグナリングに招待がない場合に入力するカスタムデータの問題を修正しました</li>
    	<li> フレンド以外のデータをプルするときに、ネットワークリクエストの失敗により、ローカルデータがブランクのデータで上書きされる問題を修正しました</li>
    	<li> グループから退出した後、グループに再び参加すると、過去のメッセージ履歴がプルされる問題を修正しました</li>
    	<li> フレンドを削除した後、onFriendListDeletedコールバックが2回発生する問題を修正しました</li>
    	<li> セッションの最後のメッセージにあるフレンドノートがブランクになる問題を修正しました</li>
    	<li> IM SDKの初期化後にログインしていないとき、getConversationListを呼び出すとコールバックが発生しない問題を修正しました</li>
    	<li> ネットワークが切断された後にグループセッションが送信に失敗したメッセージ、およびネットワークが復元された後にセッションが受信した最初のメッセージに未読がなくなる問題を修正しました</li>
	<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>
    </ul></td>
    <td> 2021-09-30 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.66ベーシック版をリリース</td>
    <td><ul style="margin:0">
        <li> 削除したWiFi情報の取得</li>
    </ul></td>
    <td> 2021-09-22 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.6.1202拡張版をリリース</td>
    <td><ul style="margin:0">
        <li> グループを退出した後に再び同じグループに参加した場合、退出中に受信されなかったメッセージもセッション未読数としてカウントされる問題を修正しました</li>
    	<li> ミュートされたために送信に失敗したグループメッセージを削除できない問題を修正しました</li>
    	<li> 履歴メッセージをプルするときに、送信者のニックネームとプロフィール画像が古いデータに復元されることがある問題を修正しました</li>
    	<li> ミーティンググループは、未読をサポートするように設定できます</li>
    	<li> シンガポール・韓国・ドイツのグローバルサイトは、アクセスアクセラレーションをサポートしています</li>
    	<li> 受信した画像メッセージに画像形式のエラーが発生することがある問題を修正しました</li>
    	<li> Windowsプラットフォームでビデオメッセージを送信するときに、サムネイルの送信に失敗することがある問題を修正しました</li>
    	<li> 通常グループメッセージの受信成功率のデータレポートを最適化しました</li>
    	<li> ライブストリーミンググループにグループメンバーのミュートを設定した場合、グループメンバーの情報を取得する際に発生するミュート時間が0になる問題を修正しました</li>
    </ul></td>
    <td> 2021-09-10 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>

## 2021年08月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 5.6.1200拡張版をリリース</td>
    <td><ul style="margin:0">
        <li>ログインの所要時間を最適化しました</li>
    	<li> シンガポール・韓国・ドイツのグローバルサイトをサポートしています</li>
    	<li> HTTPDNSの商業化をサポートします</li>
    	<li> グループ属性ロジックを最適化して、複数の端末が同時にグループ属性を変更する場合の同時実行の問題を解決しました</li>
    	<li> メッセージデータベースの照会速度を最適化しました</li>
    	<li> ネットワークポリシーを最適化しました</li>
    	<li> 画像、ビデオ、音声メッセージの検索を最適化しました</li>
    	<li> セッションリストgetConversationListを取得する際に時間がかかる問題を最適化しました</li>
    	<li> ライブストリーミンググループは既読レポートを作成しません</li>
    	<li> 統合ログインエラーコード</li>
    	<li> フレンド検索コールバックパラメータが、V2TIMFriendInfoからV2TIMFriendInfoResultに変更されたため、relationTypeに基づいてフレンドシップを判断しやすくなりました</li>
    	<li> メッセージオブジェクトは、オフラインプッシュ設定を取得するためのインターフェースを追加します</li>
    	<li> 個人情報の更新時に、データベースがクラッシュすることがある問題を修正しました</li>
        <li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください</li>
    </ul></td>
    <td> 2021-08-31 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>

## 2021年07月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 5.5.897拡張版をリリース</td>
    <td><ul style="margin:0">
	<li> データレポートで、クラッシュが偶発的に発生する問題を修正しました</li>
        <li> キャリア名を取得するための呼び出しgetSimOperatorName()を取り除きました </li>
    </ul></td>
    <td> 2021-07-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.65ベーシック版をリリース</td>
    <td><ul style="margin:0">
        <li> キャリア名を取得するための呼び出しgetSimOperatorName()を取り除きました </li>
    </ul></td>
    <td> 2021-07-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.5.892拡張版をリリース</td>
    <td><ul style="margin:0">
        <li>メッセージ検索で、「and」や「or」の関係にある複数のキーワードによる検索をサポートしました</li>
    	<li> メッセージ検索で、メッセージ送信者のアカウントによる検索の設定をサポートしました</li>
    	<li> メッセージ履歴の取得で、時間範囲の設定をサポートしました</li>
    	<li> グループのメッセージ履歴の取得で、sequenceによる取得をサポートしました</li>
    	<li> サードパーティのコールバックによってメッセージが修正された場合の通知を追加しました</li>
    	<li> グループプロファイルに、参加を許可されるグループメンバーの最大人数を取得するインターフェースを追加しました</li>
    	<li> セッションオブジェクトにソートフィールドorderKeyを追加し、最後のメッセージがないセッションをAppレベルでソートできるようにしました</li>
    	<li> ライブストリーミンググループのメッセージ受信のタイムラグを最適化し、バックエンドで事前にアカウント切り替えを完了させるようにしました</li>
    	<li> ネットワーク接続のスケジューリングプロトコルをアップグレードし、海外ネットワーク接続の所要時間を最適化しました</li>
    	<li> セッションリスト取得ロジックを最適化しました</li>
    	<li> グループメンバーリスト取得ロジックを最適化し、ローカルキャッシュを有効化しました</li>
    	<li> 「ログレベルがDebugより低い時にログコールバックがトリガーされない」という問題を修正しました</li>
	<li> 「グループメンバーのプロファイルを取得する時にフレンドノートがない」という問題を修正しました</li>
    	<li> 「参加したグループリストの中にグループマスターの承認待ちのグループを含む」という問題を修正しました</li>
    	<li> オンラインフィードバックの安定性の問題を修正しました</li>
    </ul></td>
    <td> 2021-07-14 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>


## 2021年06月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 5.4.666拡張版をリリース</td>
    <td><ul style="margin:0">
        <li> 従来の簡易版SDKを拡張版SDKに名称変更しました</li>
    	<li> メッセージ検索、グループ検索、フレンド検索（フラッグシップ版のみ対象）をサポートしました</li>
    	<li>メッセージ送信時に、セッションの最後のメッセージを更新するかどうかを設定する新たなパラメータをサポートしました。</li>
    	<li> セッションのローミングメッセージ消去と、セッションの保持をサポートしました</li>
    	<li> 同一プラットフォームにおける複数端末の同時ログインをサポートしました（フラッグシップ版のみ対象）</li>
    	<li> ネットワーク接続ログインの所要時間を最適化しました</li>
    	<li> データ報告を最適化しました</li>
    	<li> オフラインプッシュのロジックを最適化し、グローバルクローズメッセージのオフラインプッシュをサポートしました</li>
    	<li> オフラインプッシュのロジックを最適化し、VIVOスマホのオフラインプッシュによるメッセージ分類フィールドclassificationの設定をサポートしました</li>
    	<li> C2Cセッション未読数が偶発的に不正確になるという問題を修正しました</li>
    	<li> メッセージ履歴の取得速度を最適化しました</li>
    	<li> メッセージの複数Elementで顔絵文字や位置情報の追加をサポートしました</li>
    	<li> オフライン期間にグループのニックネームが変更された場合、再度ログインしても対応するセッションのニックネームの更新が間に合わないという問題を修正しました</li>
    	<li> C2Cセッションが既読の報告を行う時に、20005エラーコードが偶発的に出るという問題を修正しました</li>
    </ul></td>
    <td> 2021-06-03 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>

## 2021年05月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 5.3.435簡易版をリリース</td>
    <td><ul style="margin:0">
        <li> セッションローミングメッセージを削除するためのインターフェースを追加しました。</li>
    	<li> 一部のAndroidスマートフォンが、インターネットに長時間接続すると、ネットワークステータスの変更の通知を受信できない問題を修正しました。</li>
    	<li> フレンド以外の人に対して、バックエンドにフレンド情報を毎回リクエストしないよう、フレンド情報をプルするロジックを最適化しました。</li>
     	<li> グループが解散し、セッションが保持されるシーンで、グループ情報とセッションのメッセージ履歴が取得できない問題を修正しました。</li>
	<li> セッションリストを取得するためのインターフェースで、セッションの順序が乱れる問題を修正しました。</li>
    	<li> 未読セッションの総数を取得するためのインターフェースを追加しました。</li>
    	<li> 未読セッションの総数を取得するときは、応答不可に設定されているグループのセッションをフィルタリングして除外するようにしました。</li>
    	<li> iOSプラットフォームでのHTTPリクエストにCrashが起きる問題を修正しました。</li>
    </ul></td>
    <td> 2021-05-20 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.62標準版をリリース</td>
    <td><ul style="margin:0">
        <li> 既知の問題を修正しました。</li>
    </ul></td>
    <td> 2021-05-20 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>

## 2021年04月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> 
<tr>
    <td> SDK 5.3.425簡易版をリリース</td>
    <td><ul style="margin:0">
        <li> セッションの先頭固定表示の設定をサポートします。</li>
    	<li> シングルチャットの応答不可の設定をサポートします。</li>
    	<li> 未読としてカウントされないメッセージの送信をサポートします。</li>
     	<li> ネットワークログインに失敗していない場合での、ローカルセッションとメッセージデータの取得をサポートします。</li>
	<li> iOSバージョンにxcframeworkを追加しました（Mac Catalystをサポート）。</li>
    	<li> 未読セッションの総数を取得するためのインターフェースを追加しました。</li>
    	<li> birthdayフィールドに個人データを補足します。</li>
    	<li> 他のメンバーがグループ@メッセージを撤回した後も、@メンバーの対応するセッションにグループ@リマインダーが含まれる問題を修正しました。</li>
    	<li> 一部のAndroidスマホの長時間接続、初期のネットワーク接続後に生じる、切断と再接続の問題を修正しました。</li>
    	<li> iOSバージョンの作成グループがカスタムフィールドの設定をサポートしていない問題を修正しました。</li>
    	<li> 特殊なアカウントユーザーのfindMessageがローカルメッセージを照会できない問題を修正しました。</li>
    </ul></td>
    <td> 2021-04-19 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.2.212簡易版をリリース</td>
    <td><ul style="margin:0">
        <li> iOS : IDFA関連のキーワードを使用すると、App Storeへの出品を拒否される可能性があるという問題のため、SDKを最適化しました。</li>
    </ul></td>
    <td> 2021-04-06 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.60標準版をリリース</td>
    <td><ul style="margin:0">
        <li> iOS : IDFA関連のキーワードを使用すると、App Storeへの出品を拒否される可能性があるという問題のため、SDKを最適化しました。</li>
    </ul></td>
    <td> 2021-04-06 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>

## 2021年03月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> 
<tr>
	<td> SDK 5.2.210簡易版をリリース</td>
	<td><ul style="margin:0">
	    <li> メッセージの統合と転送の機能をサポートしました。</li>
	    <li> ネットワークの持続的接続の最適化し、特に海外とのネットワーク接続品質の向上を図りました。</li>
	    <li> ログインエラーコードを細分化し、ログイン時にネットワークが正常かどうか区別するようにしました。</li>
	    <li> COSのアップロードロジックを最適化し、リッチメディアメッセージの送信体験の向上を図りました。</li>
	    <li> メッセージ履歴を取得する高度なインターフェースを追加しました。</li>
	    <li> セッションを一括取得するインターフェースを追加しました。</li>
		<li> フレンドシップを一括チェックするインターフェースを追加しました。</li>
		<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください。</li>
	</ul></td>
	<td> 2021-03-12 </td>
	<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
	<td> SDK 5.1.56標準版をリリース</td>
	<td><ul style="margin:0">
	    <li> Windows SDKが新しいメッセージを破棄してコールバックするとき、顧客スレッドがSDKロジックスレッドを閉鎖する可能性があるという問題を修正しました。</li>
	    <li> Android SDKは新しいログコンポーネントを置き換えて、安定性を向上させます。</li>
	    <li> ネットワークの持続的接続のロジックを最適化し、特に海外とのネットワーク接続品質の向上を図ります。</li>
	    <li> データ報告を最適化し、ネットワークタイムアウト関連のエラーコードを細分化します。</li>
	    <li> iOS SDKがログの抽出時に偶発的にエラーが発生するという問題を修正しました。</li>
	    <li> 安定性に関する若干の問題を修正しました。</li>
	</ul></td>
	<td> 2021-03-03 </td>
	<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>
## 2021年01月
<table>
<tr>
    <th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">リリース日</th><th width="15%">関連ドキュメント</th>
</tr>
<tr>
    <td> SDK 5.1.138簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> ログを最適化しました。</li>
	    <li> ネットワークの持続的接続ポリシーを改善し、海外とのネットワークの接続品質を最適化しました。</li>
	    <li> 同一秒内に複数のC2Cメッセージを送受信すると、
セッションの最後のメッセージが偶発的に不正確になるという問題を修正しました。</ li>
	    <li> セッションリストをクエリーするときにコールバックが発生しないことがあるという問題を修正しました。</li>
	    <li> C2Cメッセージを送信するときにメッセージ番号が偶発的に不正確になるという問題を修正しました。</li>
	    <li> Androidプラットフォームで24MBを超えるビデオを送信すると、アップロードの進行状況が偶発的に負の数になるという問題を修正しました。</li>
	    <li> Androidプラットフォームでメッセージを送信すると偶発的にCrashが発生するという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2021-02-05 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.50標準版をリリース</td>
    <td>
        <ul style="margin:0">
            	<li> V2メッセージオブジェクトにrandomフィールドを補いました。</li>
	    	<li> セッションlastMsgにおいてメッセージの取り消しをサポートしました。</li>
		<li> getMessageで取得する最後のメッセージの状態に偶発的に異常が生じるという問題を修正しました。</li>
		<li> メッセージの受信後にユーザープロファイルを頻繁にプルすることによって引き起こされるメッセージ遅延の問題を修正しました。</li>
		<li> アカウントを削除すると、グループメンバーリストのプルに失敗する可能性があるという問題を修正しました。</li>
		<li> insertLocalMessageの後にfindMessageを呼び出すと、メッセージが見つからない可能性があるという問題を修正しました。</li>
		<li> セッションを削除するとセッションの更新がコールバックされるという問題を修正しました。</li>
		<li> Androidはグループのメッセージ履歴のニックネームが速やかに更新されないという問題を修正しました。</li>
		<li>iOSはデータベースの安定性に関する問題を修正しました。</li>
		<li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください。</li>
        </ul>
    </td>
    <td> 2021-02-05 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.137簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> 複数台のiOSデバイスまたは複数台のAndroidデバイスを使用して、同一のアカウントに繰り返しログインした後に、ログインしたインターフェースにコールバックが偶発的に生じないという問題を修正しました。</li>
	    <li> ロースペックのAndroidモデルによるログパス取得について、偶発的にcrashが発生するという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2021-01-29 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.136簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> V2 APIがログをコールバックするインターフェースを追加しました。</li>
	    <li> グループ@メッセージで、@ユーザーUserIDがブランクになるという問題を修正しました。</li>
	    <li> ライブストリーミンググループメッセージを偶発的に取得しないという問題を修正しました。</li>
	    <li>ネットワークの頻繁な重複接続によって、ログインが偶発的にうまくいかなくなるという問題を修正しました。</li>
	    <li> オフラインにしてキックアウトされてから、再ログインするときに偶発的にエラーになるという問題を修正しました。</li>
	    <li> DNSドメイン名の解析に偶発的にcrashが発生するという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2021-01-27 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.132簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> ネットワークモジュールはオーバーロード保護をサポートしています。</li>
	    <li> 標準版を簡易版にアップグレードすると、偶発的に一部のセッションが失われるという問題を修正しました。</li>
	    <li> ログイン情報が期限切れで、onUserSigExpiredコールバックを受信できないという問題を修正しました。</li>
	    <li> グループメンバーがグループからキックアウトされてから、引き続きグループに再参加する際に、onMemberKickedコールバックを再受信してしまう問題を修正しました。</li>
        </ul>
    </td>
    <td> 2021-01-22 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.131簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li>単一のメッセージ転送インターフェースを追加しました。</li>
	    <li>ライブストリーミンググループのメッセージ受信ロジックを最適化しました。ライブストリーミンググループがメッセージを受信するとき、メッセージ発信者のニックネームとプロフィール画像を再度クエリーすることはありません。</li>
	    <li>セッションの最後のメッセージを削除した時、セッション更新が破棄されないという問題を修正しました。</li>
	    <li>ログイン完了後、C2Cメッセージの同期を行うとき、C2Cセッションの未読数が偶発的にリセットされるという問題を修正しました。</li>
	    <li>オフラインから再度オンラインにして、セッションリストを同期するとき、セッションの最後のメッセージが更新されないという問題を修正しました。</li>
	    <li>Androidプラットフォームに設定したカスタムメッセージのdescriptionフィールドの設定、個人プロファイルのlevelおよびroleフィールドの設定が有効にならないという問題を修正しました。</li>
	    <li>Androidプラットフォームで再初期化するときに偶発的にcrashが発生するという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2021-01-19 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.21標準版をリリース</td>
    <td>
        <ul style="margin:0">
            <li>グローバル化サポートを改善し、英語版の一部の文字列が未だに中国語で表示されるという問題を解消しました。</li>
						<li>Androidプラットフォームでextension拡張フィールドを含むカスタムメッセージの発信がエラーになるという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2021-01-15 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.129簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li>セッションリストの取得時にセッション更新がない場合にも、セッション更新コールバックがトリガーされるという問題を修正しました。</li>
            <li>セッションのすべてのメッセージを消去されたとき、対応するセッションの最後のメッセージがブランクになるという問題を修正しました。</li>
            <li>iOSプラットフォームでgetSignallingInfoメソッドに渡される非シグナリングメッセージがnilではないという問題を修正しました。</li>
            <li>Androidプラットフォームで、JNIの一部の引用リストが制限を超えることによって偶発的にcrashが発生するという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2021-01-13 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.125簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> V2 APIメッセージオブジェクトにrandomフィールドを追加しました。</li>
            <li> V2 APIカスタムメッセージに説明メッセージdescriptionおよび拡張メッセージextensionフィールドを追加しました。</li>
            <li> V2 APIユーザープロファイルオブジェクトにユーザーロールroleとユーザーレベルlevelフィールドを追加しました。</li>
            <li> 4.8.1よりも低いバージョンから簡易版にアップグレードするとき、偶発的に発生するデータベースの互換性の問題を修正しました。</li>
            <li> 自分が自発的にメッセージを発信した際に、このメッセージのコールバックを偶発的に受信するという問題を修正しました。</li>
            <li> 自分がどのグループにも参加していないときに、参加したグループリストの取得がコールバックされないという問題を修正しました。</li>
            <li> グループメッセージの受信の選択項目を設定したときに、セッション更新コールバックがないという問題を修正しました。</li>
            <li> セッションリストをクエリーするときにコールバックが偶発的に発生しないという問題を修正しました。</li>
            <li> セッション同期ロジックに偶発的にcrashが発生するという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2021-01-08 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.20標準版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> V2カスタムメッセージにdescおよびextフィールドを補いました。</li>
            <li> V2ユーザープロファイルインターフェースにroleおよびlevelフィールドを補いました。</li>
            <li> V2インターフェースの最適化によって、ログインの成否に関わらず、ローカルでのセッションリストデータとローカルの履歴情報データを取得できます。</li>
            <li> V2のgetHistoryMessageListインターフェースの追加によって、クラウド端末またはローカルの情報取得および前後へのプルをサポートします。</li>
            <li> C2Cメッセージがプロフィール画像を取得する問題を修正しました。</li>
            <li> リッチメディアメッセージファイルをアップロードする際の安全性や更新に関する問題を修正しました。</li>
            <li> 送信したリッチメディアメッセージのローカルパスがブランクになるという問題を修正しました。</li>
            <li> グループ内に1件のローカルメッセージを挿入し、退出してから再度ログインすると、そのセッションのlastMessageが一つ前のメッセージを表示するという問題を修正しました。</li>
            <li> グループ内に1件のローカルメッセージを挿入し、退出してから再度ログインすると、そのセッションのlastMessageが一つ前のメッセージを表示するという問題を修正しました。</li>
            <li> その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください。</li>
        </ul>
    </td>
    <td> 2021-01-08 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>

## 2020年12月

<table>
<tr>
    <th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">リリース日</th><th width="15%">関連ドキュメント</th>
</tr>
<tr>
    <td> SDK 5.1.123簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> Androidバージョンで、RESTAPIが配信するグループのカスタムされたシステムメッセージを受信できない問題を修正しました。</li>
            <li> メッセージのrandomフィールドの生成方法を最適化しました。</li>
            <li> ログのプリントを最適化して、問題の特定を容易にしました。</li>
            <li> ネットワークモジュールの偶発的にcrashが発生するという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-31 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.122簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> セッションのドラフトを設定すると、コールバックしなくなる可能性があるという問題を修正しました。</li>
            <li> findMessageでメッセージをさがす時、メッセージ送信者の情報が補完されないという問題を修正しました。</li>
            <li> ローカルにメッセージを挿入した後、findMessageを介してメッセージをさがすと失敗する可能性があるという問題を修正しました。</li>
            <li> グループメッセージの受信の選択項目を設定すると、セッションオブジェクトが更新されないという問題を修正しました。</li>
            <li> 個人のニックネーム・プロフィール画像またはグループのニックネーム・プロフィール画像を変更すると、セッション変更通知が破棄されないという問題を修正しました。</li>
            <li> ローカルメッセージを挿入した時に、対応するセッションの最後のメッセージが更新されないという問題を修正しました。</li>
            <li> 個人プロファイル更新サイクルのクラウド制御を開始しました。</li>
            <li> iOSプラットフォームで、DictionaryとArrayの不適切な操作により偶発的にcrashが発生するという問題を修正しました。</li>
            <li> Androidプラットフォームでメッセージを削除すると偶発的にCrashが発生するという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-25 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.121簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> グループプロファイル取得のロジックを最適化し、ライブストリーミンググループが自分のグループメンバーの情報をプルする必要がなくなりました。</li>
            <li> ログプリントを改善し、デバイスのタイプのフィールドを補完しました。</li>
            <li> C2Cセッションの中でメッセージ取り消しの通知を受信した時、対応するセッションの最後のメッセージの状態が更新されないという問題を解決しました。</li>
            <li> ライブストリーミンググループで、ロングポーリングによりメッセージが過度に遅延する問題を修正しました。</li>
            <li> 同じアカウントで繰り返しログインした後に同じライブストリーミンググループに再度参加すると、メッセージのロングポーリングモジュールが、メッセージのプルkeyを更新しないという問題を修正しました。</li>
            <li> iOSプラットフォームで、カスタムフィールドにjson配列をインプットすると、受信側のシグナルモジュールの解析でCrashが発生するという問題を修正しました。</li>
            <li> Androidプラットフォーム設定セッションドラフトで偶発的にCrashが発生するという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-18 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.118簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> メッセージの重複除去のロジックを最適化し、同じメッセージが繰り返しコールバックされるという問題を修正しました。</li>
            <li> ローカルにC2Cメッセージを挿入するインターフェースを追加しました。</li>
            <li> グループの未読メッセージを削除および取り消した時に、グループ未読のカウントが減らないという問題を修正しました。</li>
            <li> 送信に失敗したメッセージを削除できない問題を修正しました。</li>
            <li> グループセッションを削除する時、すでにグループを退出または対応するグループが解散している場合、削除失敗のコールバックが起きるという問題を修正しました。</li>
            <li> グループメッセージの既読の報告を設定する時に、すでにグループを退出または対応するグループが解散している場合、設定失敗のコールバックが起きるという問題を修正しました。</li>
            <li> 個人プロファイルの署名設定に失敗する問題を修正しました。</li>
            <li> フレンドをブラックリストに追加すると偶発的にクラッシュが発生するという問題を修正しました。</li>
            <li> メッセージ送信と同時にメッセージIDがリターンされないという問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-11 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.115簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> シグナリングのタイムアウトの時間とサーバーの時間の同期を最適化しました。</li>
            <li> 脆弱なネットワークでの接続の確立が偶発的に失敗する問題を修正しました。</li>
            <li> iOSのAPIヘッダーファイルを改善しました。</li>
            <li> Androidで、JSONをGsonに置き変えるとクラッシュしてしまう問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-04 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.10標準版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> V2 APIに、グループカスタムフィールドおよびメッセージの複数Elementのサポートを追加しました。</li>
            <li> V2 APIに、ローカル向けにC2Cメッセージを挿入するインターフェースを追加しました。</li>
            <li> 一般のグループとライブストリーミンググループのメッセージロスの問題を修正しました。</li>
            <li> 送信に失敗したメッセージを削除できない問題を修正しました。</li>
            <li> C2Cセッションの中で、送信した最初のメッセージがオンラインメッセージである場合、開封証明を受信できない問題を修正しました。</li>
            <li> 取り消し済みのメッセージが、メッセージ履歴をプルするインターフェースによって返ってきた後、メッセージの状態が不正確になるという問題を修正しました。</li>
            <li> IOSプラットフォームで、フレンドグループ取得のインターフェースにグループ名をブランクのままインプットすると、すべてのグループ情報が戻ってこなくなる問題を修正しました。</li>
            <li> 安定性の問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-04 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.111簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> ログプリントを改善しました。</li>
            <li> 安定性に関する若干の問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-01 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>


## 2020年11月

<table>
<tr>
    <th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">リリース日</th><th width="15%">関連ドキュメント</th>
</tr>
<tr>
    <td> SDK 5.1.110簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> V2 APIのすべてのインターフェースを補完しました。</li>
            <li> セッション機能を補完しました。</li>
            <li> リレーションシップチェーン機能を補完しました。</li>
            <li> グループ@機能を追加しました。</li>
            <li> iOSでiPhoneとiPadの同時オンラインをサポートしました。</li>
            <li> 送信メッセージで複数Elementをサポートしました。</li>
            <li> グループプロファイルのカスタムフィールドを補完しました。</li>
            <li> 安定性に関する若干の問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-11-26 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.2標準版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> iOSでiPhoneとiPadの同時オンラインをサポートしました。</li>
            <li> Macでarm64アーキテクチャをサポートしました。</li>
            <li> Androidバージョンの安定性の問題を修正しました。</li>
            <li> 標準TRTC依存パッケージに置き換えました。</li>
        </ul>
    </td>
    <td> 2020-11-12 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.1標準版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> AVChatRoom（ライブストリーミンググループ）のオンライン人数を取得するインターフェースを追加しました。</li>
            <li> メッセージをその一意性IDに基づきクエリーするインターフェースを追加しました。</li>
            <li> サーバーのキャリブレーションのタイムスタンプを取得するインターフェースを追加しました。</li>
            <li> ログインスピードを最適化しました。</li>
            <li> グループメンバー@で、<code>@All</code>をサポートしました。</li>
            <li> TUIKitコンポーネントのインターナショナルサポートを追加しました。</li>
            <li> グループライブストリーミングに小型ライブストリーミングウィンドウのサポートを追加しました。</li>
        </ul>
        その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください。
    </td>
    <td> 2020-11-05 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>


## 2020年10月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td> SDK 5.0.108簡易版をリリース</td>
<td>
    <li>iOSバージョンで、安定性の問題を修正しました。</li>
    <li>Androidバージョンで偶発的に発生するメッセージがコールバックされないという問題を修正しました。</li>
</td>
<td> 2020-10-23 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a> </td>
</tr><tr>
<td> SDK 5.0.10標準版をリリース</td>
<td><ul style="margin:0">
    <li> シグナルインターフェースを最適化し、オンラインメッセージonlineUserOnlyとオフラインプッシュ情報offlinePushInfoのパラメータの設定をサポートしました。</li>
    <li> 単一セッションを取得するインターフェースの非同期コールバックを最適化しました。</li>
    <li> セッションに取得したグループタイプのインターフェースを追加し、セッションリストのフィルタリング表示ができるようにしました。</li>
    <li> グループライブストリーミング機能を新たに追加し、マイク接続、ギフト、美顔、ボイスチェンジャーなどの機能を取り揃えました。</li>
    <li> 大型ライブストリーミングルームを新たに追加し、マイク接続、PK、「いいね」、ギフト、美顔、弾幕、フレンド・フォローなどをサポートしました。</li>
    <li> 音声/ビデオシグナルの識別の問題を修正しました。</li>
</ul></td>
<td> 2020-10-15 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
</table>


## 2020年09月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td> SDK 5.0.106バージョンをリリース（Android & iOS簡易版）</td>
<td>既知の安定性の問題を修正しました。</td>
<td> 2020-09-21 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a> </td>
</tr><tr>
<td> SDK 5.0.6標準版をリリース</td>
<td><ul style="margin:0">
    <li>グループ@機能を追加しました。</li>
    <li>iOSとAndroidにdeleteMessagesインターフェースを新たに追加しました。ローカルおよびローミングメッセージを同時に削除します。</li>
    <li>deleteConversationインターフェースは、セッションを削除すると同時に、ローカルおよびローミングメッセージも削除します。</li>
    <li>API2.0インターフェースに、ユーザープロファイル、フレンドプロファイル、グループメンバープロファイルのカスタムフィールドの設定と取得のためのインターフェースを補充しました。</li></ul>
その他の更新内容については、<a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください。</td>
<td> 2020-09-18 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr><tr>
<td> SDK 5.0.102バージョンをリリース（Android & iOS簡易版）</td>
<td><ul style="margin:0">
    <li>Android & iOS簡易版SDKをリリース。</li>
    <li>簡易版SDKは、既存の標準版をベースに、フレンドとセッションの2つの機能をカットして、一部の業務ロジックに対しては最適化を行うことにより、さらに高い実行効率と、インストールパッケージ容量増加のさらなる縮小を実現しています。</li>
</ul></td>
<td> 2020-09-04 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード </td>
</tr>
</table>

## 2020年07月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.9.1バージョンをリリース（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>海外でのログインの問題を最適化しました。</li>
    <li>海外の一部エリアにおけるファイルアップロード失敗の問題を修正しました。</li>
    <li>@記号を含むアカウントのファイルアップロード失敗の問題を修正しました。</li>
    <li>C2C未読数の偶発的なエラーの問題を修正しました。</li>
    <li>セッションのshowNameの表示における偶発的な異常の問題を修正しました。</li>
    <li>ファイルタイプメッセージのダウンロードurlを取得するインターフェースを追加しました。</li>
    <li>iOSにおいて、ネットワーク切断時のC2Cメッセージ取得にコールバックがない問題を修正しました。</li>
    <li>Androidにおいて、シグナル解析インターフェースに偶発的にクラッシュが発生するという問題を修正しました。</li>
    <li>Androidにおいて、メッセージの中のオフラインプッシュ情報の取得時に偶発的にクラッシュが発生するという問題を修正しました。</li>
    <li>Androidにおいて、API2.0 getFriendApplicationListインターフェースにおいて、データがないとコールバックされない問題、およびgetGroupMembersInfoインターフェースでグループメンバー以外をインプットするとコールバックされない問題を修正しました。</li>
    <li>Windowsにおいて、グループ参加時にグループ追加の詳細情報を取得できるようになりました。</li>
    <li>Windowsにおいて、small fileを送信できない問題を修正しました。</li>
    <li>Windowsにおいて、ログ報告による6002エラーを修正しました。</li>
    <li>iOS Demo & Android Demoにおいて、音声/ビデオオフライン通話のプッシュを追加し、応答画面にリダイレクトできるようになりました。</li>
    <li>iOSにおいて、カスタムメッセージの削除、取り消しが無効になる問題を修正しました。</li>
    <li>iOSにおいて、音声/ビデオコードを swift -> ocにし、サードパーティライブラリの依存を大幅に減らしました。</li>
    <li>iOSにおいて、LiteAV_TRTC、LiteAV_Professionalの2種類の音声/ビデオ依存ライブラリのTUIKit pod統合をサポートしました。</li>
    <li>Androidにおいて、Demoのオフラインプッシュを最適化し、各メーカーのプッシュSDKバージョンをアップグレードしました。</li>
</ul></td>
<td>2020-07-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr> </table>


## 2020年06月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.8.50バージョンをリリース（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>API 2.0インターフェースにおいて、ライブストリーミンググループ(AVChatRoom)に参加者があった後、 onMemberEnterのコールバックがないという問題を修正しました。</li>
    <li>API 2.0インターフェースのonGroupInfoChangedとonMemberInfoChangedのコールバックにgroupIDのパラメータを追加しました。</li>
    <li>C2Cメッセージ送信が成功した後にセッション更新のコールバックがないという問題を修正しました。</li>
    <li>アカウントを切り替えて同じライブストリーミンググループ（AVChatRoom）に参加するとメッセージを受信できない問題を修正しました。</li>
    <li>偶発的に起きる、ログイン後の未読メッセージの同期において、コールバックの順序が不正確になる問題を修正しました。</li>
    <li>シグナルインターフェースを追加しました。</li>
    <li>ライブストリーミンググループ（AVChatRoom）にカスタマイズのグループ属性インターフェースを追加しました。</li>
    <li>既知のクラッシュの問題を修正しました。</li>
    <li>Android Qバージョンとの互換性をはかるため、ログのデフォルトの保存先を、/sdcard/Android/data/パッケージ名/files/log/tencent/imsdkに修正しました。</li>
    <li>Windowsプラットフォームにおいて、グループ作成時のグループメンバーのロールの問題を修正しました。</li>
    <li>TUIKitでAPI 2.0インターフェースを置き換えました。</li>
    <li>TRTCを結合させ、オーディオビデオ通話機能を実現しました。</li>
    <li>iOSのTUIKitに、ダークカラーモードを追加しました。</li>
    <li>AndroidXをサポートしました。</li>
</ul></td>
<td>2020-06-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr> </table>

## 2020年05月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.8バージョンをリリース（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>iOS & Androidにおいて、最新のAPI 2.0インターフェースをリリースしました。</li>
    <li>iOSとAndroidでIPv6をサポートしました。</li>
    <li>ライブストリーミンググループ（AVChatRoom）でグループメンバーリストの動的更新をサポートしました。</li>
    <li>xlogクラッシュの問題を修正しました。</li>
    <li>iOSで大容量ファイルを送信すると必ず失敗する問題を修正しました。</li>
    <li>iOSにおいて、メッセージ送信者のフレンドノートをプルすると異常が起きる問題を修正しました。</li>
    <li>IM SDKがAndroidXをサポートしました。</li>
    <li>Androidデバイスのネットワーク権限の問題によるクラッシュを修正しました。</li>
</ul></td>
<td>2020-05-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr> </table>


## 2020年03月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 2.6バージョンをリリース（ミニプログラムおよびWeb端末）</td>
<td><ul style="margin:0">
    <li>Web端末でビデオメッセージの作成・送信をサポートし、最大100MBのビデオファイルの送信が可能になりました。</li>
    <li>Messageに<code>nick</code>と<code>avatar</code>の属性を追加しました。これを音声/ビデオチャットルーム（AVChatRoom）内のメッセージ送信者のニックネームとプロフィール画像URLの表示に使用します（事前にupdateMyProfile の呼び出しによる設定が必要です）。</li>
    <li>Web端末で、マルチインスタンスでログインした時、C2Cメッセージの取り消し通知が各インスタンスにおいて同期できるようになりました。</li>
    <li>updateGroupProfileを呼び出してグループカスタムフィールドの修正に成功した場合、グループメンバーがグループプロンプトメッセージを受信でき、関連する内容 Message.payload.newGroupProfile.groupCustomFieldを取得できるようになります。</li>
    <li>TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVEDインターフェースを破棄し、MESSAGE_RECEIVEDで代替します。</li>
    <li>getGroupListインターフェースを呼び出した時の偶発的なエラーの問題を修正しました。</li></ul></td>
<td>2020-03-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr><tr>
<td>SDK 4.7バージョンをリリース（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>ローカルログのサイズを最適化しました。</li>
    <li>ログインの所要時間を最適化しました。</li>
    <li>未読数カウントのマルチデバイス同期の問題を修正しました。</li>
    <li>1人のフレンドを取得するインターフェースgetFriendListを追加しました。</li>
    <li>iOS & Android端末において、各々2つのプラットフォームのオフラインプッシュ通知バーのメッセージに表示する必要があるタイトルとコンテンツを設定できるようになります。</li>
</ul></td>
<td>2020-03-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr> </table>

## 2020年02月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.6バージョンの継続的な最適化（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>ファイルのアップロード上限を100MBに引き上げました。</li>
    <li>COSのアップロードを最適化しました。</li>
    <li>グループの未決処理のロジックを最適化しました。</li></ul></td>
<td>2020-02-28</td>
<td>-</td>
</tr><tr>
<td>SDK 2.5バージョンをリリース（ミニプログラムおよびWeb端末）</td>
<td><ul style="margin:0;">
    <li>ネットワーク状態変更のイベントTIM.EVENT.NET_STATE_CHANGEを新たに追加しました。アクセス側はこのイベントに基づき関連するプロンプトとガイダンスを行えるようになります。</li>
    <li>WeChat Mini Programのプラグイン環境での動作を新たにサポートしました。</li>
    <li>エラーコードを減らし、最適化しました。</li>
    <li>コンソールで音声/ビデオチャットルーム（AVChatRoom）を作成して、グループマスターを指定し、グループマスターがこのグループに入ると、グループ内の他の人が発信した情報がグループマスター側で重複する問題を修正しました。</li>
    <li>コンソールまたはREST APIを利用して頻繫にグループの作成・破棄を行うと、SDKが TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVEDのイベントを配信しなくなる問題を修正しました。</li>
    <li>getMessageListで偶発的に起きる、グループメッセージリストをプルできなくなる問題を修正しました。</li></ul></td>
<td>2020-02-28</td>
<td>-</td>
</tr> </table>

## 2020年01月

<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 2.4バージョンをリリース（ミニプログラムおよびWeb端末）</td>
<td><ul style="margin:0;">
    <li>メッセージ取り消しのインターフェースrevokeMessageを新たに追加しました。</li>
    <li>MessageにisRevokedの属性を追加し、値がtrueの時は取り消されたメッセージを表示します。</li>
    <li>メッセージが取り消されたイベント通知 TIM.EVENT.MESSAGE_REVOKEDを新たに追加しました。</li>
    <li>キックアウトによるオフラインのイベント通知TIM.EVENT.KICKED_OUTに、キックアウトによるオフラインのタイプとして、複数端末ログインによるキックアウトとUserSig失効によるキックアウトを追加しました。</li>
    <li>createFileMessageのアップロードファイルサイズを20Mから100MBに調整しました。</li>
    <li>グループプロンプトメッセージのmsgMemberInfoとshutupTimeはまもなく破棄されます。memberListとmuteTimeを使用して置き換えてください。</li>
    <li>コンソールに、IMのAIカスタマーサービスエントリーを新たに追加しました。</li>
    <li>offインターフェースを呼び出して、モニタリングイベントをキャンセルできない問題を修正しました。</li>
    <li>MessageのisReadの属性値とタイプが不正確であるという問題を修正しました。</li>
    <li>ビデオメッセージの送信時に、ビデオファイルが最大制限値を超えた後のエラーコードとエラー情報に誤りがあるという問題を修正しました。</li>
    <li>偶発的に起きる、カスタムフィールド更新後のフィールドの内容が不正確になるという問題を修正しました。</li>
    <li>ログイン後に音声/ビデオチャットルームタイプのグループに参加すると、JOIN_STATUS_ALREADY_IN_GROUPが偶発的に起きる問題を修正しました。</li>
    <li>core-jsによる潜在的なパフォーマンスの問題を修正しました。</li></ul></td>
<td>2020-01-03</td>
<td>-</td>
</tr> </table>

## 2019年12月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.6バージョンの継続的な最適化（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>ネットワークの接続品質を最適化し、ネットワーク品質の変化をより迅速に感知できるようになりました。</li>
    <li>AVChatRoomのメッセージの処理を最適化しました。</li>
    <li>メッセージに同時にニックネームをリターンするインターフェースgetSenderNicknameを新たに追加しました。</li>
    <li>TUIKit/Demoで、セッションリストのプロフィール画像にフィレット設定をサポートしました。</li></ul></td>
<td>2019-12-23</td>
<td>-</td>
</tr><tr>
<td>SDK 2.3バージョンをリリース（ミニプログラムおよびWeb端末）</td>
<td><ul style="margin:0;">
    <li>createImageMessageとcreateFileMessageインターフェースでFileオブジェクトのインプットを新たにサポートしました。</li>
    <li>顔絵文字メッセージ作成インターフェースcreateFaceMessageを新たに追加しました。</li>
    <li>TIM.TYPES.GRP_AVCHATROOMタイプのグループのメッセージ通知効率を最適化し、ユーザーエクスペリエンスを大幅に向上させました。</li>
    <li>メッセージ送信失敗時にSDKが返す実際のエラーコードとエラー情報を調整しました。</li>
    <li>logout呼び出し時に現在のインスタンスのメッセージチャネルのみログアウトするように調整しました。</li>
    <li>アクセス側がインプットするコールバック関数に対して安全にカプセル化し、コールバック関数のロジックにエラーがあったときに、異常をキャッチし迅速に問題を特定できるようにしました。</li>
    <li>IMサーバーのエラーコードが発生すると、SDKが中国語のエラー情報を出力します。</li>
    <li>WeChat Mini Program環境で長時間バックエンドに切り替え、再度フロントエンドに切り替えると、偶発的にメッセージロスが起きる問題を修正しました。</li>
    <li>1回のメッセージ送信で複数回のTIM.EVENT.CONVERSATION_LIST_UPDATEDがトリガーされる問題を修正しました。</li>
    <li>registerPluginを呼び出さない、またはインターフェースの入力パラメータに誤りがあり、画像などのファイルをアップロードする時にSDKがエラーを報告する問題を修正しました。</li>
    <li>TIM.TYPES.GRP_AVCHATROOMタイプのグループを解散した後、ロングポーリングが停止されない問題を修正しました。</li>
    <li>「マルチインスタンス」または「マルチ端末」のログインを有効にした場合、1つのWebインスタンスからログアウトすると、他のインスタンスや端末もメッセージを受信できなくなる問題を修正しました。</li>
    <li>偶発的に起きる、プルしたセッションリストの構造上の問題によりSDKがエラーを報告する問題を修正しました。</li></ul></td>
<td>2019-12-13</td>
<td>-</td>
</tr> </table>

## 2019年11月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 2.2バージョンをリリース（ミニプログラムおよびWeb端末）</td>
<td><ul style="margin:0;">
    <li>ミニプログラムにおいて、ビデオメッセージを作成・送信するcreateVideoMessageを新たにサポートし、ビデオメッセージのマルチプラットフォーム相互通信ができるようになりました（TUIKitおよびSDKを最新バージョンにアップデートする必要があります）。</li>
    <li>グループメンバーのプロファイルをクエリーするインターフェースgetGroupMemberProfileを新たに追加しました。</li>
    <li>Native IM v3.xから送信された音声、ファイルメッセージとの互換性をサポートしました。</li>
    <li>位置情報メッセージGeoPayloadの受信を新たにサポートしました。</li>
    <li>ログアウトした後、TIM.TYPES.GRP_AVCHATROOMタイプのグループのロングポーリングが依然として動作している問題を修正しました。</li>
    <li>TIM.TYPES.GRP_AVCHATROOMタイプのグループのメッセージインスタンスの中のグループネームカードに値がない問題を修正しました。</li>
    <li>IE 10ブラウザにおけるエラー報告の問題を修正しました。</li>
    <li>匿名でグループに参加できない問題を修正しました。</li></ul></td>
<td>2019-11-21</td>
<td>-</td>
</tr><tr>
<td>SDK 4.6バージョンをリリース（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>メッセージ取り消しのローミングをサポートしました。</li>
    <li>iOS/Mac端末において、OPPOChannelIDの設定を追加し、Android 8.0以上のOPPOスマホがiOSメッセージプッシュの受信に失敗するという問題を修正しました。</li>
    <li>iOS/Mac端末において、getGrouplistのリターンのオブジェクトのコメントを最適化しました。</li>
    <li>OPPOスマホ（システム要件：8.0以上）のオフラインプッシュのchannleIDについて、コンソールでの設定をサポートしました。</li>
    <li>TUIKit/Demoにビデオ通話機能を追加しました。</li>
    <li>TUIKit/Demoにグループのプロフィール画像の9グリッド合成表示を追加し、セッションリスト、連絡先、チャット画面UIを最適化しました。</li></ul></td>
<td>2019-11-13</td>
<td>-</td>
</tr><tr>
<td>メッセージ履歴の保存を「固定料金」に変更しました</td>
<td>メッセージ履歴の保存を「固定料金」に変更し、ルールをより簡単に、よりお得にご利用いただけるようになりました。</td>
<td>2019-11-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34350">料金説明</a></td>
</tr> </table>

## 2019年10月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>刷新したコンソールのサービスを開始しました</td>
<td>新版IMコンソールの正式なサービスを開始しました。</td>
<td>2019-10-22</td>
<td><ul style="margin:0;">
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34577">アプリケーションの作成とアップグレード</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34540">基本設定</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34419">機能設定</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34578">グループ管理</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34520">コールバック設定</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34579">統計分析</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34580">開発支援ツール</a></li></ul></td>
</tr><tr>
<td>SDK 4.5バージョンの継続的な最適化（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>ファイルタイプメッセージ送信時に生成されるURLに、ファイル形式の拡張子を追加しました。</li>
    <li>グループカスタムフィールドの修正後に通知のコールバックを追加しました。</li>
    <li>ログインせずにinitStorageのメソッドを呼び出して、ローカルユーザーとグループの情報を取得できるようになります。</li>
    <li>Android端末において、getElementCountインターフェースのリターンのタイプを最適化しました。</li>
    <li>Windowsのクロスプラットフォームライブラリにおいて、各プラットフォームのネットワーク再接続の速度を最適化しました。</li>
    <li>Windowsのクロスプラットフォームライブラリに、JVM設定を新たに追加し、Android環境からJVMをインプットしやすくしました。</li></ul></td>
<td>2019-10-16</td>
<td>-</td>
</tr><tr>
<td>SDK 2.1バージョンをリリース（ミニプログラムおよびWeb端末）</td>
<td><ul style="margin:0;">
    <li>音声メッセージとビデオメッセージの受信を新たにサポートしました。</li>
    <li>getMessageListインターフェースの1回の呼び出しで15本までメッセージをプルできるようになります。</li>
    <li>TIM.TYPES.MSG_SOUNDを破棄し、TIM.TYPES.MSG_AUDIOで置き換えます。</li>
    <li>getMessageListインターフェースが削除済みのグループチャットセッションのメッセージをプルできない問題を修正しました。</li>
    <li>グループシステムの通知にグループ名がないという問題を修正しました。</li>
    <li>メッセージを受信して新規作成したセッションにプロファイルがないという問題を修正しました。</li></ul></td>
<td>2019-10-16</td>
<td>-</td>
</tr> </table>

## 2019年09月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 2.0バージョンをリリース（ミニプログラムおよびWeb端末）</td>
<td>IMミニプログラムおよびウェブページ版SDKを刷新し、各モジュールの安定性を最適化して、アクセス体験を全面的に向上させました。さらにお客様がダイレクトに体験できるように、ビジュアル化したDemoを提供しています。</td>
<td>2019-09-19</td>
<td>-</td>
</tr><tr>
<td>SDK 4.5バージョンの継続的な最適化（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>Androidに開封証明を追加しました。</li>
    <li>ネットワーク接続の品質を最適化しました。</li>
    <li>グループ/グループメンバーのカスタムフィールドをプルするロジックを最適化しました。</li></ul></td>
<td>2019-09-18</td>
<td>-</td>
</tr> </table>

## 2019年08月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.5バージョンをリリース（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>チャットの音声メッセージ、MotionEvent.ACTION_CANCELイベントの処理を新たに追加しました。</li>
    <li>セッションリスト、チャット画面、詳細プロファイル、連絡先を新たに追加し、プロフィール画像表示機能を追加しました。</li>
    <li>個人プロファイルのプロフィール画像を修正する機能を新たに追加しました。</li>
    <li>オフラインプッシュ機能へのIntentリダイレクトを新たに追加しました。</li>
    <li>シングルチャット、グループチャットのセッションで、ランダムプロフィール画像を新たに追加しました。</li>
    <li>グループメンバーの管理者設定および管理者設定取り消しのプロンプトを新たに追加しました。</li>
    <li>グループメンバーのミュートおよびミュート取り消しのプロンプトを新たに追加しました。</li>
    <li>未読メッセージ数のカウントを最適化しました。</li>
    <li>ログイン後の最新セッションリストのロード速度を最適化しました。</li>
    <li>ログ消去の機能を追加しました。</li>
    <li>Android端末でcom.tencent.imsdk.TIMGroupReceiveMessageOptクラスを一元的に使用します。</li>
    <li>TUIKit/Demoの中に触覚フィードバックを追加しました。ユーザーはTUIKitの使用時、フィードバックを自主的に設定し、カスタマイズすることが可能です。</li>
    <li>TUIKit/Demoにカスタムメッセージ送信を新たに追加しました。</li>
    <li>TUIKit/DemoにC2Cの開封証明を新たに追加しました。</li>
    <li>TUIKit/Demoに未再生音声の赤点灯表示を新たに追加しました。</li>
    <li>TUIKit/Demoにプロフィール画像をクリックして大きな画像で見る機能を追加しました。</li>
    <li>TUIKit/Demoのグループチャットで、灰色の小型バーのスタイルを調整すると、ユーザーニックネームが青色に変わり、ニックネームをクリックするとユーザー情報画面に移動できます。</li>
    <li>チャットのスティッキーロジックを最適化し、最も近い時間から順番に表示します。</li>
    <li>Demoの中のグループ内ニックネームの表示ロジックを最適化しました。</li>
    <li>チャット画面の中のプロフィール画像を表示するロジックを最適化しました。</li>
    <li>未読メッセージ数のカウントを最適化しました。</li>
    <li>ログイン後の最新セッションリストのロード速度を最適化しました。</li>
    <li>海外ユーザーがファイルメッセージを送信する速度を最適化しました。</li></ul></td>
<td>2019-08-30</td>
<td>-</td>
</tr><tr>
<td>Instant Messaging（IM）の中国語名称を「即時通信」に変更</td>
<td>「Instant Messaging(IM)」の中国語名称を「雲通信」から「即時通信」に変更しました。</td>
<td>2019-08-06</td>
<td>-</td>
</tr> </table>

## 2019年07月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.4バージョンの継続的な最適化（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>一部のAPIインターフェースを整理、統合しました。</li>
    <li>フレンド追加に、単一方向と双方向の選択項目を追加しました。</li>
    <li>disableStorageインターフェースを新たに追加しました。これによりすべてのローカルストレージの使用が無効になります。</li>
    <li>ファイル、ビデオ、音声メッセージにダウンロードURL取得のインターフェースを追加しました。</li>
    <li>ログインモジュールを最適化しました（繰り返しログイン/頻繫なログイン/頻繫なアカウント切り替え/自動オンライン接続/キックアウトによるオフライン）。</li>
    <li>長時間バックエンドに切り替えた後、再度フロントエンドに切り替えると、メッセージ送信に時間がかかる問題を修正しました。</li>
    <li>シングルチャットの未読数カウントの問題を修正しました。</li></ul></td>
<td>2019-07-16</td>
<td>-</td>
</tr> </table>

## 2019年06月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.4バージョンおよび刷新したDemoをリリース（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>刷新したモバイルクライアントUI設計のTUIKitおよび製品Demoのサービスを開始しました。</li>
    <li>Demoの連絡先、グループ管理、リレーションシップチェーンなどの機能を改善しました。</li>
    <li>キャッシュ最適化により、UIのラグを減少させました。</li>
    <li>メッセージ送信の効率を最適化しました。</li>
    <li>クロスプラットフォームライブラリのメッセージに、メッセージの一意性IDを取得するためのJSON keyを追加しました。</li></ul></td>
<td>2019-06-27</td>
<td>-</td>
</tr> </table>

## 2019年05月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
            <td>SDK 4.3バージョンの継続的な最適化（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>TIMFriendshipManagerクラスの中にquerySelfProfileおよびqueryUserProfileインターフェース（ローカルデータ読み取り）を追加しました。</li>
    <li>フレンド情報の取得の中にaddTimeのフィールドを追加しました。</li>
    <li>x86およびx86_64アーキテクチャを新たにサポートしました。</li>
    <li>カスタムフィールドのデータの報告を新たに追加しました。</li>
    <li>メッセージを閲読後即破棄する機能を追加しました。</li>
    <li>メッセージ取り消しの使用例を新たに追加しました。</li>
    <li>フレンド検証インターフェースcheckFriendsを追加しました。</li>
    <li>queryGroupInfoインターフェースによるローカルデータ取得を追加しました。</li>
    <li>getGroupDetailInfoとgetGroupPublicInfoインターフェースを破棄し、getGroupInfoインターフェースに統合しました。</li>
    <li>サーバー接続ポリシーを最適化しました。</li>
    <li>ネットワーク切断・再接続のポリシーを最適化しました。</li>
    <li>サーバーのオーバーロードポリシーを最適化しました。</li>
    <li>ハートビートを最適化し、不要なパケット送信を減らしました。</li>
    <li>再接続時の接続リクエストを最適化しました。</li>
    <li>様々なネットワークにおける初回接続と海外アクセスポイントの品質を最適化しました。</li>
    <li>iOSにおいて、Wi-Fi切り替え時のネットワーク再接続が遅いという問題を修正しました。</li>
    <li>グループメッセージの同期の問題を最適化しました。</li></ul></td>
<td>2019-05-24</td>
<td>-</td>
</tr> </table>

## 2019年04月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.3バージョンをリリース（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>フレンドのブラックリスト機能、フレンドグループ分け機能、フレンド追加リクエスト処理などのリレーションシップチェーン機能を追加しました。</li>
    <li>未読数カウントに関する問題を最適化しました。</li>
    <li>メッセージ既読状態についての問題を修正しました。</li>
    <li>REST APIが送信するC2Cメッセージのソート異常の問題を修正しました。</li>
    <li>ローミングメッセージの取得に偶発的に繰り返しが生じる問題を修正しました。</li>
    <li>uniqueIdの空実装の問題を修正しました。</li>
    <li>TIMMessageのsenderProfileによってユーザープロファイル情報が取得できないという問題を修正しました。</li>
    <li>開封証明のコールバックおよび状態の問題を修正しました。</li>
    <li>未読メッセージの同期をとる時、最も新しいメッセージがコールバックされない問題を修正しました。</li>
    <li>グループメッセージが偶発的に受信できなくなる問題を修正しました。</li>
    <li>IP接続とlogin情報の統計報告を追加しました。</li></ul></td>
<td>2019-04-24</td>
<td>-</td>
</tr> </table>

## 2019年03月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.2バージョンをリリース（Android、iOSおよびWindows端末）</td>
<td><ul style="margin:0;">
    <li>iOS端末において、TUIKit.frameworkのbitcode 2のサポートを新たに追加しました。</li>
    <li>iOS端末において、podによる直接的なTUIKit.frameworkの統合を新たにサポートしました。</li>
    <li>Windows端末において、duilibライブラリをUIコンポーネントとするIM Demoを新たに追加しました。</li>
    <li>Windows端末において、/source-charset:.65001のコンパイルの選択項目を新たに追加しました。</li>
    <li>Web端末において、WEBIMを新たに追加し、現在すでに 「.amr」録音形式の再生をサポートしています。</li>
    <li>フレンドの追加/削除/クエリーのロジックを新たに追加しました。</li>
    <li>新旧バージョンの音声、ファイル、ビデオメッセージの相互通信の問題を修正しました。</li>
    <li>TUIkitの音声再生ロジックを最適化しました。</li>
    <li>AVChatRoomの入室が100人を超えた後のメッセージ受信異常の問題を修正しました。</li>
    <li>グループのミュートが無効になる問題を修正しました。</li>
    <li>ユーザーのグループ内身分変更機能を修正しました。</li>
    <li>グループメッセージ受信の選択項目の変更を修正しました。</li>
    <li>オフラインプッシュのスイッチング無効の問題を修正しました。</li>
    <li>ユーザーのグループ内身分変更機能を修正しました。</li>
    <li>グループの保留中および解決済みの情報を取得し、誤って返されるという問題を修正しました。</li>
    <li>クライアントがバックグランドに入るとCrashする問題を修正しました。</li>
    <li>ネットワークを再接続した後にメッセージが受信できない問題を修正・最適化しました。</li>
    <li>偶発的なメッセージソートエラーの問題を修正しました。</li>
    <li>偶発的なメッセージ送信失敗の問題を修正しました。</li>
    <li>バックエンドがグループを解散したとき、クライアントが対応するコマンドを受信できない問題を最適化しました。</li></ul></td>
<td>2019-03</td>
<td>-</td>
</tr> </table>

## 2019年01月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 4.0バージョンをリリース（Android、iOSおよびWindows端末）</td>
<td>刷新したIMクライアントSDKをリリースし、大規模なネットワーク接続、メッセージ送受信および未読数などの問題を修正し、ネットワーク、メッセージなどの重要な基盤モジュールの安定性を大幅に最適化しました。さらにオープンソースのTUIKitを提供し、お客様のアクセス手順を簡素化しています。</td>
<td>2019-01-21</td>
<td>-</td>
</tr> </table>

## 2017年07月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>UGC（ショート動画）をサポートしました</td>
<td>UGC（ショート動画）のメッセージ機能をサポートしました。ビデオ編集によってコンテンツがより良質になり、ユーザーエクスペリエンスがさらに向上します。</td>
<td>2017-07</td>
<td>-</td>
</tr> </table>

## 2017年05月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>SDK 3.0バージョンをリリース</td>
<td>機能をさらに取り揃え、容積をより小さくし、コード構造を最適化し、お客様の統合効率とダウンロード体験を効果的に向上させています。</td>
<td>2017-05</td>
<td>-</td>
</tr> </table>

## 2016年12月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>マルチインスタンスによる相互排他機能をサポートしました</td>
<td>Web端末において、マルチインスタンスによる相互排他のニーズを満たし、Web端末によるカスタマーサービスなどのシナリオのニーズに応えます。</td>
<td>2016-12</td>
<td>-</td>
</tr> </table>

## 2016年08月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>ブロードキャストメッセージ機能をサポートしました</td>
<td>全員に対するブロードキャストメッセージプッシュをサポートし、メッセージの配信効率を引き上げ、クライアントのプッシュのニーズに応えます。</td>
<td>2016-08</td>
<td>-</td>
</tr><tr>
<td>マルチ端末の同時ログインをサポートしました</td>
<td>マルチ端末の同時ログインをサポートし、スマホとPCを同時に使用するシナリオに対応して、ユーザーエクスペリエンスを効果的に向上させ、最適化しています。</td>
<td>2016-08</td>
<td>-</td>
</tr> </table>

## 2016年05月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>ライブストリーミングチャットルームのサービスを開始</td>
<td>ライブストリーミングシナリオを対象に、人数無制限のライブストリーミングチャットルームをサポートします。またメッセージ頻度の制限、メッセージのカスタマイズなどのシナリオ化のニーズにも対応しています。</td>
<td>2016-05</td>
<td>-</td>
</tr> </table>

## 2016年03月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>メッセージプッシュ機能をサポートしました</td>
<td>AndroidおよびiOSのオフラインプッシュ機能をサポートしました。メッセージの到達がより保証され、ユーザーエクスペリエンスを効果的に向上させ、最適化します。</td>
<td>2016-03</td>
<td>-</td>
</tr> </table>

## 2015年12月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>ミニビデオのメッセージタイプをサポートしました</td>
<td>ミニビデオのメッセージタイプをサポートし、メッセージコンテンツをより豊富にしました。</td>
<td>2015-12</td>
<td>-</td>
</tr> </table>

## 2015年08月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>Webプラットフォームをサポートしました</td>   
<td> WebプラットフォームのIMクラウドサービスをサポートし、顔絵文字のカスタマイズなど、メッセージのタイプを追加しました。</td>
<td>2015-08</td>
<td>-</td>
</tr> </table>

## 2015年07月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>Windowsプラットフォームをサポートしました</td>
<td>WindowsプラットフォームのIMクラウドサービスをサポートし、地理位置、音声などのメッセージのタイプを追加しました。</td>
<td>2015-07</td>
<td>-</td>
</tr> </table>

## 2015年05月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
</tr> <tr>
<td>Instant Messaging（IM）（中国語名称「即時通信」：旧名称「雲通信」）のサービスを開始</td>
<td>AndroidおよびiOSのIMクラウドサービスをサポートし、グラフィック、顔絵文字など多様なメッセージタイプをサポートしています。</td>
<td>2015-05</td>
<td>-</td>
</tr> </table>




