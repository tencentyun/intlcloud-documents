ライブストリーミングは生活のいたるところに存在すると言ってよく、自身のライブストリーミングプラットフォームを持つ企業や開発者はますます増えています。ライブストリーミングプラットフォーム自体が関与する、ライブストリームのプッシュ・プル、ライブストリーミングチャットルーム、ライブストリーミングルームのインタラクション（「いいね」、ギフト、マイク接続）、ライブストリーミングルームのステータス管理などに対するニーズは複雑であることが多いです。そのため、ここでは、Tencent Cloudの関連製品（[Tencent Cloud IM](https://console.cloud.tencent.com/im)、[Tencent Cloud TRTC](https://console.cloud.tencent.com/trtc)、[Tencent Cloud CSS](https://console.cloud.tencent.com/live/livestat)など）を基本として、ライブストリーミングルーム構築の過程でよくあるニーズの実現方法や、発生する可能性がある問題、注意が必要な点などについて整理します。開発者の皆さんがスピーディーに業務を理解し、ニーズを実現する上でお役に立てれば幸いです。

![](https://qcloudimg.tencent-cloud.cn/raw/91a6136c0b000f0c76b72a890f3e41ac.jpg)



## 1、準備作業

### アプリケーションの作成

Tencent Cloudを使用してライブストリーミングルームを構築するには、下図に示すように、まず[コンソール](https://console.cloud.tencent.com/im)でIMアプリケーションを作成する必要があります。
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-081650.png)

### TRTCまたはライブストリーミングアプリケーションの作成

ライブストリーミングルームの機能はIMの機能に依存するほか、ライブストリーミング機能にも依存しています。ライブストリーミング機能は[Tencent Cloud TRTC](https://console.cloud.tencent.com/trtc)または[CSS](https://console.cloud.tencent.com/live/livestat)を使用して実装できます。下図に示すように、TRTCアプリケーションはIMアプリケーションの作成後にアクティブ化できます。
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-081714.png)

[CSS](https://console.cloud.tencent.com/live/livestat)を使用したい場合も、下図のようにアクティブ化したプッシュおよび再生ドメイン名を使用することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/fb8a00c48c21bd8d8d74b5a83105893d.png)



### 関連基本設定の完了

準備作業のステップ1で作成したアプリケーションは体験版であり、開発段階での使用にのみ適しています。本番環境のユーザーはご自身の業務ニーズに合わせて、プロフェッショナル版またはフラッグシップ版をアクティブ化してください。バージョン間の違いについては[IM価格ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

ライブストリーミングのシーンでは、アプリケーションの作成以外にもいくつかの追加設定が必要です。

#### キーを使用したUserSigの計算
IMのアカウントシステムでは、ユーザーログインに必要なパスワードはユーザーのサーバーでIMが提供するキーを使用して計算されます。ユーザーはドキュメント[UserSigの計算](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。下図に示すように、開発段階では、クライアントでの開発に支障がないよう、[コンソールでのUserSigの計算](https://console.cloud.tencent.com/im/tool-usersig)を行うこともできます。
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-083650.png)

#### 管理者アカウントの設定

ライブストリーミング中に、管理者がライブストリーミングルームに対してメッセージの送信、違反ユーザーのミュート（強制退室）などを行う必要がある場合があります。この場合は[IMサーバーAPI](https://intl.cloud.tencent.com/document/product/1047/34621)を使用して必要な処理を行わなければなりません。サーバーAPIを呼び出す前に、[IM管理者アカウントの作成](https://console.cloud.tencent.com/im/account-management)を行っておく必要があります。IMはデフォルトで1つのUserIDをadministratorアカウントとして開発者にご提供しています。開発者は業務のシーンに応じて複数の管理者アカウントを作成することもできますが、IMで作成できる管理者アカウントは最大5つまでであることにご注意ください。

#### コールバックアドレスの設定およびコールバックのアクティブ化

ライブストリーミングルームで弾幕抽選、メッセージ統計、センシティブコンテンツチェックなどのニーズを実現したい場合は、IMのコールバックモジュールを使用する必要があります。これはIMバックエンドがいくつかの特定のシーンで、開発者の業務バックエンドにコールバックを行うものです。開発者は下図のように、HTTPのインターフェースを1つ提供し、[コンソール > コールバック設定](https://console.cloud.tencent.com/im/callback-setting)モジュールに設定するだけで済みます。

![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-083718.png)


### クライアントSDKの統合

準備作業がすべて完了した後、IMとTRTCのクライアントSDKをユーザーのプロジェクトに統合する必要があります。開発者はご自身の業務ニーズに応じて、様々な統合ソリューションを選択することができます。[クイックインテグレーションシリーズドキュメント](https://intl.cloud.tencent.com/document/product/1047/34547)をご参照ください。

続いて、ライブストリーミングルームによくある機能のポイントについて整理し、開発者のご参照用としてベストプラクティスソリューションを提供します。関連の実装コードも併せてご参照ください。

## 2、ライブストリーミングルームの各機能の開発ガイド

### ライブストリーミングルームのステータス

ライブストリーミングルームのステータスには一般的に次の数種類があります。
<table selecttype="cells" ><colgroup><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:2%">番号</td>
<th>ライブストリーミングルームのステータス</td>
</tr>
<tr  ><td>1</td>
<th>ライブストリーミング開始待機中</td>
</tr><tr  ><td>2</td>
<th>ライブストリーミング中</td>
</tr><tr  ><td>3</td>
<th>ライブストリーミング一時停止</td>
</tr><tr><td>4</td>
<th>ライブストリーミング終了</td>
</tr><tr  ><td>5</td>
<th>ライブストリーミングリプレイ中</td>
</tr></tbody>
</table>
ライブストリーミングルームのステータスには次のような特徴があります。
<table selecttype="cells" ><colgroup><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:2%">番号</td>
<th>特徴</td>
</tr><tr  ><td>1</td>
<td>ライブストリーミングルームのステータス変更はライブストリーミングルームのユーザーにリアルタイムで通知する必要がある</td>
</tr><tr  ><td>2</td>
<td>ライブストリーミングルームの新規入室ユーザーは現在のライブストリーミングルームのステータスを取得する必要がある</td>
</tr></tbody>
</table>
 

これらについては2つの実現方法を提供しています。この2つの方法のメリットとデメリットについて分析します。

<table selecttype="cells" ><colgroup><col  ><col  ><col  ></colgroup>
<tbody>
<tr  ><th>2種類の実現方法</td>
<th>メリット</td>
<th>デメリット</td>
</tr><tr  ><td>業務バックエンドでライブストリーミングルームのステータスを保守し、IMサーバーAPIを使用して<a href="https://intl.cloud.tencent.com/document/product/1047/34959">グループカスタムメッセージ</a> を送信してグループ内のユーザーに通知します。</td>
<td>ライブストリーミングルームのステータスを何度も頻繁に取得する必要がある場合は、ライブストリーミングルームのステータスをIMのグループプロファイルに保存する場合に比べて、業務バックエンドに保存することでIM SDKの呼び出し頻度を低下させることができます。<br>IM SDKを統合していない場所に、取得したライブストリーミングルームのステータスを提供できる可能性があります。</td>
<td>業務バックエンドがライブストリーミングルームステータス読み取り/書き込みモジュールを追加で提供する必要があります。<br>ライブストリーミングルームデータは業務バックエンドとIMのグループプロファイルの両方から取得するため、ライブストリーミングルームデータのエラー確率が上昇します。<br>送信したカスタムメッセージが消失する可能性があります。メッセージ量が特に多い場合、優先度の低いメッセージが破棄され、それによってライブストリーミングルームステータスの表示に影響することがあります。このため、ここでは高優先度のカスタムメッセージを使用することをお勧めします。</td>
</tr><tr  ><td>グループカスタムフィールドまたはグループ属性によってライブストリーミングルームのステータスを保存し、クライアントSDKの<a href="https://cloud.tencent.com/document/product/269/75406">グループ属性変更コールバック</a>によってグループ内のユーザーに通知します。</td>
<td>開発者は追加のライブストリーミングルームステータス読み取り/書き込みモジュールを提供する必要がありません。<br>グループ属性変更コールバックは理論上は消失の可能性がありません。<br>ライブストリーミングルームデータはグループプロファイルから取得し、データソースが1つのため、エラーが少なくなります。</td>
<td>公開性の高いモジュールではグループプロファイルを頻繁に取得する必要があり、IMの負荷が増大します。<br>IM SDKモジュールを統合していない場合は、業務バックエンドでIMサーバーSDKを呼び出してグループプロファイルを取得する必要があり、呼び出し頻度にも制限があります。</td>
</tr></tbody>
</table>


上記の分析の結果、方法1と方法2を組み合わせて使用し、ライブストリーミングルームのステータスを保守することをお勧めします。

1. ライブストリーミングルーム内では、方法1によってライブストリーミングルームのステータスを取得する
2. ライブストリーミングルーム外では、方法2によってライブストリーミングルームのステータスを取得する
3. 業務バックエンドはライブストリーミングルームのステータスが変更されると、速やかに[IMサーバーインターフェース](https://intl.cloud.tencent.com/document/product/1047/34621)を通じてデータをIMグループプロファイルに同期する（[グループ属性](https://intl.cloud.tencent.com/document/product/1047/34962)、[グループカスタムフィールド](https://intl.cloud.tencent.com/document/product/1047/34962)）

## グループタイプの選択

ライブストリーミングのシーンでは、ユーザーチャットエリアには次のような特徴があります。

1. ユーザーのグループへの出入りが頻繁で、なおかつこれらのグループのセッション情報（未読、lastMessageなど）を管理する必要がない
2. ユーザーは自動的にグループに参加し、監査の必要がない
3. ユーザーの発言は一時的であり、グループの過去のチャット記録をフォローしていない
4. グループの人数は一般的に比較的多い
5. グループメンバー情報を保存しなくてもよい

そのため、IMの[グループ特性](https://intl.cloud.tencent.com/document/product/1047/33529)に基づいて、ここではAVChatRoomを選択してライブストリーミングルームのグループタイプとします。

IMライブストリーミンググループ（AVChatRoom）には、次の特徴があります。
- **人数制限なし、数千万人のインタラクティブライブストリーミングのシナリオを実現**。
- 全オンラインユーザーへのプッシュメッセージ（グループシステム通知）をサポート。
- グループへの参加申請後、管理者の承認を受けずに、直接参加が可能。

>? IM Web &ミニプログラムSDKでは、同一のユーザーは同じ時間に1つのAVChatRoomにしか入れないという制限があります。IMの複数端末ログインのシーンでは、ユーザーのログイン端末1がライブストリーミングルームAでライブストリーミングを視聴している場合、[コンソール](https://console.cloud.tencent.com/im/login-message)で複数端末ログインを許可するよう設定した状態で、このユーザーのログイン端末2がライブストリーミングルームBに入って視聴した場合、その時点でライブストリーミングルームA内の端末1はグループから退出させられます。

### ライブストリーミングルームのお知らせ

ライブストリーミングルームのお知らせ（テーマ）は各ライブストリーミングルームが必ず備えるべきコンテンツであり、ユーザーはライブストリーミングルームに入室すると、そのライブストリーミングルームの基本情報を見ることができます。また、ライブストリーミングルームのお知らせは、変更後にリアルタイムでライブストリーミンググループのグループメンバーにも通知する必要があります。グループライブストリーミングのステータスと同じように、ライブストリーミングのステータスもお客様の業務バックエンドまたはIMのグループプロファイルに保存することができます。ライブストリーミングのステータスと異なる点は、ライブストリーミングルームのお知らせには次のような、開発者が注意すべきいくつかの追加事項があることです。

1. グループプロファイルのnotificationおよびintroductionフィールドに保存できる長さに制限があります。お客様は長い通知を送信できません（グループ概要は**240**文字まで、グループのお知らせは**300**文字までです）。
2. グループプロファイルのnotificationおよびintroductionフィールドは現在stringタイプのみサポートしています。ユーザーが画像とテキストの混在するお知らせを希望する場合は、json string形式で設定し、画像はアクセス可能なオンライン画像urlとすることができます。
3. Web端末でeditorツールを使用してお知らせを設定した場合、htmlタグが含まれる場合はnative端末での解析が行えない可能性があります。

ライブストリーミングルームのお知らせは[サーバーAPI](https://intl.cloud.tencent.com/document/product/1047/34620)またはクライアントSDKのグループ属性設定によって設定できます。クライアントはグループ属性を取得することで現在のグループ情報を取得し、GroupListener内のOnGroupInfoChangeを監視することで、変更されたグループ属性を取得できます。

関連サンプルコード：

<dx-tabs>
 ::: Android
```java
// クライアントがグループプロファイルを取得
V2TIMManager.getGroupManager().getGroupsInfo(groupIDList, new V2TIMValueCallback<List<V2TIMGroupInfoResult>>() {
  @Override
  public void onSuccess(List<V2TIMGroupInfoResult> v2TIMGroupInfoResults) {
      // グループプロファイルの取得に成功
  }

  @Override
  public void onError(int code, String desc) {
      // グループプロファイルの取得に失敗
  }
});
// クライアントがグループプロファイルを変更
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupID("変更したいグループID");
v2TIMGroupInfo.setFaceUrl("http://xxxx");
V2TIMManager.getGroupManager().setGroupInfo(v2TIMGroupInfo, new V2TIMCallback() {
  @Override
  public void onSuccess() {
      // グループプロファイルの変更に成功
  }

  @Override
  public void onError(int code, String desc) {
      // グループプロファイルの変更に失敗
  }
});
```

::: 

::: iOS & Mac

```swift
[[V2TIMManager sharedInstance] getGroupsInfo:@[@"groupA"] succ:^(NSArray<V2TIMGroupInfoResult *> *groupResultList) {
    // グループプロファイルの取得に成功
} fail:^(int code, NSString *desc) {
    // グループプロファイルの取得に失敗
}];
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"変更したいグループID";
info.faceURL = @"http://xxxx";
[[V2TIMManager sharedInstance] setGroupInfo:info succ:^{
    // グループプロファイルの変更に成功
} fail:^(int code, NSString *desc) {
    // グループプロファイルの変更に失敗
}];
```

:::

::: Flutter

```dart
// グループプロファイルの取得
V2TimValueCallback<List<V2TimGroupInfoResult>> groupinfos = await groupManager.getGroupsInfo(groupIDList: ['groupid1']);
// グループプロファイルの変更
groupManager.setGroupInfo(info: V2TimGroupInfo.fromJson({
    "groupAddOpt":GroupAddOptTypeEnum.V2TIM_GROUP_ADD_AUTH
    // ...その他のプロファイル
  }));
// コールバック
TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onGroupInfoChanged: ((groupID, changeInfos) {
    // グループ情報変更コールバック
  })));
```

:::

::: Web

```js
// グループプロファイルの取得
let promise = tim.getGroupProfile({ groupID: 'group1', groupCustomFieldFilter: ['key1','key2'] });
promise.then(function(imResponse) {
  console.log(imResponse.data.group);
}).catch(function(imError) {
  console.warn('getGroupProfile error:', imError); // 詳細なグループプロファイル取得失敗の関連情報
});
// グループプロファイルの変更
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  name: 'new name', // グループ名の変更
  introduction: 'this is introduction.', // グループ概要の変更
  // v2.6.0からは、グループメンバーがグループカスタムフィールド変更のグループプロンプトメッセージを受信でき、関連する内容を取得できるようになりました。詳細についてはMessage.payload.newGroupProfile.groupCustomFieldをご参照ください
  groupCustomField: [{ key: 'group_level', value: 'high'}] // グループディメンションカスタムフィールドの変更
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // 変更後のグループの詳細データ
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // グループ情報変更失敗の関連情報
});
// v2.6.2からは、全員ミュートおよびミュート解除機能が利用できます。現在はグループ全員をミュートにすると、グループプロンプトメッセージの送信がサポートされません。
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  muteAllMembers: true, // trueは全員ミュート、falseは全員ミュートの解除を表します
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // 変更後のグループの詳細データ
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // グループ情報変更失敗の関連情報
});
```

:::
</dx-tabs>

[グループプロファイル処理モジュールのその他のSDKコードの例](https://intl.cloud.tencent.com/document/product/1047/48185)

### メッセージの優先度

ライブストリーミングルームの特色の一つに、ユーザーのメッセージ量が非常に多く、各ユーザーが頻繁にメッセージの送受信を行う可能性がある、ということがあげられます。アップストリームメッセージがIMの頻度管理閾値に達すると、IMバックエンドは一部のメッセージを破棄することでシステムの安定した実行を保証します。実際、メッセージがクライアントに届く頻度が高すぎるとメッセージの可読性も低下するため、ライブストリーミンググループメッセージに対する頻度管理の必要性は非常に高いです。

グループメッセージの優先度は3段階に分かれ、バックエンドは優先度の高いメッセージを優先的に送信します。このため、ユーザーはメッセージの重要度に応じて、適切な優先度を選択しなければなりません。
3段階の優先度は高い方から順に、それぞれ次のようになります。

| 優先度 | 意味       |
| ------ | ---------- |
| High   | 高優先度   |
| Normal | 通常の優先度 |
| Low    | 低優先度   |

メッセージ破棄ポリシーは次のとおりです。

総メッセージ数頻度管理とは、1つのグループが1秒間に送信できる最大メッセージ数の制限であり、デフォルト値は40通/秒で、毎秒平均の頻度制限を採用します。メッセージ数が制限を超過すると、バックエンドは優先度が相対的に高いメッセージを優先的に送信します。優先度が同等のメッセージの順序はランダムとなります。

頻度制限の対象となったメッセージは送信されず、メッセージ履歴にも保存されませんが、送信者には成功と返されます。[グループ内での発言前のコールバック](https://intl.cloud.tencent.com/document/product/1047/34374)はトリガーされますが、[グループ内発信後コールバック](https://intl.cloud.tencent.com/document/product/1047/34375)はトリガーされません。

つまり、ライブストリーミングルームでメッセージの優先度ルールを制定することは非常に重要です。

ライブストリーミングルームのメッセージについて、Tencentがユーザーにとっての重要性に基づいて行う優先度の区分は、高い方から順に次のようになります。

1. ユーザーの投げ銭、ギフトメッセージ。このタイプのメッセージは、ライブストリーミングルームの全ユーザーが見ることをユーザーが望むものです
2. 通常のテキスト、音声、画像などのメッセージ
3. 「いいね」メッセージ

>? 通常、消費者側のユーザー自身が送信したメッセージは、優先度の高低を問わず、必ず画面に表示させる必要があります。メッセージ量が特に多い場合、ユーザーは他のユーザーのメッセージの一部を受け取らないことが可能です。

メッセージの優先度設定コードの例は次のとおりです。
<dx-tabs>
::: Android

```java
// カスタムメッセージの作成
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createCustomMessage("シングルチャットカスタムメッセージ".getBytes());
// メッセージの優先度を高優先度メッセージに設定します
v2TIMMessage.setPriority(V2TIMMessage.V2TIM_PRIORITY_HIGH)
// メッセージを送信します
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
    @Override
    public void onProgress(int progress) {
        // カスタムメッセージは進捗をコールバックしません
    }

    @Override
    public void onSuccess(V2TIMMessage message) {
        // グループチャットカスタムメッセージの送信に成功しました
    }

    @Override
    public void onError(int code, String desc) {
        // グループチャットカスタムメッセージの送信に失敗しました
    }
});
```

:::

:::  iOS&Mac

```swift
/ テキストメッセージを作成します
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"content"];
// メッセージを送信します
[V2TIMManager.sharedInstance sendMessage:message
                                receiver:@"userID"
                                 groupID:nil
                                priority:V2TIM_PRIORITY_NORMAL
                          onlineUserOnly:NO
                         offlinePushInfo:nil
                                progress:nil
                                succ:^{
    // テキストメッセージ送信に成功しました
}
                                fail:^(int code, NSString *desc) {
    // テキストメッセージ送信に失敗しました
}];
```

:::

::: Flutter

```dart
/ テキストメッセージを作成します
V2TimValueCallback<V2TimMsgCreateInfoResult> createTextAtMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(
    text: "test",
    atUserList: [],
  );
 if(createTextAtMessageRes.code == 0){
    String id =  createTextAtMessageRes.data.id;

       // テキストメッセージを送信します
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "", groupID: "groupID");
    if(sendMessageRes.code == 0){
      // 送信に成功
    }
  }
```

:::

::: Web&

```js
// テキストメッセージを送信します
// 1. メッセージインスタンスを作成します。インターフェースから返されたインスタンスを画面に表示できます
let message = tim.createTextMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // メッセージの優先度をグループチャットに適用します（v2.4.2からサポート）。あるグループのメッセージが頻度制限を超過すると、バックエンドは高優先度のメッセージを優先的に送信します。詳細については、https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6)をご参照ください
  // サポートされる列挙値：TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL（デフォルト）, TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    text: 'Hello world!'
  },
  // v2.20.0からは、C2Cメッセージの開封確認機能がサポートされました。送信したメッセージの開封確認が必要な場合は、フラッグシップ版パッケージをご購入の上、メッセージの作成時にneedReadReceiptをtrueに設定する必要があります
  needReadReceipt: true
  // メッセージのカスタムデータ（クラウドに保存され、相手側に送信されます。プログラムをアンインストールして再インストールした後でも取得できます。v2.10.2からサポート）
  // cloudCustomData: 'your cloud custom data'
});
// 2. メッセージの送信
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // 送信に成功
  console.log(imResponse);
}).catch(function(imError) {
  // 送信に失敗
  console.warn('sendMessage error:', imError);
});
```

:::
</dx-tabs>

[メッセージ優先度設定のその他のSDKバージョンコードの例](https://intl.cloud.tencent.com/document/product/1047/47994)

### ギフトと「いいね」メッセージのベストプラクティス

![](https://qcloudimg.tencent-cloud.cn/raw/5c7b5b56d78df30840ff9b0ddad00467.jpg)

#### ギフトメッセージ

1. クライアントの短時間接続リクエストが自身の業務サーバーに届き、課金ロジックに関与します。
2. 課金後、送信者は「XXXがXXX（ギフト）を贈りました」というメッセージを直接見ることができます。（送信者が自身の贈ったギフトを確認できるようにするためのものです。メッセージ量が多い場合は、破棄ポリシーがトリガーされる可能性があります）
3. 料金の決済後、サーバーのインターフェースを呼び出してカスタムメッセージ（ギフト）を送信します
4. ギフトを連続して贈るケースではメッセージの一括化が必要です
   1. ギフトの数を直接選択して贈る場合、例えば99個のギフトを選択した場合は、メッセージを1通送信し、パラメータにギフト数を99と入力します
   2. ギフトを連続送付し、いくつで止めるか決めていない場合は、20個（数は自身で調整）ごとに、または連続送付の間隔が1秒を超えた場合に1通送信することができます。このロジックの場合、例えば99個のギフトを連続送付する場合、最適化後は5通の送信で済みます

#### 「いいね」メッセージ

1. 「いいね」とギフトではやや異なり、「いいね」は課金の必要がない場合が多いため、通常は端末からの直接送信方式を用います
2. サーバー側でカウントする必要がある「いいね」メッセージについては、クライアントで流れを制限した後、クライアントで「いいね」回数を統計し、短時間内の複数の「いいね」メッセージを一括化し、メッセージを1回だけ送信すればよいようにします。業務側サーバーはメッセージ送信前コールバックから「いいね」回数を取得し、統計を行います
3. カウントの必要がない「いいね」メッセージについては、ステップ2のロジックと同様に、業務側がクライアントで「いいね」メッセージの流れを制限してから送信します。メッセージ送信前コールバックからカウントする必要はありません。

### ライブストリーミングルームユーザーの身分、レベル

ほとんどのライブストリーミングルームにはユーザーレベルの概念があります。開発者は次の数点に基づき、一定の重み付けに従ってユーザーのレベルを計算することができます。

1. ライブストリーミングルームユーザーのオンライン時間の長さ
2. ライブストリーミングルームユーザーが送信に成功した一般ライブストリーミングルームメッセージ数
3. ライブストリーミングルームユーザーの「いいね」、ギフト送付数
4. ライブストリーミングルームユーザーがライブストリーミングルームメンバーになったかどうか
5. ...

このうち、IMに関連する、オンライン時間の長さの統計、メッセージ量の統計などはすべてIMのコールバックを使用して実現します。最初の準備作業のモジュールに、コールバック設定の関連ガイドがあります。[コンソール](https://console.cloud.tencent.com/im/callback-setting)にあるコールバックの詳細は次のとおりです。
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-083830.png)

統計関連情報のフローチャートは次のとおりです。
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-091055.png)


メッセージ送信後コールバックデータの例です。

```json
{
    "CallbackCommand": "Group.CallbackAfterSendMsg", // コールバックコマンド
    "GroupId": "@TGS#2J4SZEAEL", // グループID
    "Type": "Public", // グループタイプ
    "From_Account": "jared", // 送信者
    "Operator_Account":"admin", // リクエストの送信者
    "Random": 123456, // 乱数
    "MsgSeq": 123, // メッセージ番号
    "MsgTime": 1490686222, // メッセージの時間
    "OnlineOnlyFlag": 1, //オンラインメッセージは1、そうでない場合は0となります。ライブストリーミンググループの場合はこの属性を無視し、デフォルト値の0とします。
    "MsgBody": [ // メッセージボディです。TIMMessageのメッセージオブジェクトをご参照ください
        {
            "MsgType": "TIMTextElem", // テキスト
            "MsgContent": {
                "Text": "red packet"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

開発者はデータ内のMsgBodyのメッセージタイプに基づいて一般メッセージと「いいね」ギフトメッセージを区別することができます。すべてのフィールドの意味については、ドキュメント[サーバーAPI](https://intl.cloud.tencent.com/document/product/1047/34375)をご参照ください。

ユーザーのオンラインステータス変更コールバックデータの例です。

```json
{
    "CallbackCommand": "State.StateChange",
    "EventTime": 1629883332497,
    "Info": {
        "Action": "Login",
        "To_Account": "testuser316",
        "Reason": "Register"
    },
    "KickedDevice": [
        {
            "Platform": "Windows"
        },
        {
            "Platform": "Android"
        }
    ]
}
```

開発者はInfo内のフィールドに基づいてユーザーのオンラインステータスを判断することができます。すべてのフィールドの意味については、ドキュメント[サーバーAPI](https://intl.cloud.tencent.com/document/product/1047/34357)をご参照ください。

>?また、多くのライブストリーミングルームではライブストリーミングルームの人気度を表示し、人気度に応じてライブストリーミングルームをユーザーにおすすめしています。ライブストリーミングルームの人気度の統計方法はユーザーレベルの統計方法と似ており、こちらもIMが提供するコールバックシステムによって実現できます。ここでは詳しくはご説明しません。

### ライブストリーミングルームのメッセージ履歴

AVChatRoomを使用する際、デフォルトではライブストリーミングルームのメッセージ履歴は保存されず、ユーザーが新たにライブストリーミングルームに入室した場合は、入室後にユーザーが送信したメッセージしか見ることができません。グループの新規参加ユーザーの体験を最適化するため、次のように、ライブストリーミンググループユーザーが取得できるグループ参加前のメッセージの数をコンソールで設定することができます。
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-085957.png)



>? この機能はフラッグシップ版のユーザーのみアクティブ化することができます。またグループで24時間に最大20通までのメッセージ履歴の取得のみサポートします。

ライブストリーミンググループユーザーによるグループ参加前のメッセージの取得は、他グループのメッセージ履歴の取得と同様です。コードの例は次のとおりです。
<dx-tabs>
::: Android

```java
V2TIMMessageListGetOption option = new V2TIMMessageListGetOption();
option.setGetType(V2TIMMessageListGetOption.V2TIM_GET_CLOUD_OLDER_MSG); // クラウドのより古いメッセージを取得
option.setGetTimeBegin(1640966400);         // 2022-01-01 00:00:00から開始
option.setGetTimePeriod(1 * 24 * 60 * 60);  // 1日全体のメッセージを取得
option.setCount(Integer.MAX_VALUE);         // 時間範囲内の全メッセージを返す
option.setGroupID(#you group id#);          // グループチャットメッセージを取得
V2TIMManager.getMessageManager().getHistoryMessageList(option, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```

::: 

::: iOS&Mac

```swift
// シングルチャットメッセージ履歴の取得
// 初回の取得では、lastMsgをnilに設定します
// 再度取得する際、lastMsgは返されたメッセージリストの最後の1通を使用することができます
[V2TIMManager.sharedInstance getC2CHistoryMessageList:#your user id# count:20 lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    // 次回取得するlastMsgを記録し、次回の取得に使用します
    V2TIMMessage *lastMsg = msgs.lastObject;
    NSLog(@"success, %@", msgs);
} fail:^(int code, NSString *desc) {
    NSLog(@"fail, %d, %@", code, desc);
}];
```

::: 

::: Flutter

```dart
// シングルチャットメッセージ履歴の取得
// 初回の取得では、lastMsgIDをnullに設定します
// 再度取得する際、lastMsgIDは返されたメッセージリストの最後の1通のidを使用することができます
TencentImSDKPlugin.v2TIMManager.getMessageManager().getC2CHistoryMessageList(
        userID: "userId",
        count: 10,
        lastMsgID: null,
);
```

::: 

::: Web

```js
// あるセッションを開いた際、最初に取得するメッセージリスト
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // メッセージリスト。
  const nextReqMessageID = imResponse.data.nextReqMessageID; // 続けて取得する場合に使用します。ページごとに取得する場合はこのフィールドを渡す必要があります。
  const isCompleted = imResponse.data.isCompleted; // すべてのメッセージの取得が完了したかどうかを表します。
});
// その他のメッセージをドロップダウンして確認
let promise = tim.getMessageList({conversationID: 'C2Ctest', nextReqMessageID, count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // メッセージリスト。
  const nextReqMessageID = imResponse.data.nextReqMessageID; // 続けて取得する場合に使用します。ページごとに取得する場合はこのフィールドを渡す必要があります。
  const isCompleted = imResponse.data.isCompleted; // すべてのメッセージの取得が完了したかどうかを表します。
});
```

::: 
</dx-tabs>

[メッセージ履歴取得のその他のSDKバージョンコードの例](https://intl.cloud.tencent.com/document/product/1047/47998)

### ライブストリーミングルームオンライン人数

ライブストリーミングルームでオンライン人数を表示することは、ライブストリーミングのシーンでのごく一般的なニーズの一つです。2種類の実現方法がありますが、それぞれにメリットとデメリットがあります。

1. クライアントSDKが提供する[getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a56840105a4b3371eeab2046d8c300bce)APIによる定期ポーリング方式でグループのオンライン人数を取得します。
2. ユーザーのグループ参加・退出のバックエンドコールバックによって統計を行い、サーバーAPIの[グループシステム通知](https://intl.cloud.tencent.com/document/product/1047/34958)または[グループカスタムメッセージ](https://intl.cloud.tencent.com/document/product/1047/34959)などによってグループ内の全メンバーに送信します。

クライアントSDKが提供するインターフェースによってオンライン人数を取得する方式は、シングルライブストリーミングルームモードのユーザーにとっては基本的なニーズを満たすものです。ただし、Appに複数のライブストリーミングルームがあり、なおかつ公開性の高い位置にライブストリーミングルームのオンライン人数を表示する必要がある場合は、2つ目の方法でオンライン人数の統計を行うことをお勧めします。

>? 開発者サーバーからクライアントに対しオンライン人数統計メッセージを送信する際は、例えば5秒に1回などの定時送信方式を用いることができますが、この方式では、ライブストリーミングルームの人数にあまり変化がない場合には余分なネットワークオーバーヘッドが発生することになります。人数の変化率をモニタリングする方式で更新を行うことを開発者にはお勧めします。
>
> ライブストリーミングルームオンライン人数の正確性とリアルタイム性の優先度については、開発者が業務に応じて設定することができます。

### ライブストリーミングルームのミュート

ライブストリーミングルームのミュートには2種類あり、1つはライブストリーミングルーム全体のミュート、もう1つは特定のユーザーに対するミュートです。2種類のミュートはそれぞれの業務シナリオで使用されます。

ミュートの設定は一般的にサーバーSDKを使用して行います。ライブストリーミングルーム全体のミュートは[グループ属性の設定](https://intl.cloud.tencent.com/document/product/1047/34962)の全員ミュートフィールドで設定します。単独のグループメンバーに対するミュートは、[グループメンバー属性の設定](https://intl.cloud.tencent.com/document/product/1047/34951)で設定します。

ライブストリーミングルーム管理者がバックエンドでグループミュートを設定すると、クライアントは対応するコールバックイベントを受信した後、ユーザーの入力ボックスをdisable状態に設定しなければなりません。これはユーザーがメッセージを送信した際に、メッセージの送信に失敗したと表示されることを防ぐためです。ミュートを解除した後は、入力ボックスはenable状態に設定しなければなりません。

クライアントの対応するコールバックコードは次のとおりです。

<dx-tabs>
::: Android

```java
V2TIMGroupListener groupListener = new V2TIMGroupListener() {
  // グループメンバーに関する通知、グループライフサイクルに関する通知、グループ参加申請に関する通知、トピックイベント監視コールバックなどは個々に列挙しません
  @Override
  public void onGroupInfoChanged(String groupID, List< V2TIMGroupChangeInfo > changeInfos) {
    // グループプロファイル変更
  }
  @Override
  public void onMemberInfoChanged (String groupID, List< V2TIMGroupMemberChangeInfo > v2TIMGroupMemberChangeInfoList) {
    // グループメンバープロファイル変更
  }
  
};
```

::: 

::: iOS&Mac

```swift
V2TIMManager.getInstance().addGroupListener(groupListener);
[[V2TIMManager sharedInstance] addGroupListener:self];

// グループメンバーに関する通知、グループライフサイクルに関する通知、グループ参加申請に関する通知、トピックイベント監視コールバックなどは個々に列挙しません
- (void)onGroupInfoChanged:(NSString *)groupID memberList:(NSArray<V2TIMGroupMemberInfo *>*)memberList {
    // グループプロファイルの変更あり
}

- (void)onMemberInfoChanged:(NSString *)groupID member:(V2TIMGroupMemberInfo *)member {
    // グループメンバープロファイル変更
}

```

::: 

::: Flutter

```dart
// グループ参加イベントの監視
 TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onGroupInfoChanged: ((groupID, memberList) {
    // グループプロファイルの変更あり
},onMemberInfoChanged: ((groupID, memberList) {
    // グループメンバープロファイル変更
})));
```

::: 

::: Web

```js
let onGroupListUpdated = function(event) {
   console.log(event.data);// Groupインスタンスを含む配列
};
tim.on(TIM.EVENT.GROUP_LIST_UPDATED, onGroupListUpdated);
```

::: 
</dx-tabs>

[グループ監視のその他のSDKバージョンコードの例](https://intl.cloud.tencent.com/document/product/1047/48466)

グループメンバーのミュート状態の変更は、デフォルトではクライアントに通知されず、[コンソールで設定](https://console.cloud.tencent.com/im/qun-setting)しなければならないことに注意が必要です。
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-090219.png)

>?現在AVChatRoomではプロファイル変更通知の送信をサポートしていないため、AvChatRoomに対して、開発者は[カスタムメッセージ](https://intl.cloud.tencent.com/document/product/1047/34959)を送信して通知することができます。

### ライブストリーミングルームからの強制退室

ライブストリーミングルームのミュートと同様に、開発者はサーバーの[グループ強制退出](https://intl.cloud.tencent.com/document/product/1047/34949)インターフェースを通じて、グループメンバーを強制退出させることができます。ただし、AVChatRoomはこのインターフェースをサポートしていないため、他の方法で実現する必要があります。

方法は次のとおりです。

1. バックエンドがグループカスタムメッセージを送信し、カスタムメッセージの内容を強制退出ユーザーのuserIDにします。一度に強制退出させる人数が多すぎる場合はメッセージボディのサイズに注意し、何度かに分けて送信します。
2. 業務バックエンドでグループ参加ブラックリストを保守します
3. クライアントがカスタムメッセージを受信して解析し、userIDに自身のuserIDが含まれる場合は自主的にグループ退出インターフェースを呼び出します
4. ユーザーのグループ参加前コールバックを設定し、現在グループに参加しようとしているユーザーがステップ2のブラックリストにないかどうかをチェックします。

[コンソールの関連設定](https://console.cloud.tencent.com/im/callback-setting)は図のとおりです。

![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-090320.png)


#### ライブストリーミングルームのセンシティブコンテンツフィルタリング

ライブストリーミングルームのセンシティブコンテンツをフィルタリングすることも、ライブストリーミング業務の非常に重要な機能です。実現方法は次のとおりです。

1. ユーザーグループにメッセージ送信前コールバックをバインドします
2. コールバックデータからメッセージタイプを判断し、メッセージデータを天御またはその他のサードパーティチェックサービスに転送します
3. メッセージが一般テキストメッセージの場合は、天御のチェックを待って同期的に返すことができ、メッセージを送信するかどうかのデータパケットをIMバックエンドに返します
4. メッセージがマルチメディアメッセージの場合は、メッセージ送信のデータパケットを直接IMバックエンドに返すことができます。さらに天御から非同期的に返された結果を返した後、メッセージに違反が発見された場合は、メッセージ編集インターフェースまたはグループカスタムメッセージインターフェースを通じてメッセージ変更通知を送信することができます。クライアントは通知を受信した後、違反メッセージをブロックします。

メッセージ送信前コールバックデータの例です。

```json
{
    "CallbackCommand": "Group.CallbackBeforeSendMsg", // コールバックコマンド
    "GroupId": "@TGS#2J4SZEAEL", // グループID
    "Type": "Public", // グループタイプ
    "From_Account": "jared", // 送信者
    "Operator_Account":"admin", // リクエストの送信者
    "Random": 123456, // 乱数
    "OnlineOnlyFlag": 1, //オンラインメッセージは1、そうでない場合は0となります。ライブストリーミンググループの場合はこの属性を無視し、デフォルト値の0とします。
    "MsgBody": [ // メッセージボディです。TIMMessageのメッセージオブジェクトをご参照ください
        {
            "MsgType": "TIMTextElem", // テキスト
            "MsgContent": {
                "Text": "red packet"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

開発者はMsgBody内のMsgTypeフィールドによってメッセージタイプを判断することができます。フィールド全体の説明については[コールバックドキュメント](https://intl.cloud.tencent.com/document/product/1047/34374)をご参照ください。

開発者は違法なメッセージに対して異なる処理を選択することができ、コールバック内のリターンパケットによってIMバックエンドで制御することができます。

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // ErrorCodeごとに意味が異なります
}
```



| ErrorCode | 意味                        |
| --------- | --------------------------- |
| 0         | 発言を許可し、メッセージは正常に送信されます    |
| 1         | 発言を拒否し、クライアントは10016を返します |
| 2         | サイレントで破棄し、クライアントは正常を返します  |

開発者は自身の業務ニーズに応じて選択し、使用できます

センシティブコンテンツチェックのフローチャートは次のとおりです。

![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-091347.png)


### ライブストリーミングルームのグループメンバーリスト

ライブストリーミングルームにオンラインのグループメンバーリストを表示する必要がある場合は、`getGroupMemberList`インターフェースによってグループメンバーリストを取得することができますが、AVChatRoomでは人数が多いため、全量のメンバーリストを取得する機能は提供していません。機能はフラッグシップ版か非フラッグシップ版かによって異なります。

1. フラッグシップ版以外のお客様は、`getGroupMemberList`を呼び出して、直近でグループに参加した30名のグループメンバーを取得することができます。
2. フラッグシップ版のお客様は、`getGroupMemberList`を呼び出して、直近でグループに参加した1000名のグループメンバーを取得することができます。この機能はIMコンソールで有効化する必要があり、有効化しなければデフォルトで非フラッグシップ版と同様に、直近でグループに参加した30名のグループメンバーのみを取得します。

コンソールの設定は図2.6のとおりです。

![img](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-090445.png)

フラッグシップ版以外の場合、開発者は`getGroupMemberList`とグループ監視中のonGroupMemberEnterおよびonGroupMemberQuitコールバックによって、現在オンラインのグループメンバーリストをクライアントで保守することもできます。ただし、この方法では、ユーザーがライブストリーミングルームから退出して入り直した場合も、最新の30名のグループメンバーしか取得できません。

### ライブストリーミングルームの弾幕抽選

ライブストリーミング抽選はメッセージ統計に似ており、どちらもメッセージ送信後コールバックを使用する必要があります。メッセージの内容をチェックして、抽選キーワードにヒットしたユーザーを抽選プールに加えます。ここではこれ以上の補足説明は行いません。

### ライブストリーミング弾幕
 AVChatRoomは、弾幕、ギフト、「いいね」など複数のメッセージタイプをサポートし、優れたライブストリーミングチャットのインタラクティブな体験を手軽に構築できます。
![](https://qcloudimg.tencent-cloud.cn/raw/5c854b6e5754167b6fd394072d4bc42a.png)

### ライブストリーミングルーム内のブロードキャスト

ブロードキャスト機能はライブストリーミングルームでのシステムからのお知らせ機能に相当しますが、お知らせとは異なり、ブロードキャスト機能はメッセージに分類されます。システム管理者がブロードキャストメッセージを送信すると、SDKAppID下のすべてのライブストリーミングルームでこのメッセージを受信することができます。

ブロードキャスト機能は現在はフラッグシップ版のみの機能であり、コンソールでアクティブ化する必要があります。

業務バックエンドからのブロードキャストメッセージ送信については、ドキュメント[ライブストリーミンググループのブロードキャストメッセージ](https://intl.cloud.tencent.com/document/product/1047/49440)をご参照ください。

>?開発者のバージョンがフラッグシップ版ではない場合は、サーバーからグループカスタムメッセージを送信して実現できます。
>

## 3、ライブストリーミングのオーディオビデオストリーム部分

- ### キャスター側（プッシュ）

  現在、Tencent Cloud CSSプッシュには、次のいくつかの方法があります。

  1. クライアントプッシュには[OBSツールプッシュ](https://intl.cloud.tencent.com/document/product/267/31569)を使用できます
  2. Web端末では[Webプッシュ](https://console.cloud.tencent.com/live/tools/webpush)を使用できます
  3. App端末では[モバイルライブストリーミングSDKプッシュ](https://www.tencentcloud.com/document/product/1071/38158)を使用できます
  
>? キャスター側でのプッシュの前にはプッシュアドレスの設定が必要です。[プッシュ設定](https://intl.cloud.tencent.com/document/product/267/31059)または[アドレスジェネレーター](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)を参照してアドレスを生成してください。

- ### ユーザー側（プル）

  ユーザー側でのCSSストリームの取得方法にも、次のようないくつかの方法があります。

  1. PC端末では[VLCツールの再生](https://intl.cloud.tencent.com/document/product/267/32483)を使用できます
  2. Web端末では[Player+での再生](https://www.tencentcloud.com/document/product/1071/41881)を使用できます
  3. App端末では[Player+での再生](https://www.tencentcloud.com/document/product/1071/38158)を使用できます
  
>? プルの前にも再生アドレスの設定が必要です。[再生設定](https://intl.cloud.tencent.com/document/product/267/31058)または[アドレスジェネレーター](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)を参照してアドレスを生成してください。

- ### Live Video Caster

  ライブストリーミングシーンのより多くのニーズを満たすために、開発者はクラウドの[Live Video Caster](https://console.cloud.tencent.com/live/caster)を使用してCSSストリームの処理を行うことができます。現在Live Video Casterは次の機能をサポートしています。

  1. CSSウォーターマーク、テキスト、トランジション
  2. VODからライブストリーミングへの変換
  3. ライブストリーミング画質、ビットレート、解像度の設定
  4. ライブストリーミングのレイアウト調整
  5. CSSレコーディング
  6. ライブストリーミング弾幕の追加
  7. CSSストリームの監視


- ### TRTCライブストリーミング

  Tencent Real-Time Communication（TRTC）の使用によっても、同様にライブストリーミングの機能を実装することができます。CSSと比べて、TRTCは次のようなより高度な機能を備えています。

  1. [Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618)
  2. [クラウドレコーディングと再生](https://intl.cloud.tencent.com/document/product/647/35426)
  3. [低遅延のリアルタイムCDN視聴](https://intl.cloud.tencent.com/document/product/647/35242)
  4. ...

## 4、よくあるご質問
### 1. 自身がメッセージを送信する際、メッセージ送信状態の `Message.nick` と `Message.avatar` フィールドがどちらも空である場合、インターフェース上でニックネームとプロフィール画像を正常に表示するにはどうすればよいですか。
getUserInfoインターフェースによって、ご自身のユーザー情報のnickおよびavatarフィールドを、メッセージ送信のnickおよびavatarフィールドにすることができます。

### 2. TRTCとCSSはどのように選択すればよいですか。
TRTCライブストリーミングは遅延が少なく、キャスターとのインタラクションをより便利に実現できますが、価格がやや高いです。CSSは遅延がわずかに大きいですが、価格は安いです。

### 3. メッセージが紛失するのはなぜですか。

メッセージ紛失の原因として次の原因が考えられます。

- ライブストリーミンググループは、40通/秒のレート制限があります。メッセージ送信前のコールバックとメッセージ送信後のコールバックを介して判断できます。紛失したメッセージが、メッセージ送信前にコールバックを受信し、メッセージ送信後にコールバックを受信していない場合、このメッセージは制限を受けています。
- [よくあるご質問4](#p4)を参考に、Web端末から退出したことによって、Android、iOS、PCで同期的な退出が生じているかどうかを判断することができます。
- Webで問題が発生した場合は、使用しているSDKがV2.7.6より以前のバージョンかどうかを確認してください。V2.7.6より以前の場合は、最新版にアップグレードしてください。

上記の可能性をすでに排除している場合は、チケットを提出して弊社にご連絡ください。

### 4. ビデオとチャットを直接使用できるオープンソースのライブストリーミングコンポーネントはありますか。

はい、コードはオープンソースです。詳細については、 [Tencent Cloud TWebLIVEコンポーネント](https://github.com/tencentyun/TWebLive)をご参照ください。


## 5、お問い合わせ

Tencent Cloud IMの技術コミュニケーショングループに参加すると、次のものが得られます。

- 信頼できるテクニカルサポート
- 詳細な製品情報
- 緊密な業界交流

Telegramコミュニケーショングループ：[クリックして参加](https://t.me/tencent_imsdk)

