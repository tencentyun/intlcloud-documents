## 2020年12月

<table>
<tr>
    <th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">リリース日</th><th width="15%">関連ドキュメント</th>  
</tr> 
<tr>
    <td> SDK 5.1.123 簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> Androidバージョンで、RESTAPIが配信するグループのカスタムされたシステムメッセージを受信できない問題を修正しました。</li>
            <li> メッセージのrandomフィールドの生成方法を最適化しました。</li>
            <li> ログプリントの位置決めについての問題を最適化しました。</li>
            <li> ネットワークモジュールの偶発的なcrashの問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-31 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.122 簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> セッションのドラフトを設定すると、コールバックしなくなる可能性がある問題を修正しました。</li>
            <li> findMessageでメッセージをさがす時、メッセージ送信者の情報が補完されない問題を修正しました。</li>
            <li> ローカルにメッセージを挿入した後、findMessageを介してメッセージをさがすと失敗する可能性がある問題を修正しました。</li>
            <li> グループメッセージの受信の選択項目を設定するとセッションオブジェクトが更新されない問題を修正しました。</li>
            <li> 個人のニックネーム・プロフィール画像またはグループのニックネーム・プロフィール画像を変更すると、セッション変更通知がスローされない問題を修正しました。</li>
            <li> ローカルメッセージを挿入した時に、対応するセッションの最後のメッセージが更新されない問題を修正しました。</li>
            <li> 個人プロファイル更新サイクルのクラウド制御を開始しました。</li>
            <li> iOSプラットフォームで、DictionaryとArrayの不正な操作により偶発的にCrashが起きる問題を修正しました。</li>
            <li> Androidプラットフォームでメッセージを削除すると偶発的にCrashが起きる問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-25 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.121 簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> グループプロファイル取得のロジックを最適化し、ライブストリーミングにおいて、グループで自分のグループメンバーの情報をプルする必要がなくなりました。</li>
            <li> ログプリントを完備し、デバイスのタイプのフィールドを補完しました。</li>
            <li> C2Cセッションの中でメッセージ取り消しの通知を受信した時、対応するセッションの最後のメッセージの状態が更新されない問題を解決しました。</li>
            <li> ライブストリーミンググループで、ロングポーリングによりメッセージが過度に遅延する問題を修正しました。</li>
            <li> 同じアカウントで繰り返しログインした後に同じライブストリーミンググループに再度参加すると、メッセージのロングポーリングモジュールが、メッセージのプルkeyを更新しない問題を修正しました。</li>
            <li> iOSプラットフォームで、カスタムフィールドにjson配列をインプットすると、受信側のシグナルモジュールの解析で Crashが起きる問題を修正しました。</li>
            <li> Androidプラットフォームで、セッションのドラフトを設定すると偶発的にCrashが起きる問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-18 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.118 簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> メッセージの重複除去のロジックを最適化し、同じメッセージが繰り返しコールバックされる問題を修正しました。</li>
            <li> ローカルにC2Cメッセージを挿入するインターフェースを追加しました。</li>
            <li> グループの未読メッセージを削除および取り消した時に、グループ未読のカウントが減らない問題を修正しました。</li>
            <li> 送信に失敗したメッセージを削除できない問題を修正しました。</li>
            <li> グループセッションを削除する時、すでにグループを退出または対応するグループが解散している場合、削除失敗のコールバックが起きる問題を修正しました。</li>
            <li> グループメッセージの既読の報告を設定する時に、すでにグループを退出または対応するグループが解散している場合、設定失敗のコールバックが起きる問題を修正しました。</li>
            <li> 個人プロファイルの署名設定に失敗する問題を修正しました。</li>
            <li> フレンドをブラックリストに追加すると偶発的なクラッシュが起きる問題を修正しました。</li>
            <li> メッセージ送信と同時にメッセージIDがリターンされない問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-11 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.115 簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> シグナリングのタイムアウトの時間とサーバーの時間の同期を最適化しました。</li>
            <li> 脆弱なネットワークでの接続の確立が偶発的に失敗する問題を修正しました。</li>
            <li> iOSのAPIヘッダーファイルを完備しました。</li>
            <li> Androidで、GsonをJSONで代替するとクラッシュしてしまう問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-04 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>
<tr>
    <td> SDK 5.1.10 標準版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> V2 APIに、グループカスタムフィールドおよびメッセージの複数Elementのサポートを追加しました。</li>
            <li> V2 APIに、ローカル向けにC2Cメッセージを挿入するインターフェースを追加しました。</li>
            <li> 一般のグループとライブストリーミンググループのメッセージロスの問題を最適化しました。</li>
            <li> 送信に失敗したメッセージを削除できない問題を修正しました。</li>
            <li> C2Cセッションの中で、送信した最初のメッセージがオンラインメッセージである場合、開封証明を受信できない問題を修正しました。</li>
            <li> 取り消し済みのメッセージが、メッセージ履歴をプルするインターフェースによって返ってきた後、メッセージの状態が不正確である問題を修正しました。</li>
            <li> IOSプラットフォームで、フレンドグループ取得のインターフェースにグループ名をブランクのままインプットすると、すべてのグループ情報が戻ってこなくなる問題を修正しました。</li>
            <li> 安定性の問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-04 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr> 
<tr>
    <td> SDK 5.1.111 簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> ログプリントを完備しました。</li>
            <li> 若干の安定性の問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-12-01 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr> 
</table>


## 2020年11月

<table>
<tr>
    <th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">リリース日</th><th width="15%">関連ドキュメント</th>  
</tr> 
<tr>
    <td> SDK 5.1.110 簡易版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> V2 API のすべてのインターフェースを補完しました。</li>
            <li> セッション機能を補完しました。</li>
            <li> リレーションシップチェーン機能を補完しました。</li>
            <li> グループ@機能を追加しました。</li>
            <li> iOSでiPhoneとiPadの同時オンラインをサポートしました。</li>
            <li> 送信メッセージで複数Elementをサポートしました。</li>
            <li> グループプロファイルのカスタムフィールドを補完しました。</li>
            <li> 若干の安定性の問題を修正しました。</li>
        </ul>
    </td>
    <td> 2020-11-26 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr> 
<tr>
    <td> SDK 5.1.2 標準版をリリース</td>
    <td>
        <ul style="margin:0">
            <li> iOSでiPhoneとiPadの同時オンラインをサポートしました。</li>
            <li> Macでarm64アーキテクチャをサポートしました。</li>
            <li> Androidバージョンの安定性の問題を修正しました。</li>
            <li> 標準TRTC依存パッケージで代替します。</li>
        </ul>
    </td>
    <td> 2020-11-12 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr> 
<tr>
    <td> SDK 5.1.1 標準版をリリース</td>
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
        その他の更新内容については、 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください。
    </td>
    <td> 2020-11-05 </td>
    <td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>   
</table>


## 2020年10月

<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>
<td>SDK 5.0.108 簡易版をリリース</td>
<td>
    <li>iOSバージョンで、安定性の問題を修正しました。</li>
    <li>Androidバージョンで偶発的に起きるメッセージがコールバックされない問題を修正しました。</li>
</td>
<td> 2020-10-23 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a> </td>
</tr><tr>
<td> SDK 5.0.10 標準版をリリース</td>
<td><ul style="margin:0">
    <li> シグナルインターフェースを最適化し、オンラインメッセージonlineUserOnlyとオフラインプッシュ情報offlinePushInfoのパラメータの設定をサポートしました。</li>
    <li> 単一セッションを取得するインターフェースの非同期コールバックを最適化しました。</li>
    <li> セッションに取得したグループタイプのインターフェースを追加し、セッションリストのフィルタリング表示ができるようにしました。</li>
    <li> グループライブストリーミング機能を新たに追加し、マイク接続、ギフト、美顔、ボイスチェンジャーなどの機能を取り揃えました。</li>
    <li> 大型ライブルームを新たに追加し、マイク接続、PK、「いいね」、ギフト、美顔、弾幕、フレンド・フォローなどをサポートしました。</li>
    <li> 音声/ビデオシグナルの識別の問題を最適化しました。</li>
</ul></td>
<td> 2020-10-15 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr>   
</table>


## 2020年09月

<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>
<td> SDK 5.0.106 バージョンをリリース（Android & iOS 簡易版）</td>
<td>既知の安定性の問題を修正しました。</td>
<td> 2020-09-21 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a> </td>
</tr><tr>
<td> SDK 5.0.6 標準版をリリース</td>
<td><ul style="margin:0">
    <li>グループ@機能を追加しました。</li>
    <li>iOSとAndroidにdeleteMessagesインターフェースを新たに追加しました。ローカルおよびローミングメッセージを同時に削除します。</li>
    <li>deleteConversationインターフェースは、セッションを削除すると同時に、ローカルおよびローミングメッセージも削除します。</li>
    <li>API2.0インターフェースに、ユーザープロファイル、フレンドプロファイル、グループメンバープロファイルのカスタムフィールドの設定と取得のためのインターフェースを補充しました。</li></ul>
その他の更新内容については、 <a href="https://intl.cloud.tencent.com/document/product/1047/34282">更新ログ</a>をご参照ください。</td>
<td> 2020-09-18 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>
</tr><tr>
<td> SDK 5.0.102 バージョンをリリース（Android & iOS 簡易版）</td>
<td><ul style="margin:0">
    <li>Android & iOS 簡易版SDKをリリース</li>
    <li>簡易版SDKは、既存の標準版をベースに、フレンドとセッションの2つの機能をカットして、一部の業務ロジックに対しては最適化を行うことにより、さらに高い実行効率と、インストールパッケージ容量増加のさらなる縮小を実現しています。</li>
</ul></td>
<td> 2020-09-04 </td>
<td> <a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード </td>
</tr>
</table>

## 2020年07月

<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>    
<td>SDK 4.9.1バージョンをリリース（Android、iOS および Windows 端末）</td>   
<td><ul style="margin:0;">
    <li>海外でのログインの問題を最適化しました。</li>
    <li>海外の一部エリアにおけるファイルアップロード失敗の問題を修正しました。</li>
    <li>@記号を含むアカウントのファイルアップロード失敗の問題を修正しました。</li>
    <li>C2C未読数の偶発的なエラーの問題を修正しました。</li>
    <li>セッションのshowNameの表示における偶発的な異常の問題を修正しました。</li>
    <li>ファイルタイプメッセージのダウンロードurlを取得するインターフェースを追加しました。</li>
    <li>iOSにおいて、ネットワーク切断時のC2Cメッセージ取得にコールバックがない問題を修正しました。</li>
    <li>Androidにおいて、シグナル解析インターフェースの偶発的なクラッシュの問題を修正しました。</li>
    <li>Androidにおいて、メッセージの中のオフラインプッシュ情報の取得時に起きる偶発的クラッシュの問題を修正しました。</li>
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


## 2020年6月

<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>    
<td>SDK 4.8.50バージョンをリリース（Android、iOS および Windows端末）</td>   
<td><ul style="margin:0;">
    <li>API 2.0インターフェースにおいて、ライブストリーミンググループ（AVChatRoom）に参加者があった後、 onMemberEnterのコールバックがない問題を修正しました。</li>
    <li>API 2.0インターフェースのonGroupInfoChangedとonMemberInfoChangedのコールバックにgroupIDのパラメータを追加しました。</li>
    <li>C2Cメッセージ送信が成功した後にセッション更新のコールバックがない問題を修正しました。</li>
    <li>アカウントを切り替えて同じライブストリーミンググループ（AVChatRoom）に参加するとメッセージを受信できない問題を修正しました。</li>
    <li>偶発的に起きる、ログイン後の未読メッセージの同期において、コールバックの順序が正しくない問題を修正しました。</li>
    <li>シグナルインターフェースを追加しました。</li>
    <li>ライブストリーミンググループ（AVChatRoom）にカスタマイズのグループ属性インターフェースを追加しました。</li>
    <li>既知のクラッシュの問題を修正しました。</li>
    <li>Android Qバージョンとの互換性をはかるため、ログのデフォルトの保存先を /sdcard/Android/data/パッケージ名/files/log/tencent/imsdkに修正しました。</li>
    <li>Windowsプラットフォームにおいて、グループ作成時のグループメンバーのロールの問題を修正しました。</li>
    <li>TUIKitでAPI 2.0インターフェースを代替しました。</li>
    <li>TRTCを結合させ、オーディオビデオ通話機能を実現しました。</li>
    <li>iOSのTUIKitに、ダークカラーモードを追加しました。</li>
    <li>AndroidXをサポートしました。</li>
</ul></td>   
<td>2020-06-22</td>   
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>   
</tr> </table>

## 2020年05月

<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>    
<td>SDK 4.8バージョンをリリース（Android、iOS および Windows端末）</td>   
<td><ul style="margin:0;">
    <li>iOS & Androidにおいて、最新のAPI 2.0インターフェースをリリースしました。</li>
    <li>iOSとAndroidでIPv6をサポートします。</li>
    <li>ライブストリーミンググループ（AVChatRoom）でグループメンバーリストの動的更新をサポートします。</li>
    <li>xlogクラッシュの問題を修正しました。</li>
    <li>iOSでBig Fileを送信すると必ず失敗する問題を修正しました。</li>
    <li>iOSにおいて、メッセージ送信者のフレンドノートをプルすると異常が起きる問題を修正しました。</li>
    <li>IM SDKがAndroidXをサポートしました。</li>
    <li>Androidデバイスのネットワーク権限の問題によるクラッシュを修正しました。</li>
</ul></td>   
<td>2020-05-15</td>   
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>   
</tr> </table>


## 2020年03月

<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>    
<td>SDK 2.6バージョンをリリース（ミニプログラムおよびWeb端末）</td>   
<td><ul style="margin:0">
    <li>Web端末でビデオメッセージの作成・送信をサポートし、最大100MBのビデオファイルの送信が可能になります。</li>
    <li>Messageに<code>nick</code>と<code>avatar</code>の属性を追加し、これを音声/ビデオチャットルーム（AVChatRoom）内のメッセージ送信者のニックネームとプロフィール画像URLの表示に使用します（事前にupdateMyProfile の呼び出しによる設定が必要です）。</li>
    <li>Web版で、マルチインスタンスでログインした時、C2Cメッセージの取り消し通知が各インスタンスにおいて同期できるようになりました。</li>
    <li>updateGroupProfileを呼び出してグループカスタムフィールドの修正を完了した後、グループメンバーがグループのプロンプトを受信でき、関連する内容 Message.payload.newGroupProfile.groupCustomFieldを取得できるようになります。</li>
    <li>TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVEDインターフェースを破棄し、MESSAGE_RECEIVEDで代替します。</li>
    <li>getGroupListインターフェースを呼び出した時の偶発的なエラーの問題を修正しました。</li></ul></td>   
<td>2020-03-30</td>   
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">SDKダウンロード</a></td>   
</tr><tr>      
<td>SDK 4.7バージョンをリリース（Android、iOS および Windows 端末）</td>   
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
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 4.6バージョンの継続的な最適化（Android、iOS および Windows端末）</td>   
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
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 2.4バージョンをリリース（ミニプログラムおよびWeb端末）</td>   
<td><ul style="margin:0;">
    <li>メッセージ取り消しのインターフェースrevokeMessageを新たに追加しました。</li>
    <li>MessageにisRevokedの属性を追加し、値がtrueの時は取り消されたメッセージを表示します。</li>
    <li>メッセージが取り消されたイベント通知 TIM.EVENT.MESSAGE_REVOKEDを新たに追加しました。</li>
    <li>退場によるオフラインのイベント通知 TIM.EVENT.KICKED_OUT に、退場によるオフラインのタイプとして、複数端末ログインによる退場と UserSig失効による退場を追加しました。</li>
    <li>createFileMessageのアップロードファイルサイズを20Mから100MBに調整しました。</li>
    <li>グループプロンプトメッセージのmsgMemberInfoとshutupTimeはまもなく破棄されます。memberListと muteTimeを代替として使用してください。</li>
    <li>コンソールに、IMのAIBotのエントリーを新たに追加しました。</li>
    <li>offインターフェースを呼び出して、モニタリングイベントをキャンセルできない問題を修正しました。</li>
    <li>MessageのisReadの属性値とタイプが正しくない問題を修正しました。</li>
    <li>ビデオメッセージの送信時に、ビデオファイルが最大制限値を超えた後のエラーコードとエラー情報に誤りがある問題を修正しました。</li>
    <li>偶発的に起きる、カスタムフィールド更新後のフィールドの内容が正しくない問題を修正しました。</li>
    <li>ログイン後に音声/ビデオチャットルームタイプのグループに参加すると、JOIN_STATUS_ALREADY_IN_GROUPが偶発的に起きる問題を修正しました。</li>
    <li>core-jsによる潜在的な性能面の問題を修正しました。</li></ul></td>   
<td>2020-01-03</td>   
<td>-</td>   
</tr> </table>

## 2019年12月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>「フラッグシップ版」パッケージのサービスを開始</td>   
<td>「フラッグシップ版」パッケージのサービスを開始しました。これには、「無制限音声/ビデオチャットルーム」、「30日間のメッセージ履歴保存」、「グループメンバー数上限2000人」などが含まれ、1回の購入でより多くの機能がサポートされています。</td>   
<td>2019-12-26</td>   
<td><ul style="margin:0;">
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34349">課金概要</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34350">料金説明</a></li>
    <li><a href="https://intl.cloud.tencent.com/document/product/1047/34577">アプリケーションの作成とアップグレード</a></li></ul></td>   
</tr><tr>      
<td>SDK 4.6バージョンの継続的な最適化（Android、iOS および Windows端末）</td>   
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
    <li>TIM.TYPES.GRP_AVCHATROOMタイプのグループのメッセージ通知効率を最適化し、使用体験を大幅に向上させました。</li>
    <li>メッセージ送信失敗時に SDKが返す実際のエラーコードとエラー情報を調整しました。</li>
    <li>logout呼び出し時に現在のインスタンスのメッセージチャネルのみログアウトするように調整しました。</li>
    <li>アクセス側がインプットするコールバック関数に対して安全にカプセル化し、コールバック関数のロジックにエラーがあったときに、異常をキャプチャし迅速に問題の位置を特定できるようにしました。</li>
    <li>IMサーバーのエラーコードに遭遇した時、SDKが中国語のエラー情報を出力します。</li>
    <li>WeChat Mini Program環境で長時間バックエンドに切り替え、再度フロントエンドに切り替えると、偶発的にメッセージロスが起きる問題を修正しました。</li>
    <li>1回のメッセージ送信で複数回のTIM.EVENT.CONVERSATION_LIST_UPDATEDがトリガーされる問題を修正しました。</li>
    <li>registerPluginを呼び出さない、またはインターフェースの入力パラメータに間違いがあり、画像等のファイルをアップロードする時にSDKがエラーを報告する問題を修正しました。</li>
    <li>TIM.TYPES.GRP_AVCHATROOMタイプのグループを解散した後、ロングポーリングが停止されない問題を修正しました。</li>
    <li>「複数のインスタンス」または「複数の端末」のログインを有効にした時、1つのWebインスタンスをログアウトするとその他インスタンスまたはその他端末もメッセージを受信できなくなる問題を修正しました。</li>
    <li>偶発的に起きる、プルしたセッションリストの構造上の問題によりSDKがエラーを報告する問題を修正しました。</li></ul></td>  
<td>2019-12-13</td>   
<td>-</td>   
</tr> </table>

## 2019年11月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 2.2バージョンをリリース（ミニプログラムおよびWeb端末）</td>   
<td><ul style="margin:0;">
    <li>Mini Programにおいて、ビデオメッセージを作成・送信するcreateVideoMessageを新たにサポートし、ビデオメッセージのマルチプラットフォーム相互通信ができるようになりました（TUIKitおよびSDKを最新バージョンにアップデートする必要があります）。</li>
    <li>グループメンバーのプロファイルをクエリーするインターフェースgetGroupMemberProfileを新たに追加しました。</li>
    <li>Native IM v3.xから送信された音声、ファイルメッセージとの互換性をサポートしました。</li>
    <li>位置情報メッセージGeoPayloadの受信を新たにサポートしました。</li>
    <li>ログアウトした後、TIM.TYPES.GRP_AVCHATROOMタイプのグループのロングポーリングが依然として動作している問題を修正しました。</li>
    <li>TIM.TYPES.GRP_AVCHATROOM タイプのグループのメッセージインスタンスの中のグループネームカードに値がない問題を修正しました。</li>
    <li>IE 10ブラウザにおける報告エラーの問題を修正しました。</li>
    <li>匿名でグループに参加できない問題を修正しました。</li></ul></td>   
<td>2019-11-21</td>   
<td>-</td>   
</tr><tr>      
<td>SDK 4.6バージョンをリリース（Android、iOS および Windows端末）</td>   
<td><ul style="margin:0;">
    <li>メッセージ取り消しのローミングをサポートしました。</li>
    <li>iOS/Mac端末において、OPPOChannelIDの設定を追加し、Android 8.0以上のOPPO携帯がiOSメッセージプッシュの受信に失敗する問題を修正しました。</li>
    <li>iOS/Mac端末において、 getGrouplistのリターンのオブジェクトの注釈を最適化しました。</li>
    <li>OPPO携帯（システム要件：8.0以上）のオフラインプッシュのchannleIDについて、コンソールでの設定をサポートしました。</li>
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
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>刷新したコンソールのサービスを開始</td>   
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
<td>SDK 4.5バージョンの継続的な最適化（Android、iOS および Windows端末）</td>   
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
    <li>TIM.TYPES.MSG_SOUNDを破棄し、TIM.TYPES.MSG_AUDIOで代替します。</li>
    <li>getMessageListインターフェースが削除済みのグループチャットセッションのメッセージをプルできない問題を修正しました。</li>
    <li>グループシステムの通知にグループ名がない問題を修正しました。</li>
    <li>メッセージを受信して新規作成したセッションにプロファイルがない問題を修正しました。</li></ul></td>   
<td>2019-10-16</td>   
<td>-</td>   
</tr> </table>

## 2019年09月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 2.0バージョンをリリース（ミニプログラムおよびWeb端末）</td>   
<td>IM Mini Programおよびウェブページ版SDKを刷新し、各モジュールの安定性を最適化して、アクセス体験を全面的に向上させました。さらに可視化によるDemoを提供し、顧客が直接体験できるようにしています。</td>   
<td>2019-09-19</td>   
<td>-</td>   
</tr><tr>      
<td>SDK 4.5バージョンの継続的な最適化（Android、iOS および Windows端末）</td>   
<td><ul style="margin:0;">
    <li>Androidに開封証明を追加しました。</li>
    <li>ネットワーク接続の品質を最適化しました。</li>
    <li>グループ/グループメンバーのカスタムフィールドをプルするロジックを最適化しました。</li></ul></td>   
<td>2019-09-18</td>   
<td>-</td>   
</tr> </table>

## 2019年08月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 4.5バージョンをリリース（Android、iOS および Windows端末）</td>   
<td><ul style="margin:0;">
    <li>チャットの音声メッセージ、MotionEvent.ACTION_CANCELイベントの処理を新たに追加しました。</li>
    <li>セッションリスト、チャット画面、詳細プロファイル、連絡先を新たに追加し、プロフィール画像表示機能を追加しました。</li>
    <li>個人プロファイルのプロフィール画像を修正する機能を新たに追加しました。</li>
    <li>オフラインプッシュ機能へのIntentリダイレクトを新たに追加しました。</li>
    <li>シングルチャット、グループチャットのセッションで、ランダムプロフィール画像を新たに追加しました。</li>
    <li>グループメンバーの管理者設定許可および管理者設定取り消しのプロンプトを新たに追加しました。</li>
    <li>グループメンバーのミュートおよびミュート取り消しのプロンプトを新たに追加しました。</li>
    <li>未読メッセージ数のカウントを最適化しました。</li>
    <li>ログイン後の最新セッションリストのロード速度を最適化しました。</li>
    <li>ログ消去の機能を追加しました。</li>
    <li>Android端末でcom.tencent.imsdk.TIMGroupReceiveMessageOptクラスを一元化して使用します。</li>
    <li>TUIKit/Demoの中に触覚フィードバックを追加しました。ユーザーはTUIKitの使用時、フィードバックを自主的に設定し、カスタマイズすることが可能です。</li>
    <li>TUIKit/Demoにカスタムメッセージ送信を新たに追加しました。</li>
    <li>TUIKit/DemoにC2Cの開封証明を新たに追加しました。</li>
    <li>TUIKit/Demoに未再生音声の赤点灯表示を新たに追加しました。</li>
    <li>TUIKit/Demoにプロフィール画像をクリックして大きな画像で見る機能を追加しました。</li>
    <li>TUIKit/Demoのグループチャットで、灰色の小型バーのスタイルを調整すると、ユーザーニックネームが青色に変わり、ニックネームをクリックするとユーザー情報画面に移動できます。</li>
    <li>チャットのトップ設定のロジックを最適化し、最も近い時間から順番に表示します。</li>
    <li>Demoの中のグループ内ニックネームの表示ロジックを最適化しました。</li>
    <li>チャット画面の中のプロフィール画像を表示するロジックを最適化しました。</li>
    <li>未読メッセージ数のカウントを最適化しました。</li>
    <li>ログイン後の最新セッションリストのロード速度を最適化しました。</li>
    <li>海外ユーザーがファイルメッセージを送信する速度を最適化しました。</li></ul></td>   
<td>2019-08-30</td>   
<td>-</td>   
</tr><tr>      
<td>Instant Messaging（IM）の中国語名称を「即時通信」に変更</td>   
<td>“Instant Messaging（IM)”の中国語名称を「雲通信」から「即時通信」に変更しました。</td>   
<td>2019-08-06</td>   
<td>-</td>   
</tr> </table>

## 2019年07月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 4.4バージョンの継続的な最適化（Android、iOS および Windows端末）</td>   
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
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 4.4バージョンおよび刷新したDemoをリリース（Android、iOS および Windows端末）</td>   
<td><ul style="margin:0;">
    <li>刷新したモバイルクライアントUI設計のTUIKitおよび製品Demoのサービスを開始しました。</li>
    <li>Demoの連絡先、グループ管理、リレーションシップチェーンなどの機能を完備しました。</li>
    <li>キャッシュ最適化により、UIのラグを減少させました。</li>
    <li>メッセージ送信の効率を最適化しました。</li>
    <li>クロスプラットフォームライブラリのメッセージに、メッセージの一意性IDを取得するためのJSON keyを追加しました。</li></ul></td>   
<td>2019-06-27</td>   
<td>-</td>   
</tr> </table>

## 2019年05月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
            <td>SDK 4.3バージョンの継続的な最適化（Android、iOS および Windows端末）</td>   
<td><ul style="margin:0;">
    <li>TIMFriendshipManager クラスの中に querySelfProfile および queryUserProfileインターフェース（ローカルデータ読み取り）を追加しました。</li>
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
    <li>iOSにおいて、 Wi-Fi切り替え時のネットワーク再接続が遅い問題を最適化しました。</li>
    <li>グループメッセージの同期の問題を最適化しました。</li></ul></td>   
<td>2019-05-24</td>   
<td>-</td>   
</tr> </table>

## 2019年04月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 4.3バージョンをリリース（Android、iOS および Windows端末）</td>   
<td><ul style="margin:0;">
    <li>フレンドのブラックリスト機能、フレンドグループ分け機能、フレンド追加リクエスト処理などのリレーションシップチェーン機能を追加しました。</li>
    <li>未読数カウントに関する問題を最適化しました。</li>
    <li>メッセージ既読状態についての問題を修正しました。</li>
    <li>REST APIが送信するC2Cメッセージの順序異常の問題を最適化しました。</li>
    <li>ローミングメッセージの取得に偶発的に繰り返しが生じる問題を最適化しました。</li>
    <li>uniqueIdの空実装の問題を最適化しました。</li>
    <li>TIMMessageのsenderProfileによってユーザーのプロファイル情報が取得できない問題を最適化しました。</li>
    <li>開封証明のコールバックおよび状態の問題を修正しました。</li>
    <li>未読メッセージの同期をとる時、最も新しいメッセージがコールバックされない問題を修正しました。</li>
    <li>グループメッセージが偶発的に受信できなくなる問題を修正しました。</li>
    <li>IP接続とlogin情報の統計報告を追加しました。</li></ul></td>   
<td>2019-04-24</td>   
<td>-</td>   
</tr> </table>

## 2019年03月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 4.2バージョンをリリース（Android、iOS および Windows端末）</td>   
<td><ul style="margin:0;">
    <li>iOS端末において、TUIKit.frameworkのbitcode 2のサポートを新たに追加しました。</li>
    <li>iOS端末において、podによる直接的なTUIKit.frameworkの統合を新たにサポートしました。</li>
    <li>Windows端末において、duilibライブラリをUIコンポーネントとするIM Demoを新たに追加しました。</li>
    <li>Windows端末において、/source-charset:.65001のコンパイルの選択項目を新たに追加しました。</li>
    <li>Web端末において、WEBIMを新たに追加し、現在すでに 「.amr」録音形式の再生をサポートしています。</li>
    <li>フレンドの追加/削除/クエリーのロジックを新たに追加しました。</li>
    <li>新旧バージョンの音声、ファイル、ビデオメッセージの相互通信の問題を修正しました。</li>
    <li> TUIkitの音声再生ロジックを最適化しました。</li>
    <li>AVChatRoomの入室が100人を超えた後のメッセージ受信異常の問題を修正しました。</li>
    <li>グループのミュートが無効になる問題を修正しました。</li>
    <li>ユーザーのグループ内身分変更機能を修正しました。</li>
    <li>グループメッセージ受信のオプションの変更を修正しました。</li>
    <li>オフラインプッシュのスイッチング無効の問題を修正しました。</li>
    <li>ユーザーのグループ内身分変更機能を修正しました。</li>
    <li>グループの未決および既決情報取得のリターンが正しくない問題を修正しました。</li>
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
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 4.0バージョンをリリース（Android、iOS および Windows端末）</td>   
<td>刷新したIMクライアントSDKをリリースし、大規模なネットワーク接続、メッセージ送受信および未読数などの問題を修正し、ネットワーク、メッセージ等の重要な基盤モジュールの安定性を大幅に改善しました。さらにオープンソースのTUIKitを提供し、顧客のアクセス手順を簡素化しています。</td>   
<td>2019-01-21</td>   
<td>-</td>   
</tr> </table>

## 2017年07月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>UGC（ショート動画）をサポートしました</td>   
<td>UGC（ショート動画）のメッセージ機能をサポートしました。ビデオ編集によってコンテンツがより良質になり、ユーザーエクスペリエンスがさらに向上します。</td>   
<td>2017-07</td>   
<td>-</td>   
</tr> </table>

## 2017年05月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>SDK 3.0バージョンをリリース</td>   
<td>機能をさらに取り揃え、容積をより小さくし、コード体系を最適化しました。顧客の統合効率とダウンロード体験を効果的に向上させています。</td>   
<td>2017-05</td>   
<td>-</td>   
</tr> </table>

## 2016年12月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>複数のインスタンスによる相互排他機能をサポートしました</td>   
<td>Web端末において、複数インスタンスによる相互排他のニーズを満たし、Web端末によるカスタマーサービスなどのシナリオのニーズに応えます。</td>   
<td>2016-12</td>   
<td>-</td>   
</tr> </table>

## 2016年08月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>メッセージ同報機能をサポートしました</td>   
<td>全員への同報メッセージプッシュをサポートし、メッセージの伝播の効率を引き上げ、クライアントのプッシュのニーズに応えています。</td>   
<td>2016-08</td>   
<td>-</td>   
</tr><tr>      
<td>マルチ端末の同時ログインをサポートしました</td>   
<td>マルチ端末の同時ログインをサポートし、携帯とPCを同時に使用するシナリオに対応し、体験を効果的に向上させ、最適化しています。</td>   
<td>2016-08</td>   
<td>-</td>   
</tr> </table>

## 2016年05月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>ライブストリーミングチャットルームのサービスを開始</td>   
<td>ライブストリーミングシナリオを対象に、人数無制限のライブストリーミングチャットルームをサポートします。またメッセージ頻度の制限、メッセージのカスタマイズなどのシナリオ化のニーズにも対応しています。</td>   
<td>2016-05</td>   
<td>-</td>   
</tr> </table>

## 2016年03月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>メッセージプッシュ機能をサポートしました</td>   
<td> AndroidおよびiOSのオフラインプッシュ機能をサポートしました。メッセージによるアプローチをさらに保障し、体験を効果的に向上させ、最適化します。</td>   
<td>2016-03</td>   
<td>-</td>   
</tr> </table>

## 2015年12月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>ミニビデオのメッセージタイプをサポートしました</td>   
<td>ミニビデオのメッセージタイプをサポートし、メッセージコンテンツをより豊かにしました。</td>   
<td>2015-12</td>   
<td>-</td>   
</tr> </table>

## 2015年08月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>Webプラットフォームをサポートしました</td>   
<td> WebプラットフォームのIMクラウドサービスをサポートし、顔絵文字のカスタマイズなど、メッセージの種類を追加しました。</td>   
<td>2015-08</td>   
<td>-</td>   
</tr> </table>

## 2015年07月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>Windowsプラットフォームをサポートしました</td>   
<td>WindowsプラットフォームのIMクラウドサービスをサポートし、地理位置、音声などのメッセージの種類を追加しました。</td>   
<td>2015-07</td>   
<td>-</td>   
</tr> </table>

## 2015年05月
<table>
<tr><th width="20%">動的名称</th>  <th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>  
</tr> <tr>     
<td>Instant Messaging（IM）（中国語名称「即時通信」：旧名称「雲通信」）のサービスを開始</td>   
<td>AndroidおよびiOSのIMクラウドサービスをサポートし、グラフィック、顔絵文字など多様なメッセージタイプをサポートしています。</td>   
<td>2015-05</td>   
<td>-</td>   
</tr> </table>

