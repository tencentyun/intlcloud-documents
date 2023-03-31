## 機能説明
ユーザーがアプリにログインすると、最近のセッションのリストを表示し、ターゲットセッションを簡単に見つけることができます。
セッションリスト機能は、主にセッションリストの取得とセッションリストの更新処理に分けられます。
この文書では、具体的な実装の詳細について説明します。

## セッションリストの取得
`getConversationList`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/getConversationList.html))を呼び出すことで、セッションリストを取得できます。このインターフェースは、ローカルにキャッシュされたセッションをプルします。サーバーセッションが更新されると、SDK内部は自動的に同期され、`V2TIMConversationListener`コールバックでクライアントに通知されます。

ユーザーのセッションはリスト形式で返され、リストには`V2TIMConversation`オブジェクトが格納されます。現在、IM SDKは次のようにセッションリストを並べ替えます：
* Flutter SDK 3.8.0以降のバージョンでは、このインターフェースで取得したセッションリストは、デフォルトでセッションオブジェクトの`orderKey`によって並べ替えられています。`orderKey`の値が大きいほど、セッションは前に並べ替えられます。`orderKey`フィールドは整数型です。新しいメッセージを送信・受信したり、下書きを設定したり、またはセッションをピン留めしたりする場合、セッションが有効になり、`orderKey`フィールドの値が増加します。
* Flutter SDK 3.8.0より前のバージョンでは、このインターフェースで取得したセッションリストは、デフォルトでセッション`lastMessage` -> `timestamp`によって並べ替えられています。`timestamp`が大きいほど、セッションがより前に並べ替えられます。

> ! 一部のシナリオでは、セッションの`lastMessage`が空になる（セッションメッセージのクリアなど）場合があります。5.5.892より前のバージョンのSDKを使用している場合は、`lastMessage`で並べ替えるときにこのような異常を追加で処理する必要があります。5.5.892以降のバージョンにアップデートして、並べ替えに`orderKey`フィールドを使用することをお勧めします。

`getConversationList`では、ワンタイムプルまたはページ別でのプルを実現できます。以下の説明をご参照ください。

### ワンタイムプル
ワンタイムプルは、セッション数が比較的少ない（100個以内）場合に適しています。このような場合は、プルするcountをINT_MAXに設定できます(通常、セッション数はINT_MAXに達しません)。

サンプルコードは次のとおりです：


```dart
V2TimValueCallback<V2TimConversationResult> convList = await TencentImSDKPlugin.v2TIMManager.getConversationManager().getConversationList(nextSeq: '0',count: 100);
```
### ページ別でのプル
運用シナリオで多数のセッションが生成された場合は、読み込みの効率とネットワークトラフィックの節約の理由により、ページ別でのプル方法を使用することをお勧めします。1ページあたり100個を超えないようにすることをお勧めします。

ページ別でのプルの手順：
1. `getConversationList`を初めて呼び出す場合は、パラメータ`nextSeq`を0（セッションリストを最初からプルすることを意味します）に、`count`を50（一度に50件のセッションオブジェクトをプルすることを意味します）に指定します。
2. セッションリストが初めて正常にプルされた後、`getConversationList`のコールバック結果`V2TIMConversationResult`には、`nextSeq`（ページ別でのプルの次のフィールド）、`isFinish`（セッションプルが完了したかどうか）が含まれます。
   * `isFinished`がtrueの場合は、すべてのセッションのプルが完了したことを意味します。
   * `isFinished`がfalseの場合は、プルできるセッションがさらにあることを意味します。これは「次のページ」のセッションリストのプルをただちに開始する必要があることを意味するものではありません。一般的な通信ソフトウェアでは、ページ別でのプルは、通常、ユーザーのスライド操作によってトリガーされ、ユーザーがセッションリストをプルアップするたびに、ページ別でのプルがトリガーされます。
3. ユーザーが引き続き会話リストをプルアップし、プルする会話がさらにある場合は、`getConversationList`インターフェースを引き続き呼び出して、新しいラウンドの`nextSeq`および`count`パラメータを渡すことができます（数値の由来は前回のプルによって返された`V2TIMConversationResult`オブジェクトです）。
4. `isFinished`がtrueを返すまで**ステップ3**を繰り返します。

サンプルコードは次のとおりです：


```dart
    //セッションリストの取得
    V2TimValueCallback<V2TimConversationResult> getConversationListRes =
        await TencentImSDKPlugin.v2TIMManager
            .getConversationManager()
            .getConversationList(
            count: 100, //ページ別でプルする数。ページ別で1回のプル数を多くしすぎないようにしてください。プルの速度に影響を及ぼします。毎回100セッションをプルすることをお勧めします。
            nextSeq: "0"//ページ別でプルするカーソル。初めてプルする場合、デフォルトで0が渡され、その後、前回正常に完了した「ページ別でのプル」のコールバックにあるnextSeqがページ別でプルされ、渡されます。
            );
    if (getConversationListRes.code == 0) {
      //取得に成功しました
      bool? isFinished = getConversationListRes.data?.isFinished;//プルが完了したかどうか
      String? nextSeq = getConversationListRes.data?.nextSeq;//後でページ別でプルするカーソル
      List<V2TimConversation?>? conversationList =
          getConversationListRes.data?.conversationList;//今回プルしたメッセージリスト
      //プルがすべて完了していない場合は、返されたnextSeqを使用して、isFinishedがtrueになるまでプルを続けます。
      if (!isFinished!) {
        V2TimValueCallback<V2TimConversationResult> nextConversationListRes =
            await TencentImSDKPlugin.v2TIMManager
                .getConversationManager()
                .getConversationList(count: 100, nextSeq: nextSeq = "0");//返されたnextSeqを使用して、isFinishedがtrueになるまでプルを続けます。
      }

      getConversationListRes.data?.conversationList?.forEach((element) {
        element?.conversationID;//セッションの一意のID。個人チャットの場合、その形式はc2c_userIDです。グループチャットの場合、その形式はgroup_groupIDです。
        element?.draftText;//メッセージの下書き
        element?.draftTimestamp;//下書きの編集時間。下書き設定時に自動的に生成されます。
        element?.faceUrl;//表示されるセッションのプロフィール写真。グループチャットのプロフィール写真：グループのプロフィール写真。個人チャットのプロフィール写真：相手のプロフィール写真。
        element?.groupAtInfoList;//グループ会話の@メンション情報リスト。通常、「他のメンバーが自分に@メンション」または「全員に@メンション」の2つのリマインダー状態を表示するために使用されます。
        element?.groupID;//現在のグループチャットID。セッションタイプがグループチャットの場合、groupIDは現在のグループのIDとして保存されます。グループチャットでない場合、値はnullになります。
        element?.groupType;//現在のグループチャットのタイプ。セッションタイプがグループチャットの場合、groupTypeは現在のグループタイプになります。グループチャットでない場合、値はnullになります。
        element?.isPinned;//セッションがピン留めされているかどうか
        element?.lastMessage;//セッションの最後のメッセージ
        element?.orderkey;//セッションの並べ替えフィールド
        element?.recvOpt;//メッセージの受信オプション
        element?.showName;//表示されるセッション名。グループチャットのセッション名の優先度：グループ名 > グループID。個人チャットのセッション名の優先度：相手となる友達の注釈 > 相手のニックネーム > 相手のuserID。
        element?.type;//セッションタイプ。2C（個人チャット）とGroup（グループチャット）に分けられます。
        element?.unreadCount;//セッション内の未読メッセージの数。ライブ配信グループ（AVChatRoom）は未読カウントをサポートしていません。既定値は0です。
        element?.groupID;//相手のユーザーID。セッションタイプが個人チャットの場合、userIDは相手のユーザーIDとして保存されます。個人チャットでない場合、値はnullになります。
      });
    }
```



## セッションリストの更新
IM SDKは、ログイン完了後、ユーザーがオンラインになった後、ネットワークが切断されて再接続された後にセッションリストを自動的に更新します。
セッションリストの利用可能な更新を取得するには、以下の取得手順に従って操作してください：
1. セッションリスナーを追加します。
2. セッション変更通知を受け取り、処理します。
3. セッションリスナーを削除します。このステップはオプションです。サービスロジックに従って、必要に応じて呼び出すことができます。

### セッションリスナーの追加
`addConversationListener`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/addConversationListener.html))を呼び出すことで、セッションリスナーを追加できます。リスナーを追加した後にのみ、セッション変更イベントを受信できます。

サンプルコードは次のとおりです。

```dart
TencentImSDKPlugin.v2TIMManager.getConversationManager().addConversationListener(listener: V2TimConversationListener(onConversationChanged: (conversationList) {
    
  },
	//その他                                                                                                                    ));
```


### セッションの新規変更通知
`V2TIMConversationListener`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Listener/V2TimConversationListener.html))のイベントでセッションリストの変更通知を取得できます。

現在、IM SDKでサポートされているセッション変更イベントを以下に示します。

| イベント                         | 説明                           | 推奨                                                         |
| -------------------------------- | ------------------------------ | ------------------------------------------------------------ |
| onSyncServerStart                | サーバーセッションの同期開始   | ログイン完了後、またはネットワークが切断されて再接続された後、SDKはサーバーセッションを自動的に同期します。このイベントを監視して、いくつかのUI進捗状況を表示させる操作を実行できます。 |
| onSyncServerFinish               | サーバーセッションの同期完了   | セッションに変更が加えた場合、`onNewConversation`/`onConversationChangedによってコールバックされ、通知されます。 |
| onSyncServerFailed               | サーバーセッションの同期失敗   | このイベントを監視して、いくつかのUI異常を表示させる操作を実行できます。 |
| onNewConversation                | 追加したセッションがある       | たとえば、新しい同僚から個人チャットメッセージを受信し、新しいグループに招待された場合は、セッションリストを再度並べ替えることができます。 |
| onConversationChanged            | 更新したセッションがある       | たとえば、未読数が変化した場合、最後のメッセージが更新された場合は、セッションリストを再度並べ替えることができます。 |
| onTotalUnreadMessageCountChanged | 未読セッションの総数の変更通知 | 詳細については、[セッションの未読数](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Message/V2TimConversation.html#unreadcount)をご参照ください。 |

> ? セッションリストの順序が最後のメッセージの並べ替えの原則に従っていることを確認するには、各セッションが変更または追加された後にデータソースの順序を再度並べ替える必要があります。
> * Flutter SDK 3.8.0より前のバージョンを使用している場合は、`lastMessage`で並べ替えることができます。ただし、`lastMessage`が空になっていること（セッションメッセージのクリアなど）を処理することに注意する必要があります。
> * Flutter SDK 3.8.0以降のバージョンを使用している場合は、`orderKey`フィールドを使用して並べ替えます。
> * Flutter SDK 3.8.0以降のバージョンにアップデートすることを強くお勧めします。

サンプルコードは次のとおりです。


```dart
    //グループリスナーを設定する
    V2TimGroupListener listener = V2TimGroupListener(onApplicationProcessed:
        (String groupID, V2TimGroupMemberInfo opUser, bool isAgreeJoin,
            String opReason) async {
      //グループへの参加リクエストは、グループオーナーまたは管理者によって処理されました（申請者のみが受信できます）
      //groupID    グループID
      //opUser    処理者
      //isAgreeJoin    グループへの参加に同意するかどうか
      //opReason    処理理由
    }, onGrantAdministrator: (String groupID, V2TimGroupMemberInfo opUser,
        List<V2TimGroupMemberInfo> memberList) async {
      //管理者のロールを指定する
      //groupID    グループID
      //opUser    処理者
      //memberList    処理されるグループメンバー
    }, onGroupAttributeChanged:
        (String groupID, Map<String, String> groupAttributeMap) async {
      //グループ属性の更新の受信に関するコールバック
      //groupID    グループID
      //groupAttributeMap    グループのすべての属性
    }, onGroupCreated: (String groupID) async {
      //グループを作成する（主に多端末同期に使用）
      //groupID    グループID
    }, onGroupDismissed: (String groupID, V2TimGroupMemberInfo opUser) async {
      //グループが解散された（全員受信可能）
      //groupID    グループID
      //opUser    処理者
    }, onGroupInfoChanged:
        (String groupID, List<V2TimGroupChangeInfo> changeInfos) async {
      //グループメッセージが変更された（全員受信可能）
      //groupID    グループID
      //changeInfos    変更したグループ情報
    }, onGroupRecycled: (String groupID, V2TimGroupMemberInfo opUser) async {
      //グループが回収された（全員受信可能）
      //groupID    グループID
      //opUser    処理者
    }, onMemberEnter:
        (String groupID, List<V2TimGroupMemberInfo> memberList) async {
      //ユーザーがグループに参加した（全員受信可能）
      //groupID    グループID
      //memberList    参加したメンバー
    }, onMemberInfoChanged: (String groupID,
        List<V2TimGroupMemberChangeInfo> v2TIMGroupMemberChangeInfoList) async {
      //グループメンバーのメッセージが変更され、発言禁止通知のみ対応（全員受信可能）。
      //groupID    グループID
      //v2TIMGroupMemberChangeInfoList    変更されたグループメンバー情報
    }, onMemberInvited: (String groupID, V2TimGroupMemberInfo opUser,
        List<V2TimGroupMemberInfo> memberList) async {
      //ユーザーがグループに招待された（全員受信可能）
      //groupID    グループID
      //opUser    処理者
      //memberList    招待されたグループメンバー
    }, onMemberKicked: (String groupID, V2TimGroupMemberInfo opUser,
        List<V2TimGroupMemberInfo> memberList) async {
      //ユーザーがグループから強制退出させられた（全員受信可能）
      //groupID    グループID
      //opUser    処理者
      //memberList    強制退出させられたメンバー
    }, onMemberLeave: (String groupID, V2TimGroupMemberInfo member) async {
      //ユーザーがグループから離れた（全員受信可能）
      //groupID    グループID
      //member    離れたメンバー
    }, onQuitFromGroup: (String groupID) async {
      //自分からグループを退出する（主に多端末同期に使用、ライブ配信グループ（AVChatRoom）の場合は非対応）
      //groupID    グループID
    }, onReceiveJoinApplication:
        (String groupID, V2TimGroupMemberInfo member, String opReason) async {
      //グループに参加するための新しいリクエストがある（グループオーナーまたは管理者のみが受信）
      //groupID    グループID
      //member    申請者
      //opReason    申請理由
    }, onReceiveRESTCustomData: (String groupID, String customData) async {
      //RESTAPIが送信したカスタムシステムメッセージを受信する
      //groupID    グループID
      //customData    カスタムデータ
    }, onRevokeAdministrator: (String groupID, V2TimGroupMemberInfo opUser,
        List<V2TimGroupMemberInfo> memberList) async {
      //管理者のロールを取り消す
      //groupID    グループID
      //opUser    処理者
      //memberList    処理されるグループメンバー
    }, onTopicCreated: (String groupID, String topicID) async {
      //トピックの作成通知
      //groupID    トピックを作成したグループID
      //topicID    作成したトピックID
    }, onTopicDeleted: (String groupID, List<String> topicIDList) async {
      //トピックの作成通知
      //groupID    トピックを削除したグループID
      //topicIDList    削除したトピックIDの一覧
    }, onTopicInfoChanged: (String groupID, V2TimTopicInfo topicInfo) async {
      //トピック情報の更新通知
      //groupID    トピック情報が更新されたグループID
      //topicInfo    トピック情報が更新された属性
    });
    //グループリスナーを追加する
    TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: listener);
```


### セッションリスナーの削除
`removeConversationListener`([クリックして詳細を表示](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/removeConversationListener.html))を呼び出すことで、セッションリスナーを削除できます。削除後、セッション変更イベントを受信できなくなります。
このステップはオプションです。サービスロジックに従って、必要に応じて呼び出すことができます。

サンプルコードは次のとおりです：


```dart
conversationManager.removeConversationListener(conversationListener);
```



### `lastMessage`の更新なしでのメッセージ送信
セッションリストのインターフェースは通常、各セッションの最新メッセージのプレビューと送信時刻を表示する必要があります。このとき、`V2TIMConversation`の`lastMessage`をデータソースとして使用できます。ただし、一部のシナリオでは、一部のメッセージ（システムプロンプトなど）をセッションの最新メッセージとして表示することを所望しない場合は、`sendMessage`のときに`isExcludedFromLastMessage`を`false`/`no`に設定できます。

メッセージ送信の詳細については、[メッセージの送信](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)をご参照ください。


>? `isExcludedFromLastMessage`は、Flutter SDK 4.0.0 以降のバージョンでのみサポートされています。
