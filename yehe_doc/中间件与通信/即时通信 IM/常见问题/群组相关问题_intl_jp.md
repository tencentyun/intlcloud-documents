### グループチャットでグループメンバーの発言禁止を設定または解除するにはどうすればよいですか？
発言禁止（ミュート）は、グループメンバーのメッセージ送信を制御する方法の1つです。発言が禁止されたメンバーは、ミュートされている間に当該グループ内でメッセージを送信できません。設定ドキュメントの詳細については、次のSDKドキュメントをご参照ください。
- [グループメンバーの発言禁止(Android)](https://intl.cloud.tencent.com/document/product/1047/48466)
- [グループメンバーの発言禁止(iOS)](https://intl.cloud.tencent.com/document/product/1047/48181)
- [グループメンバーの発言禁止(Web)](https://intl.cloud.tencent.com/document/product/1047/48180)


また、App管理者は、REST APIで任意のグループの任意のメンバーに対して発言禁止を設定することもできます。詳細については、[REST API：一括発言禁止と発言禁止の解除](https://intl.cloud.tencent.com/document/product/1047/34951)をご参照ください。


###　発言が禁止されているメンバーと発言禁止時間を確認するにはどうすればよいですか？
管理者とグループ所有者は、IM SDKが提供するインターフェースでメンバーに対して発言禁止を設定または解除できます（発言禁止を解除するには、発言禁止時間を0に設定すればよいです）。
メンバーの発言禁止情報は、グループメンバープロフィールから確認できます。設定ドキュメントの詳細については、次のSDKドキュメントをご参照ください：
- [グループメンバープロフィールの取得(Android)](https://intl.cloud.tencent.com/document/product/1047/48178)
- [グループメンバープロフィールの取得(iOS)](https://intl.cloud.tencent.com/document/product/1047/48178)
- [グループメンバーリストの取得(Web)](https://intl.cloud.tencent.com/document/product/1047/48180)

また、App管理者は、REST APIでグループの発言禁止情報を確認することもできます。詳細については、[REST API：グループの発言禁止ユーザーリストの取得](https://intl.cloud.tencent.com/document/product/1047/34964)をご参照ください。

### グループ参加前のローミングメッセージを表示するにはどうすればよいですか？

グループ参加前のローミングメッセージを表示できる前提は、当該グループタイプの履歴メッセージがクラウドストレージをサポートしていることです。グループタイプと設定の運用シナリオによって、次のように設定しました。
- **ライブ配信グルー(AVChatRoom)**および**古いバージョンの**オンラインメンバーブロードキャストグループ(BChatRoom)**は、履歴メッセージの保存をサポートしていないため、これら2つのグループは、グループ参加前のローミングメッセージの表示をサポートできません。
- 非ライブ配信グループである**フレンズワークグループ(Work)**および**知らない人とのソーシャルグループ(Public)**は、デフォルトでグループ参加前のローミングメッセージを表示することをサポートしません。**臨時ミーティンググル(Meeting)**および**コミュニティ(Community)**の場合、グループメンバーはデフォルトでグループ参加前のローミングメッセージを表示できます。デフォルト設定を変更する必要がある場合は、[**コンソール**](https://console.cloud.tencent.com/im)>**機能設定>グループ設定>グループメッセージの設定**で変更できます。

非ライブ配信グループのメッセージ履歴は、デフォルトで7日保存されます（Ultimate版はデフォルトで30日です）。メッセージ履歴をより長い期間保存したい場合は、[コンソール](https://console.cloud.tencent.com/im)の**機能設定**で設定できます。メッセージ履歴の保存期間を延長するには、付加価値サービスの費用がかかります。具体的な課金説明については、[料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

### AVChatRoomとMeeting（古いバージョンのChatRoomのタイプ）の違いは何ですか？

これらの2つのグループは、異なる運用シナリオに適用されます。Meetingは中規模のグループ（6,000人未満）、AVChatRoomは大規模なライブブロードキャストシナリオ（メンバー数に制限はありません）に適しています。そのため、これら2つのグループには、機能設計にいくつかの違いがあります。主な違いを次の表に示します：

| グループ機能項目                  | Meeting                                | AVChatRoom            |
| ------------------------- | --------------------------------------- | --------------------- |
| グループメンバーの上限                | 6000人                                 | 制限なし               |
| グループメンバー情報                | すべてのグループメンバー情報を保存                      | グループメンバー情報を保存しない |
| グループ所有者によるグループ管理者の設定のサポート状況  | サポート                                    | 未サポート                |
| グループメンバーの削除                | グループ管理者、グループ所有者、App管理者はグループメンバーを削除可能 | 未サポート                |
| メッセージローミングのサポート状況          | サポート                                    | 未サポート                |
| グループ参加前の履歴メッセージのサポート状況    | デフォルトでは、有効期間内に保存される履歴メッセージを表示可能          | 未サポート                |
| メンバー変更通知のサポート状況      | 未サポート                                  | サポート                  |
| App管理者によるグループインポートのサポート状況 | サポート                                    | 未サポート                |

### グループ/グループメンバーディメンションのカスタムフィールド値を取得できないのはなぜですか？

この問題については、次の側面からトラブルシューティングを行うことができます。
1. コンソールからカスタムフィールドの設定が正しいかどうかを確認します。
2. クエリーリクエストの確認：リクエストユーザーが読み取り権限を持っているかどうか、グループタイプがこのカスタムフィールドをサポートしているかどうかを確認します。
3. 当該カスタムフィールドの設定リクエストが成功したかどうかを確認します。
4. グループディメンションのカスタムフィールドの場合：
   - iOS：IM SDKにログインする前に、TIMManager > setUserConfig > TIMUserConfig > TIMGroupInfoOption > groupCustomで該当する設定を実行してください。
   - Android：IM SDKにログインする前に、TIMManager > setUserConfig > TIMUserConfig >  TIMGroupSettings > groupInfoOptions > setCustomTagsで該当する設定を実行してください。
5. グループメンバーディメンションのカスタムフィールドの場合：
   - iOS：IM SDKにログインする前に、TIMManager > setUserConfig > TIMUserConfig > TIMGroupMemberInfoOption > memberCustomで該当する設定を実行する必要があります。
   - Android：IM SDKにログインする前に、TIMManager > setUserConfig > TIMUserConfig > TIMGroupSettings > memberInfoOptions > setCustomTagsで該当する設定を実行してください。
   
   
 ### ライブ配信グループのオンライン人数を取得するにはどうすればよいですか？
AVChatRoomのオンライン人数は、SDKインターフェース（[Android](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a56840105a4b3371eeab2046d8c300bce
)、[iOS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ada2eadb44f6865e9848df94fb5bae4ae)、[Web](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getGroupOnlineMemberCount)、[Flutter](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupOnlineMemberCount.html)）または[REST API](https://intl.cloud.tencent.com/document/product/1047/38521)インターフェースから取得できます。

### グループメッセージは40件/秒に制限されています。関連するヒントと説明はありません。40件/秒の制限を超えているかどうかを判断するにはどうすればよいですか？
頻度制御を超えた場合、デフォルトでは、頻度制限エラーコードは発信者に返されません。エラーコード（[10023](https://intl.cloud.tencent.com/document/product/1047/34348)）を発信者に返す必要がある場合は、[設定変更リクエスト作業依頼書](https://intl.cloud.tencent.com/document/product/1047/44322)をプラットフォームに提供してください。
