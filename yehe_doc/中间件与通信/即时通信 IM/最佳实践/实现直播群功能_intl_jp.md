IMライブストリーミンググループ（AVChatRoom）には、次の特徴があります：
- **人数制限なし、数千万人のインタラクティブライブストリーミングのシナリオを実現**。
- 全オンラインユーザーへのプッシュメッセージ（グループシステム通知）をサポート。
- WebとWeChatミニプログラムは、ゲストID（非ログイン状態）でのメッセージの受信をサポート
- グループへの参加申請後、管理者の承認を受けずに、直接参加が可能。

>?ここでは、WebとWeChatミニプログラムSDKを例に説明します。他のSDKでも実装プロセスは同じですが、操作が若干異なります。

## 適用ケース

#### ライブストリーミング弾幕
 AVChatRoomは、弾幕、ギフト、いいね！など複数のメッセージタイプをサポートし、優れたライブストリーミングチャットのインタラクティブな体験を手軽に構築できます。弾幕コンテンツのレビュー機能を提供し、ライブストリーミングが不適切な情報による妨害を受けないことを保証します。
#### インフルエンサーマーケティング
 AVChatRoom とビジネスライブブロードキャストを組み合わせて、いいね！、問い合わせ、クーポンなど特定のメッセージタイプを適用することにより、トラフィックの収益化を支援します。

#### ティーチングホワイトボード
 AVChatRoomは、オンライン教室、テキストメッセージ、手書き入力などの機能を提供し、教師と学生のコミュニケーション、手書き入力の保存、大教室から小教室まで各種授業の教学シナリオを手軽に実現します。

## 使用制限
- [メッセージの取り消し](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#revokeMessage)はサポートしていません。
- グループマスターはグループを退出できません。グループマスターのグループ退出手段は、グループの解散のみです。
- グループメンバーの削除はサポートしていません。


## 関連ドキュメント
- [グループ管理](https://intl.cloud.tencent.com/document/product/1047/33530)
- [グループシステム](https://intl.cloud.tencent.com/document/product/1047/33529)
- [SDKダウンロード](https://intl.cloud.tencent.com/document/product/1047/33996)
- [ログの更新（Web & ミニプログラム）](https://intl.cloud.tencent.com/document/product/1047/34281)
- [SDKマニュアル](https://web.sdk.qcloud.com/im/doc/zh-cn/TIM.html)
- [SDK（Web & ミニプログラム）の統合](https://intl.cloud.tencent.com/document/product/1047/34309)
- [初期化とログイン（Web & ミニプログラム）](https://intl.cloud.tencent.com/document/product/1047/34314)
- [メッセージの送受信（Web & ミニプログラム）](https://intl.cloud.tencent.com/document/product/1047/34322)
- [グループ管理（Web & ミニプログラム）](https://intl.cloud.tencent.com/document/product/1047/34330)

## 使用ガイドライン
<span id="Step1"></span>
### 手順1：アプリケーションの作成

1. [IMコンソール](https://console.cloud.tencent.com/im)にログインします。
 >?アプリケーションをすでに保有している場合は、そのSDKAppIDを記録してから [手順2](#Step2)を実行してください。
 >同じTencent Cloudのアカウントで、最大300個のIMアプリケーションを作成することができます。すでにアプリケーションが300個ある場合は、使用する必要のないアプリケーションを[使用停止して削除](https://intl.cloud.tencent.com/document/product/1047/34540)すると、新しいアプリケーションを作成することができます。**アプリケーションを削除した後、そのSDKAppIDに対応するすべてのデータとサービスは失われます。慎重に操作を行ってください。**
 >
2. **+新しいアプリケーションの追加**をクリックします。
3. **アプリケーションの作成**ダイアログボックスにアプリケーション名を入力し**OK**をクリックします。作成が完了すると、コンソールの概要ページで、作成したアプリケーションのステータス、サービスバージョン、SDKAppID、作成時間、有効期限を確認できます。
4. このアプリケーションのSDKAppID情報を記録します。

<span id="Step2"></span>
### 手順2：AVChatRoomの作成
コンソールを介して、または[グループ作成API](https://intl.cloud.tencent.com/document/product/1047/34895) を呼び出して、グループを作成することができます。ここではコンソールを介した作成を例示します。


1. [IMコンソール](https://console.cloud.tencent.com/im)にログインし、ターゲットのアプリケーションカードをクリックします。
2. 左側のナビゲーションバーで**グループ管理**を選択し、**グループの追加**をクリックします。
3. グループ名を入力し、グループマスターIDを選択して入力し、**グループタイプ**に**AVChatRoom**を選択します。
4. **OK**をクリックし、グループが正常に作成されたら、その**グループID**（このドキュメントでは `@TGS#aC72FIKG3` を例とします）を記録します。


<span id="Step3"></span>
### 手順3：SDKの統合 
NPMまたはScriptを介してSDKを統合することができますが、NPMを使用して統合することを推奨します。このドキュメントではNPMを使用した 統合を例示します。

-  Webプロジェクト
```javascript
// Webプロジェクト
npm install tim-js-sdk --save-dev
```
-  ミニプログラムプロジェクト
```javascript
// WeChat Mini Programプロジェクト
npm install tim-wx-sdk --save-dev
```

>?依存の同期に問題が発生した場合は、npmソースを切り替えて再試行してください。
```
// cnpmソースの切り替え
npm config set registry http://r.cnpmjs.org/
```

<span id="Step4"></span>
### 手順4： SDKインスタンスの作成

<pre><code><span class="hljs-comment">// SDK インスタンスを作成します。TIM.create() メソッドは、同じSDKAppIDに対して同じインスタンスのみを返します</span>
<span class="hljs-keyword">let</span> options = {
  SDKAppID: <span class="hljs-number">0</span> <span class="hljs-comment">// アクセス時に0をIMアプリケーションのSDKAppIDに置き換える必要があります</span>
}
<span class="hljs-keyword">let</span> tim = TIM.create(options) <span class="hljs-comment">// SDK インスタンスは通常timで表示されます</span>
<span class="hljs-comment">// SDKログ出力レベルを設定します。詳細なレベル分けについては <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html?_ga=1.43970405.1562552652.1542703643#setLogLevel">setLogLevel インターフェースの説明</a>をご参照ください</span>
tim.setLogLevel(<span class="hljs-number">0</span>) <span class="hljs-comment">// 通常レベル。アクセス時にログ量が多くなるので、このレベルを使用することを推奨します</span>

tim.<span class="hljs-keyword">on</span>(TIM.EVENT.SDK_READY, function (<span class="hljs-keyword">event</span>) {
  <span class="hljs-comment">// SDK readyにならなければ、アクセス側はsendMessageなどの認証が必要なインターフェースを呼び出すことができず、失敗します！</span>
  <span class="hljs-comment">// event.name - TIM.EVENT.SDK_READY</span>
})

tim.<span class="hljs-keyword">on</span>(TIM.EVENT.MESSAGE_RECEIVED, function(<span class="hljs-keyword">event</span>) {
  <span class="hljs-comment">// プッシュされたシングルチャット、グループチャット、グループプロンプト、グループシステム通知の新規メッセージを受信します。event.dataをトラバースしてメッセージリストデータを取得し、ページにレンダリングできます</span>
  <span class="hljs-comment">// event.name - TIM.EVENT.MESSAGE_RECEIVED</span>
  <span class="hljs-comment">// event.data - Messageオブジェクトをストレージする配列 - [Message]</span>
  <span class="hljs-keyword">const</span> length = <span class="hljs-keyword">event</span>.data.<span class="hljs-function">length
  <span class="hljs-keyword">let</span> message
  <span class="hljs-title">for</span> (<span class="hljs-params"><span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; length; i++</span>)</span> {
    <span class="hljs-comment">// Messageインスタンスの詳細なデータ構造については、 <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html">Message</a>をご参照ください</span>
    <span class="hljs-comment">// 特に、typeとpayloadの属性に重点的な注意を払う必要があります</span>
    <span class="hljs-comment">// v2.6.0以上は、AVChatRoomのグループチャットメッセージ、グループへの参加やグループからの退出等のグループプロンプトメッセージに、nick（ニックネーム）とavatar（プロフィール画像URL）属性が追加され、アクセス側のより良い表示体験に貢献しています</span>
    <span class="hljs-comment">// まずupdateMyProfileを呼び出し、自身のnick（ニックネーム）と avatar（プロフィール画像URL）を設定します。<a href="https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#updateMyProfile">updateMyProfileインターフェースの説明</a>をご参照ください</span>
    message = <span class="hljs-keyword">event</span>.data[i]
    <span class="hljs-keyword">switch</span> (message.type) {
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_TEXT:
        <span class="hljs-comment">// テキストメッセージを受信</span>
        <span class="hljs-keyword">this</span>._handleTextMsg(message)
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_CUSTOM:
        <span class="hljs-comment">// カスタムメッセージを受信</span>
        <span class="hljs-keyword">this</span>._handleCustomMsg(message)
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_GRP_TIP:
        <span class="hljs-comment">// メンバーのグループへの参加、メンバーのグループからの退出など、グループプロンプトメッセージが受信されます</span>
        <span class="hljs-keyword">this</span>._handleGroupTip(message) 
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_GRP_SYS_NOTICE:
        <span class="hljs-comment">// グループシステム通知を受信します。REST APIを使用して送信されるグループシステム通知については、 <a href="https://intl.cloud.tencent.com/document/product/1047/34958">グループでのシステム通知の送信API</a>をご参照ください</span>
        <span class="hljs-keyword">this</span>._handleGroupSystemNotice(message)
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">default</span>:
         <span class="hljs-keyword">break</span>
    }
  }
})

_handleTextMsg(message) {
  <span class="hljs-comment">// 詳細なデータ構造については、 <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html#.TextPayload">TextPayloadインターフェースの説明</a>をご参照ください</span>
  console.log(message.payload.text) <span class="hljs-comment">// テキストメッセージの内容</span>
}

_handleCustomMsg(message) {
  <span class="hljs-comment">// 詳細なデータ構造については、<a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html#.CustomPayload">CustomPayloadインターフェースの説明</a>をご参照ください</span>
  console.log(message.payload)
}

_handleGroupTip(message) {
  <span class="hljs-comment">// 詳細なデータ構造については、 <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html#.GroupTipPayload">GroupTipPayloadインターフェースの説明</a>をご参照ください</span>
  <span class="hljs-keyword">switch</span> (message.payload.operationType) {
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_JOIN: <span class="hljs-comment">// メンバーのグループへの参加</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_QUIT: <span class="hljs-comment">// メンバーのグループからの退出</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_KICKED_OUT: <span class="hljs-comment">// メンバーのグループからのキックアウト</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_SET_ADMIN: <span class="hljs-comment">// メンバーを管理者に設定</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_CANCELED_ADMIN: <span class="hljs-comment">// メンバーの管理者のロールの取り消し</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_GRP_PROFILE_UPDATED: <span class="hljs-comment">// グループプロファイルの変更</span>
      <span class="hljs-comment">//v2.6.0以降は、グループがカスタマイズしたフィールドを変更できます</span>
      <span class="hljs-comment">// message.payload.newGroupProfile.groupCustomField </span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_PROFILE_UPDATED: <span class="hljs-comment">// グループメンバープロファイルの変更。例：グループメンバーに対するミュート</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">default</span>:
      <span class="hljs-keyword">break</span>
  }
}

_handleGroupSystemNotice(message) {
  <span class="hljs-comment">// 詳細なデータ構造については、 <a href="https://web.sdk.qcloud.com/im/doc/zh-cn/Message.html#.GroupSystemNoticePayload">GroupSystemNoticePayloadインターフェースの説明</a>をご参照ください</span>
  console.log(message.payload.userDefinedField) <span class="hljs-comment">// ユーザーカスタムフィールド。RESTAPIを使用してグループシステム通知を送信する場合は、この属性値内でカスタム通知のコンテンツを入手できます。</span>
  <span class="hljs-comment">// REST APIを使用してグループシステム通知を送信する場合は、 <a href="https://intl.cloud.tencent.com/document/product/1047/34958">グループ内システム通知送信API</a>をご参照ください</span>
}</code></pre>

<span id="Step5"></span>
### 手順5：SDKにログイン 

```javascript
let promise = tim.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(function(imResponse) {
  console.log(imResponse.data); // ログイン成功
}).catch(function(imError) {
  console.warn('login error:', imError); // ログイン失敗の関連情報
});
```

<span id="Step6"></span>
### 手順6：自身のニックネームとプロフィール画像の設定
2.6.2以上の SDKには、AVChatRoom内のグループチャットメッセージとグループプロンプトメッセージ（グループへの参加やグループからの退出など）に、nick（ニックネーム）とavatar（プロフィール画像URL）属性が追加されています。インターフェース [updateMyProfile](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#updateMyProfile) を呼び出して、自身のnick（ニックネーム）とavatar（プロフィール画像URL）を設定できます。

```javascript
// v2.6.0以降、AVChatRoom内のグループチャットメッセージ、グループへの参加やグループからの退出などのグループプロンプトメッセージに、nick（ニックネーム） とavatar（プロフィール画像URL）属性が追加されており、アクセス側のより良い表示体験に貢献しています。まずupdateMyProfileを呼び出し、個人プロファイルを設定する必要があります。
// 個人の基本プロファイルの修正
let promise = tim.updateMyProfile({
  nick: '自身のニックネーム',
  avatar: 'http(s)://url/to/image.jpg'
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // プロファイルの更新に成功
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // プロファイル更新失敗の関連情報
});
```

<span id="Step7"></span>
### 手順7：グループへの参加
```javascript
// 匿名ユーザーの参加（ログインする必要はなく、グループに参加した後にのみメッセージを受信できます）
let promise = tim.joinGroup({ groupID: 'avchatroom_groupID'});
promise.then(function(imResponse) {
  switch (imResponse.data.status) {
    case TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: // 管理者の同意を待機
      break
    case TIM.TYPES.JOIN_STATUS_SUCCESS: // グループへの参加に成功
      console.log(imResponse.data.group) // 参加するグループのプロファイル
      break
    case TIM.TYPES.JOIN_STATUS_ALREADY_IN_GROUP: // グループに参加済み
      break
    default:
      break
  }
}).catch(function(imError){
  console.warn('joinGroup error:', imError) // グループ参加申請失敗の関連情報
});
```

### 手順8：メッセージインスタンスの作成と送信
ここでは、テキストメッセージの送信を例示します。

<pre><code class="language-javascript"><span class="hljs-comment">// テキストメッセージの送信は、Webとミニプログラムで同じです</span>
<span class="hljs-comment">// 1. メッセージインスタンスを作成します、インターフェースから返されたインスタンスを画面に表示できます</span>
<span class="hljs-keyword">let</span> message = tim.createTextMessage({
  <span class="hljs-attr">to</span>: <span class="hljs-string">'avchatroom_groupID'</span>,
  <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_GROUP,
  <span class="hljs-comment">// メッセージの優先度は、グループチャットに使用されます（v2.4.2以降でサポート）。グループのメッセージが頻度制限を超過した場合、バックエンドでは最初に優先度の高いメッセージが配信されます。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/1047/33526">メッセージ優先度と頻度制御</a>をご参照ください</span>
  <span class="hljs-comment">// サポートされる列挙値：TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL（デフォルト）, TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST</span>
  <span class="hljs-attr">priority</span>: TIM.TYPES.MSG_PRIORITY_NORMAL,
  <span class="hljs-attr">payload</span>: {
    <span class="hljs-attr">text</span>: <span class="hljs-string">'Hello world!'</span>
  }
})
<span class="hljs-comment">// 2. メッセージの送信</span>
<span class="hljs-keyword">let</span> promise = tim.sendMessage(message)
promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
  <span class="hljs-comment">// 送信成功</span>
  <span class="hljs-built_in">console</span>.log(imResponse)
}).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
  <span class="hljs-comment">// 送信失敗</span>
  <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError)
})</code></pre>


## よくあるご質問

### 1. 自身が送信するメッセージ `Message.nick` と `Message.avatar` がいずれも空である場合、どのように処理すれば、インターフェースでニックネームとプロフィール画像を正常に表示できますか？

[getMyProfile](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#getMyProfile) を呼び出すことによって自身のニックネームとプロフィール画像を取得できます。

### 2. ライブストリーミンググループでミュート機能を実現するにはどうすればよいですか？

ミュート機能はカスタムメッセージを介して実現でき、カスタムメッセージにはミュートするメンバーのMembers_Accountとミュート時間を含める必要があります。[グループ内での発言前のコールバック](https://intl.cloud.tencent.com/document/product/1047/34374) を介して、このカスタムメッセージをビジネスバックエンドにCC送信すると、ビジネスバックエンドが [一括ミュートとミュート解除](https://intl.cloud.tencent.com/document/product/1047/34951) インターフェースを呼び出し、指定ユーザーに対するミュート機能を実現できます。

### 3. ライブストリーミンググループでキックアウト機能を実現するにはどうすればよいですか？

キックアウト機能はカスタムメッセージを介して実現でき、カスタムメッセージにはキックアウト対象メンバーのMembers_Accountを含める必要があります。このメッセージの優先度をHighに設定することで、40通/秒メッセージ頻度制限によりこのメッセージがバックエンドによって廃棄されることを防止し、追放対象メンバーのSDKがこのメッセージを受信した後、[グループからの退出](https://intl.cloud.tencent.com/document/product/1047/36169) インターフェースを呼び出し、ライブストリーミンググループで追放機能を実現できます。
<span id="p4"></span>
### 4. ミニプログラム、Webでグループ退出インターフェースを呼び出した後、Android、iOS、PCでも同期的にグループ退出となるのに、Android、iOS、PC でグループ退出インターフェースを呼び出した後、ミニプログラム、Webで、退出にならないのはなぜですか？

ミニプログラムやWebはユーザーのゲストモードアクセスをサポートしているため、Android、iOS、PCでグループから退出した後も、ミニプログラム、Webではグループ退出操作が自動的にトリガーされません。

- 全端末で同期的な退出操作を実現したい場合は、 [グループメンバーが退出した後](https://intl.cloud.tencent.com/document/product/1047/34373) のコールバックを設定し、OptPlatform フィールドに基づいて現在の退出プラットフォームを決定します。グループ退出プラットフォームがAndroid、iOS、PCである場合は、[シングルチャットメッセージ](https://intl.cloud.tencent.com/document/product/1047/34919) インターフェースを介してシステムメッセージの方式でカスタムメッセージをグループ退出者に送信すると、フロントエンドはこのセッションをブロックし、UIに表示しません。ミニプログラムまたはWebで、このメッセージを受信した後、 [グループ退出](https://intl.cloud.tencent.com/document/product/1047/33999) インターフェースを呼び出すことができます。
- 単一の端末で個別に退出操作を実現したい場合は、 [グループメンバーが退出した後](https://intl.cloud.tencent.com/document/product/1047/34373)のコールバックを設定し、OptPlatformフィールドに基づいて退出プラットフォームを決定します。 [シングルチャットメッセージ](https://intl.cloud.tencent.com/document/product/1047/34919) インターフェースを介してシステムメッセージの方式でカスタムメッセージをグループ退出者に送信すると、フロントエンドはこのセッションをブロックし、UIに表示しません。退出しない端末でこのメッセージを受信した後、 [グループ参加](https://intl.cloud.tencent.com/document/product/1047/36169) インターフェースを呼び出し、このグループに参加します。グループ参加および退出のシステム通知が複数回出現する事態を回避するため、チケットを送信してグループ参加および退出のシステム通知を閉じることができます。

### 5. メッセージが紛失するのはなぜですか？

メッセージ紛失の原因として次の原因が考えられます。

- ライブストリーミンググループは、40通/秒の頻度制限があります。メッセージ送信前のコールバックとメッセージ送信後のコールバックを介して判断できます。紛失したメッセージが、メッセージ送信前にコールバックを受信し、メッセージ送信後にコールバックを受信していない場合、このメッセージは制限を受けています。
- [よくあるご質問4](#p4)を参考に、ミニプログラム、Webから退出したことによって、Android、iOS、PCで同期的な退出が生じているかどうかを判断することができます。
- ミニプログラム、Webに問題が発生した場合は、使用するSDKがV2.7.6より以前のバージョンかどうかを確認してください。V2.7.6より以前の場合は、最新版にアップグレードしてください。

上記の可能性をすでに排除している場合は、チケットを送信して弊社にご連絡ください。

### 6. いいね！/フォロー数の集計を実現するにはどうすればよいですか？

まずカスタムメッセージを介して、いいね！/フォローのメッセージタイプを構築し、ユーザーがフロントエンドでいいね！/フォローのアイコンをクリックしてカスタムメッセージを配信する場合、[グループ内での発言前のコールバック](https://intl.cloud.tencent.com/document/product/1047/34374) を呼び出して、いいね！/フォローメッセージをビジネス側にCC送信します。ビジネス側は受信したいいね！/フォローメッセージ数に基づき数量の集計を行い、3秒～5秒ごとに [グループ基本プロファイル修正インターフェース](https://intl.cloud.tencent.com/document/product/1047/34962)を介してこのデータをグループプロファイルフィールドで更新し、SDKは [グループプロファイル取得インターフェース](https://intl.cloud.tencent.com/document/product/1047/36169) を介していいね！/フォロー数を集計します。

### 7. メッセージ優先度をより合理的に設定するにはどうすればよいですか？

重要メッセージが廃棄されることを回避するため、ライブルームはすべてのメッセージに対し、3つの優先度の選択を提供しており、SDKはメッセージ取得時に優先度の高いメッセージを優先的に取得します。カスタムメッセージの優先度の設定は、次のとおりです。

- High： Red packet（紅包）、ギフト、キックアウトメッセージ。
- Normal：一般的なテキストメッセージ。
- Low：いいね！、フォローメッセージ。

### 8.ビデオとチャットを直接使用できるオープンソースのライブストリーミングコンポーネントはありますか？

はい、コードはオープンソースです。詳細については、 [Tencent Cloud TWebLIVBコンポーネント](https://github.com/tencentyun/TWebLive)をご参照ください。



