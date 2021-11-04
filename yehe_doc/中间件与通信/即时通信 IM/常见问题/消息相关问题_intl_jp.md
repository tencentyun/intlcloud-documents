[](id:Q1)
### IMとTPNSは同時に統合され、たくさんのベンダーが競合していますが、この問題を解決するにはどうすればよいですか。
現在、IMは、[TPNS](https://intl.cloud.tencent.com/product/tpns)が提供するベンダーjarパッケージを使用しています。ドキュメント[IMオフラインプッシュ（Android）](https://intl.cloud.tencent.com/document/product/1047/39156)を参照して、関連する依存パッケージを置き換えることで、この問題を解決できます。

[](id:Q2)
### メッセージが受信されないか、または失われた場合はどうすればよいですか。

-  シングルチャットメッセージ
 - メッセージの送信が完了しているかどうかを確認します。
 - 受信者がログインを完了しているかどうかを確認します。
 - メッセージを送信した指定セッションが受信者と同じかどうかを確認します。
- グループメッセージ
 - メッセージの送信が完了しているかどうかを確認します。
 - 受信者がログインを完了しているかどうかを確認します。
 - 受信者がグループメンバーであるかどうかを確認します。

C2Cメッセージかグループメッセージかを問わず、上記の手順で問題を確認できない場合は、引き続き次の状況を確認する必要があります。
1. メッセージリスナーを登録したかどうかを確認します。
2. 送信者がメッセージを送信した際に、`elem`をメッセージに追加したかどうかを確認します（メッセージを送信する際に`addElement`の戻り値を確認する必要があります）。
3. Androidでは、複数のメッセージリスナーを登録したかどうか、また、メッセージリスナーで`true`が返されたかどうかを確認する必要があります。


[](id:Q3)
### オフラインプッシュを受信できない場合はどうすればよいですか。

- APNs
[オフラインプッシュ（iOS）](https://intl.cloud.tencent.com/zh/document/product/1047/34347)の説明ドキュメントを参照して、以下を確認してください。
 - 証明書がTencent Cloudコンソールに正しくアップロードされているかどうかを確認します。
 - ログインに成功した後、tokenのTencent Cloudへのアップロードが成功したかどうかを確認します。
 - tokenの報告時に正しい証明書IDが報告されているかどうかを確認します。
 - フロントエンドイベントとバックエンドイベントが正しく報告されているかどうかを確認します。
 - メッセージに`TIMCustomElem`のみがあり、そのうちの` desc`属性がブランクであるかどうかを確認します。
 - `MsgRandom`など、重複排除フラグが同じに設定されているため、重複排除が発生し、プッシュできません。
 - グループメッセージの場合、メッセージを通知しないオプションが設定されているかどうか。

- Android
[オフラインプッシュ](https://intl.cloud.tencent.com/document/product/1047/34336)の説明ドキュメントを参照して、以下を確認してください。
 - プッシュ証明書が正しくアップロードされているかどうかを確認します。
 - tokenが正常に報告されているかどうかを確認します。
 - サードパーティのオフラインプッシュ(Huawei、Xiaomi、Meizu)でない場合は、QALServiceプロセスが存在しているかどうかを確認します。存在していない場合、オフラインプッシュは受信されないため、システムの自動起動権限に依存する必要があります。
 - 複数のプロセスの場合、IM SDKはメインプロセスでのみ初期化されているかどうか。正気化されていない場合は、メインプロセスでのみ初期化するように変更する必要があります。
 - Xiaomi、Huawei、Meizuといったサードパーティのオフラインプッシュの場合は、まず対応するサードパーティのコンソールから直接メッセージをプッシュして、電話を受信できるかどうかを確認できます。受信できない場合、次の2つの理由が考えられます。
    1）サードパーティのオフラインプッシュを統合するユーザーに問題があります。ドキュメントに従って操作してください。
    2）携帯電話の互換性の問題。携帯電話自体はオフラインプッシュと互換性がありません。例えば、一部のHuawei携帯電話は、Huaweiのオフラインプッシュを受信できません。
 - OPPOによるオフラインプッシュの場合は、IMコンソールのAndroidプッシュ証明書に、AppSecretではなくMasterSecretを入力しているか確認してください。

APNプッシュか、またはAndroidでのオフラインプッシュかどうかに関わらず、上記の手順で問題を確認できない場合は、引き続き以下の状況を確認する必要があります。
1. 受信者IDがプッシュされるメッセージのユーザーIDと一致しているかどうかを確認します。
2. オフラインプッシュリスナー（Android）が設定されているかどうかを確認します。
3. DNDが設定されているかどうかを確認します。iOSについては、[プッシュ通知音のカスタム設定](https://intl.cloud.tencent.com/zh/document/product/1047/34347)を参照し、Androidについては、[グローバルオフラインプッシュの設定](https://intl.cloud.tencent.com/document/product/1047/34336#.E8.AE.BE.E7.BD.AE.E5.85.A8.E5.B1.80.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81.E9.85.8D.E7.BD.AE)を参照します。
4. メッセージが`sendOnlineMessage`インターフェースを介して送信されたオンラインメッセージであるかどうかを確認するか、RESTAPIを介してプッシュするときに`MsgLifeTime`を`0`に設定します。
5. メッセージにオフラインプッシュを実行しないフラグが設定されているかどうかを確認します。iOSについては、[オフラインメッセージプロパティのカスタマイズ](https://intl.cloud.tencent.com/zh/document/product/1047/34347)を参照し、Androidについては、[単一メッセージのオフラインプッシュ構成の設定](https://intl.cloud.tencent.com/document/product/1047/34336#.E9.92.88.E5.AF.B9.E5.8D.95.E6.9D.A1.E6.B6.88.E6.81.AF.E8.AE.BE.E7.BD.AE.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81)をご参照ください。
6. それでも場所を特定できない場合は、技術者に関連情報を提供し、トラブルシューティングを行うことができます。

[](id:Q4)
### グループ@メッセージはどのように処理すればよいですか。
グループ内の@メッセージと通常メッセージの間に本質的な違いはありませんが、@の付いた人がメッセージを受信すると、UIで特別な処理が必要になります。例えば、QQのメッセージリストに赤いプロンプトが表示されます。具体的な実装については、以下のソリューションを参照できます。
1. メッセージ送信時のキーボードイベントに、@文字が入力されているかどうかを監視します。送信者が@文字を入力したことが検出されると、グループメンバーリストがUIにポップアップ表示され、送信者が@を付ける必要のある人を選択できます。ここでは、選択したユーザーがuser1であると仮定します。
2. @を付ける必要のある人を選択した後、メッセージ入力ボックスに「@ user1」など、@および選択した人のIDを追加します。
3. メッセージに`TIMCustomElem`を追加し、`TIMCustomElem`で自分が設計したフラグを追加し、このメッセージを@メッセージのメッセージプロトコルとします。
簡単なプロトコル定義は次のとおりです。
```
{
	"type":"REMIND",
	"target":"user1"
}
```
@メッセージ作成プロセスのサンプルコードは次のとおりです（例としてAndroidプラットフォームを取り上げます）。

```java
// テキストメッセージを送信し、メッセージ内で@グループメンバーuser1とします
TIMMessage msg = new TIMMessage();
### テキストメッセージ要素を作成します
TIMTextElem txtElem = new TIMTextElem();
txtElem.setText("@user1 nice to meet u");
if(msg.addElement(txtElem) != 0){
	Log.e(TAG, "add text elem failed");
	return;
}
try{
	// カスタマイズしたメッセージプロトコルを入力します
	JSONObject remindProto = new JSONObject();
	remindProto.put("type", "REMIND");
	remindProto.put("target", "user1");
	// 自分で定義したプロトコルに従ってカスタムメッセージ要素を作成します
	TIMCustomElem customElem = new TIMCustomElem();
	customElem.setDesc("remind msg");
	customElem.setData(remindProto.toString().getBytes("utf-8"));
	if(msg.addElement(customElem) != 0){
		Log.e(TAG, "add custom elem failed");
		return;
	}
}catch(Exception e){
	Log.e(TAG, "build custom elem failed");
	return;
}
```

>!そのうち、`TIMTextElem`は必須ではありません。ダーティワードフィルタリングが不要であることが確認された場合、`TIMTextElem`のメッセージ内容を`TIMCustomElem`の`desc`属性に入力できます。
>
4. メッセージを作成したら、グループに送信します。
5. グループのメンバーがメッセージを受信したら、メッセージの`TIMCustomElem`のメッセージプロトコルが@メッセージプロトコルであるかどうかを確認します。そうである場合は次の手順に進み、そうでない場合はスキップします。
6. @を付けられた人が、現在ログインしているユーザーと同じであるかどうかを確認します。同じである場合は、UIで特殊処理を行います。そうでない場合、処理は不要です。

[](id:Q5)
### Red Packetメッセージはどのように処理すればよいですか。

Red Packetメッセージは、@メッセージと似通っており、 `TIMCustomElem`を介して実装できます。UI上で対応する特殊処理を適用する必要があります。例えば、現在のメッセージがRed Packetメッセージであることを確認した場合、メッセージはRed Packetの形式で表示されます。
また、Red Packetメッセージは重要なメッセージです。頻度制限に達してもメッセージを配信できるように、メッセージを送信するときに優先度の高いメッセージとして設定することをお勧めします（現在、グループ内のメッセージのデフォルトの頻度制限は40件/秒であり、シングルチャットメッセージのデフォルトの頻度制限は5件/秒です）。

メッセージの優先度に関する内容については、[メッセージの優先度](https://intl.cloud.tencent.com/document/product/1047/33526)をご参照ください。

>!Red Packetメッセージの支払部分の機能では、アプリケーションが対応する支払SDKを統合する必要があります。現時点でIM SDKは、この部分の機能を提供していません。

Red Packetメッセージの簡単な作成プロセスは次のとおりです(Android)。
```java
// 新しいメッセージを作成します
TIMMessage msg = new TIMMessage();
try{
	// カスタマイズしたメッセージプロトコルを入力します
    JSONObject redPacket= new JSONObject();
	redPacket.put("type", "RED_PACKET");
    redPacket.put("amount", 2018);
	redPacket.put("msg", "Happy new year!");

    // 自分で定義したプロトコルに従ってカスタムメッセージ要素を作成します
	TIMCustomElem customElem = new TIMCustomElem();
    customElem.setDesc("red packet");
	customElem.setData(redPacket.toString().getBytes("utf-8");
    if(msg.addElement(customElem) != 0){
	    Log.e(TAG, "add custom elem failed");
	    return;
	}
}catch(Exception e){
	Log.e(TAG, "build custom elem failed");
    return;
}

// メッセージの優先度を高優先度に設定します
msg.setPriority(TIMMessagePriority.High);
```

[](id:Q6)
### IMメッセージの保存期間はどのくらいですか。
シングルチャットメッセージと非ライブストリーミンググループメッセージには、メッセージ履歴の保存機能があります。<a href="https://console.cloud.tencent.com/im">IMコンソール</a>にログインして、関連の設定を変更することができます。それぞれのパッケージのデフォルト設定は次のとおりです。<ul style="margin:0;"><li>体験版：7日間。延長機能はサポートしていません。</li><li>プロフェッショナル版：7日間。延長機能をサポートしています。</li><li>フラッグシップ版：30日間。延長機能をサポートしています。</li></ul>履歴メッセージの保存期間の延長は、有料の付加価値サービスです。料金の詳細については、<a href="https://intl.cloud.tencent.com/document/product/1047/34350">付加価値サービスの料金</a>をご参照ください。

[](id:Q7)

### 送信者がブラックリストに登録されているのに、メッセージの送信が成功したと表示されるのはなぜですか。
IMは、コンソールの[ブラックリストチェック](https://intl.cloud.tencent.com/document/product/1047/34419)管理において、メッセージ送信後に成功した送信を表示する機能を提供します。この機能を有効にすると、ブラックリストに登録されたユーザーがメッセージを送信した後も、送信が成功したことが表示されます（実際には相手はメッセージを受信しません）。この設定を無効にすると、ブラックリストに登録されたユーザーはメッセージの送信後に「失敗」と表示され、SDKは[エラーコード20007](https://intl.cloud.tencent.com/document/product/1047/34348)を受信します。具体的な設定については、ドキュメント[ブラックリストチェック](https://intl.cloud.tencent.com/document/product/1047/34419)をご参照ください。

