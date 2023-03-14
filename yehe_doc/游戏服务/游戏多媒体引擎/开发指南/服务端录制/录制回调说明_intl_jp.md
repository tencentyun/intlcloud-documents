## サーバー側レコーディングコールバックの説明[](id:date)

### 説明
ネットワークの影響を受け、サーバーで通知を受信した順番は、イベントの発生順番と異なる可能性があります。  
こちらから提供するサービスにはリトライメカニズムはありますが、すべてのメッセージが届く保証はできません。  
そのため、お客様の重要な業務ロジックがメッセージ通知サービスに依存しないようにすることをお勧めします。

### ネットワークプロトコル

コンソールでコールバックアドレス、すなわち、HTTP(S)プロトコルインターフェースのURLを設定した場合、POSTメソッドをサポートし、データ転送にUTF-8エンコードを使用する必要があります。

### HTTPヘッダーのパラメータ

<table>
<tr><th>名前</th><th>タイプ</th><th>必須か</th><th>説明</th></tr>
<tr>
<td>Signature</td>
<td>string</td>
<td>はい</td>
<td>署名。詳細については、以下の<a href="#Signature">署名生成</a>の説明をご参照ください</td>
</tr></table>

### 署名生成[](id:Signature)

Signature = HMAC-SH1 ( strContent, SecretKey )

- **strContent**：署名そのものの文字列であり、bodyのJSON内容（長さはContent-Lengthと同様）です。
- **body**：業務にコールバックするJSON内容。以下の[コールバックの例](#example) におけるすべての内容はbodyです。
- **SecretKey**：キー。アプリケーションの権限キーで、[コンソール > アプリケーションの詳細](https://console.tencentcloud.com/gamegme)で参照できます。
- **HMAC-SH1**：署名アルゴリズム。


### コールバックのパラメータ

<table>
<thead><tr>
<th width="20%">名前</th>
<th width="20%">タイプ</th>
 <th width="60%">説明</th>  
</tr></thead>
<tbody><tr>
<td>BizID</td>
<td>Integer</td> 
<td>アプリケーションのAppID。<a href="https://console.tencentcloud.com/gamegme">コンソール > アプリケーションの詳細</a>で参照できます。</td> 
</tr>
<tr>
<td>RoomID</td>
<td>String</td> 
<td>ルームID</td> 
</tr>
<tr>
<td>UserID</td>
<td>String</td> 
<td>ユーザーID</td> 
</tr>
<tr>
<td>RecordMode</td>
<td>Integer</td> 
<td >レコーディングモード<ul style="margin:0">
	<li/>0: シングルストリーミング
	<li/>1: ミックスストリーミング
</ul ></td>
</tr>
<tr>
<td>Timestamp</td>
<td>Integer</td> 
<td>コールバックを送信した時のタイムスタンプ（s）</td> 
</tr>
<tr>
<td>TaskID</td>
<td>Integer</td> 
<td>クラウドレコーディングサービスに割り当てたタスクID。タスクIDは1回のレコーディングライフサイクルの一意の識別子であり、レコーディング終了後に意味がなくなります。カスタムレコーディングモードを使用した場合、
タスクIDは、レコーディング開始時にレスポンスパラメータにより取得でき、次回このレコーディングタスクを操作する時のリクエストパラメータとして、業務を保存する必要があります。</td> 
</tr>
<tr>
<td>EventType</td>
<td>Integer</td> 
<td>イベントタイプ</td> 
</tr>
</tr>
<tr>
<td>Detail</td>
<td><a href="#EventDetail">EventDetail</a></td> 
<td>イベント詳細。EventTypeでフォーマットが決まります</td> 
</tr>
</table>



### EventDetailイベントの詳細な説明[](id:EventDetail)

| EventType | 説明             | Detail                                                         |
| --------- | --------------- | ------------------------------------------------------------ |
| 1         | オーディオファイルレコーディング開始   | <ul><li>SeqNo: Number。マルチパートの番号</li><li> FileName: String。ファイル名</li></ul> |
| 2         | オーディオファイルレコーディング完了   | <ul><li>SeqNo: Number。マルチパートの番号</li><li> FileName: String。ファイル名</li></ul> |
| 3         | オーディオファイルアップロード完了   | <ul><li>SeqNo: Number。マルチパートの番号</li><li> FileName: String。ファイル名</li></ul> |


### コールバックの例[](id:example)

```json
{
    "BizID":1400000000,
    "RoomID":"100",
    "UserID":"999",
    "TaskID":446946705284000000,
    "RecordMode":1,
    "Timestamp":1675930605,
    "EventType":1,
    "Detail":{
    	"SeqNo":0,
    	"FileName":"1400000000_100_999/2023-02-09-16-16-45_446946705284000000_audio.mp3"
    }
}
```