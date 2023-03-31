## 機能説明
まとめて転送する機能を実装する場合は、次の手順を実行する必要があります：
1. 元のメッセージリストからまとめるメッセージを作成します。
2. まとめたメッセージをピアに送信します。
3. まとめたメッセージを受信した後、ピアは元のメッセージリストを解析します。

下図に示すように、まとめたメッセージを表示させるには、タイトルと概要情報も必要です：

| まとめて転送                                                 | まとめたメッセージを表示させる                               | まとめたメッセージをクリックして、まとめたメッセージの一覧表示をダウンロード |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="https://qcloudimg.tencent-cloud.cn/raw/cb970fdd471cdd668b5ce31d188970fd.png" width = "300" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/2304c7ea1e29de702f99d96e52a9739c.png" width = "300" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/f2c81dc8df0064cf8202d06a79f7af16.png" width = "300"/> |


## メッセージをまとめて転送
### まとめて転送するメッセージの作成・送信

まとめるメッセージを作成する場合、まとめるメッセージのリストを設定するだけでなく、タイトルと概要情報も設定する必要があります。実装プロセスは次のとおりです：
1. まとめるメッセージを作成します。まとめるメッセージを作成するとき、元のメッセージリスト、まとめるメッセージのタイトル、まとめるメッセージの概要などの情報を設定する必要があります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/dbc9a0f199effcf6d865b6497ec185f3.png" width = "450" /> 
<table>
<thead>
<tr>
<th>プロパティ</th>
<th>意味</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>merge_elem_message_array</td>
<td>元のメッセージリスト</td>
<td>まとめて転送する元のメッセージリスト</td>
</tr>
<tr>
<td>merge_elem_title</td>
<td>タイトル</td>
<td>まとめるメッセージのタイトル。たとえば、上記の図に示す「XixiyahとHelloのチャット履歴」です。</td>
</tr>
<tr>
<td>merge_elem_abstract_array</td>
<td>概要リスト</td>
<td>まとめるメッセージの概要情報。上記の図に示すように、まとめるメッセージは元のメッセージの概要情報を事前に表示させる必要があり、ユーザーがCellをクリックした後にのみ完全なメッセージの内容が表示されます。</td>
</tr>
<tr>
<td>merge_elem_compatible_text</td>
<td>対応のテキスト情報</td>
<td>低バージョンのSDKが統合メッセージをサポートしていない場合は、デフォルトでテキストメッセージを受信します。テキストメッセージの内容はmerge_elem_compatible_textです。</td>
</tr>
</tbody></table>
2. まとめるメッセージを作成して送信するためのサンプルコードを以下に示します：
<dx-codeblock>
:::  c#
// 転送する必要のあるメッセージリスト。メッセージリストには統合メッセージを含めることができますが、グループTipsメッセージを含めることはできません
var message = new Message
{
   message_conv_id = conv_id,
   message_conv_type = TIMConvType.kTIMConv_Group,
   message_elem_array = new List<Elem>{
    new Elem
   {
     elem_type = TIMElemType.kTIMElem_Merge,
     merge_elem_title = "user1とuser2のチャット", // まとめるメッセージのタイトル
     merge_elem_message_array = new List<Message>
     {
      message1,
      message2
     },
     merge_elem_abstract_array = new List<string>
     {
      "user1:hello", "user2:こんにちは" // まとめるメッセージの概要リスト
     },
     merge_elem_compatible_text = "現在のバージョンではこのメッセージがサポートされていません" // まとめるメッセージの対応テキスト。低バージョンのSDKがまとめるメッセージをサポートしていない場合は、デフォルトでテキストメッセージを受信します。テキストメッセージの内容はcompatibleTextです
   }},
};
StringBuilder messageId = new StringBuilder(128);
TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_Group, message, messageId, (int code, string desc, string json_param, string user_data)=>{
 // メッセージの非同期送信の結果
});
:::
</dx-codeblock>




### まとめて転送するメッセージの受信

#### リスナーの追加
受信者から`AddRecvNewMsgCallback`([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/AddRecvNewMsgCallback.html))を呼び出すことで、セッションリスナーを追加できます。
一般に、アプリが時間内にメッセージを確実に受信できるように、チャットメッセージのインターフェースが初期化された後など、比較的早い時点で呼び出すことをお勧めします。

サンプルコードは次のとおりです：


```c#
TencentIMSDK.AddRecvNewMsgCallback((List<Message> messages, string user_data)=>{
  foreach(Message message in messages)
  {
    foreach (Elem elem in message.message_elem_array)
    {
      // 次のメッセージがある
      if (elem.elem_type == TIMElemType.kTIMElem_Merge)
      {
      }
    }
  }
})
```


#### メッセージの解析
リスナーを追加すると、受信者は`RecvNewMsgCallback`でまとめたメッセージの`Message`を受信します。
まとめるメッセージの要素を使用して、先に`merge_elem_title`と `merge_elem_abstract_array`のUI 表示を取得できます。
ユーザーがまとめたメッセージをクリックすると、`MsgDownloadMergerMessage`([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgDownloadMergerMessage.html))インターフェースを呼び出して、まとめたメッセージリストのUI表示をダウンロードします。

サンプルコードは次のとおりです：


```c#
if(elem.TIMElemType == TIMElemType.kTIMElem_Merge){
   elem.merge_elem_abstract_array;
   elem.merge_elem_layer_over_limit;
   elem.merge_elem_title;
   TIMResult res = TencentIMSDK.MsgDownloadMergerMessage(message, (int code, string desc, List<Message> messages, string user_data)=>{
    // 非同期処理のロジック
   });
}
```



## メッセージを1つずつ転送
単一のメッセージを転送する必要がある場合は、先に元のメッセージとまったく同じ内容の転送メッセージを作成してから、`MsgSendMessage` ([クリックして詳細を表示](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSendMessage.html))インターフェースを呼び出して転送メッセージを送信できます。
