- - - グループ内の特定メンバーまたはメンバー全員をミュートにし、かつミュート期間を設定することができます。ミュート中に利用を禁止されたメンバーは現在のグループ内でメッセージを送信できません。この操作は現在のグループのみで有効です。ミュート中において、ミュートされたメンバーがグループを退出し、再度このグループに参加した場合もミュート期間が終了するか、またはミュートが解除されるまで、ミュートは有効です。
      ここでは、主にWebとミニプログラムSDKでのグループメンバーに対するミュート/ミュートの解除方法について説明します。
  
      ## 使用制限
  
      - グループタイプの制限
       <table>
      <tr>
      <th width="25%">ワークグループ（Workまたは旧バージョンのPrivate）</th>
      <th width="25%">パブリックグループ（Public）</th>
      <th width="25%">ミーティンググループ（Meetingまたは旧バージョンのChatRoom）</th>
      <th width="25%">ライブストリーミンググループ（AvChatRoom）</th>
      </tr>
      <tr>
      <td><strong>サポートなし</strong></td>
      <td>サポートしています</td>
      <td>サポートしています</td>
      <td>サポートしています</td>
      </tr>
      </table>
  
      - メンバーロールの制限
      <table>
      <tr>
      <th width="25%">メンバーロール</th>
      <th>権限</th>
      </tr>
      <tr>
      <td>App管理者</td>
      <td>現在のSDKAppIDの全グループの全メンバーに対するミュート/ミュート解除操作の実行をサポート</td>
      </tr>
      <tr>
      <td>グループマスター</td>
      <td>現在のグループ内の管理者と一般メンバーに対するミュート/ミュート解除操作の実施をサポート</td>
      </tr>
      <tr>
      <td>グループ管理者</td>
      <td>現在のグループ内の一般メンバーに対するミュート/ミュート解除操作の実施をサポート</td>
      </tr>
      <tr>
      <td>一般メンバー</td>
      <td>ミュート権限なし</td>
      </tr>
      </table>
  
      ## 操作手順
  
      ### 手順1：操作権限の確認
      1.  [getGroupProfile](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getGroupProfile) インターフェースを呼び出して、所属するグループタイプをクエリーし、ミュート/ミュート解除操作がサポートされているかどうか確認します。
       >!グループタイプがPrivateまたはWork（ワークグループ）である場合は、ミュートをサポートしていません。
       >
       >2.  [getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getGroupMemberProfile) インターフェースを呼び出して、指定されたuserIDの現在のグループでのメンバーロールをクエリーし、ミュート/ミュート解除操作を実行する権限があるかどうかを確認します。
  
      ### 手順2：グループメンバーのミュート/ミュート解除
      #### 単一ユーザーのミュート/ミュート解除
      App管理者、グループマスターまたはグループ管理者は [setGroupMemberMuteTime](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#setGroupMemberMuteTime) インターフェースを呼び出し、指定グループ内の指定メンバーに対してミュート/ミュート解除を実行できます。1回の呼び出しは単一のメンバーのみに対するミュート/ミュート解除をサポートします。
      リクエストパラメータは下表のとおりです。
  
      | 名称     | タイプ | 説明                                                         |
      | -------- | ------ | ------------------------------------------------------------ |
      | groupID  | String | グループID                                                   |
      | userID   | String | グループメンバーID                                           |
      | muteTime | Number | ミュート時間。単位は秒。0に設定の場合はミュートの解除を意味します |
  
      リクエスト例は次のとおりです：
      ```javascript
      let promise = tim.setGroupMemberMuteTime({
        groupID: 'group1',
        userID: 'user1',
        muteTime: 1000
      });
      ```
  
      #### 全メンバーのミュート/ミュート解除
      >!この機能を使用するには、 SDKを2.6.2以上にアップグレードする必要があります。全メンバーをミュートにするか、または全メンバーのミュートを解除する場合は、現状、関連のグループにプロンプトメッセージは送信されません。
  
      App管理者またはグループマスターは、 [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#updateGroupProfile) インターフェースを呼び出し、指定グループのすべての管理者と一般メンバーに対するミュート/ミュート解除を実行できます。
      リクエストパラメータは下表のとおりです。
  
      | 名称           | タイプ  | 説明                                                         |
      | -------------- | ------- | ------------------------------------------------------------ |
      | groupID        | String  | グループID                                                   |
      | muteAllMembers | Boolean | ミュートの設定。trueは全体のミュートを意味し、falseは全体のミュート解除を意味します |
  
      リクエスト例は次のとおりです：
      ```javascript
      let promise = tim.updateGroupProfile({
        groupID: 'group1',
        muteAllMembers：true, // true 全体のミュート。false 全体のミュート解除
      });
      promise.then(function(imResponse) {
        console.log(imResponse.data.group) // 変更後のグループの詳細データ
      }).catch(function(imError) {
        console.warn('updateGroupProfile error:', imError); // グループ情報変更失敗の関連情報
      });
      ```
  
      
  
      ### 手順3：TIM.EVENT.MESSAGE_RECEIVEDイベントの監視と処理
      ミュート後、グループメンバーはミュートされたことを示す[グループプロンプトメッセージ](https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html#.GroupTipPayload) を受信します。event.dataをトラバースして、関連データを取得し、それをページにレンダリングできます。
      >?ミュート/ミュート解除の関連通知を受信後、入力ボックスまたは入力領域のステータスの有効化/無効化をご自身で実装することを推奨します。
  
      <pre>
      tim.on(TIM.EVENT.MESSAGE_RECEIVED, function(event) {
        // プッシュされたシングルチャット、グループチャット、グループプロンプト、グループシステム通知の新しいメッセージを受信します。event.dataをトラバースしてメッセージリストデータを取得し、ページにレンダリングできます。
        // event.name - TIM.EVENT.MESSAGE_RECEIVED
        // event.data - Message オブジェクトを保存する配列 - [Message]
        const length = event.data.length;
        let message;
        for (let i = 0; i < length; i++) {
          message = event.data[i];
          switch (message.type) {
            // ユーザーAをミュートにすると、ユーザーAはミュートされたことを示すグループプロンプトメッセージを受信します
            case TIM.TYPES.MSG_GRP_TIP:
              this._handleGroupTip(message);
              break;
            case TIM.TYPES.MSG_TEXT: // テキストメッセージ。さらに詳細なメッセージタイプについては、 <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html">Message</a>をご参照ください。
              break;
            default:
              break;
          }
        }
      });
  
      _handleGroupTip(message) {
        switch (message.payload.operationType) {
          case TIM.TYPES.GRP_TIP_MBR_PROFILE_UPDATED: // グループメンバープロファイルの変更、例：グループメンバーのミュート
            const memberList = message.payload.memberList;
            for (let member of memberList) {
              console.log(`${member.userID} ミュート${member.muteTime}秒`);
            }
            break;
          case TIM.TYPES.GRP_TIP_MBR_JOIN: // グループに参加したメンバー
            break;
          case TIM.TYPES.GRP_TIP_MBR_QUIT: // グループを退出したグループメンバー
            break;
          case TIM.TYPES.GRP_TIP_MBR_KICKED_OUT: // グループからキックアウトされたグループメンバー
            break;
          case TIM.TYPES.GRP_TIP_GRP_PROFILE_UPDATED: // グループプロファイルの変更
            break;
      	default:
      	  break;
        }
      }
      </pre>
  
      ### 手順4：ミュート状態の判断
  
      - 2.6.2以上のSDKでは、 [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getGroupMemberList) インターフェースを呼び出し、グループメンバーのミュート期限のタイムスタンプ（muteUntil）をプルできます。この数値をもとにグループメンバーのミュート状況、およびミュートの残り時間を判断できます。ミュート解除後、このグループメンバーの次の計算式が有効になります： GroupMember.muteUntil * 1000 <= Date.now()。
      ```javascript
      // v2.6.2 以降、getGroupMemberList インターフェースを使用して、グループメンバーミュート期限のタイムスタンプをプルできます。
      let promise = tim.getGroupMemberList({ groupID: 'group1', count: 30, offset:0 }); // 0から30のグループメンバーのプルを開始します
      promise.then(function(imResponse) {
        console.log(imResponse.data.memberList); // グループメンバーリスト
        for (let groupMember of imResponse.data.memberList) {
          if (groupMember.muteUntil * 1000  > Date.now()) {
            console.log(`${groupMember.userID} ミュート中`);
          } else {
            console.log(`${groupMember.userID} ミュートにされていません`);
          }
        }
      }).catch(function(imError) {
        console.warn('getGroupMemberProfile error:', imError);
      });
      ```
      - 2.6.2以下のSDKでは、 [getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getGroupMemberProfile) インターフェースを呼び出し、グループメンバーのミュート期限のタイムスタンプ（muteUntil）などの詳細情報をクエリーできます。
