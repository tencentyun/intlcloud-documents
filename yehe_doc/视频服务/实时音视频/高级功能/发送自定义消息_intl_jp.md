## 内容紹介

TRTC SDK はカスタムメッセージを送信する機能を提供します。この機能を介して、キャスターのロールを持つユーザーは同じビデオルーム内の他のユーザーに自身のカスタムメッセージをブロードキャストすることができます。

## サポートするプラットフォーム

| iOS | Android | Mac OS | Windows | Electron| web|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|   &#10003;  |   &#10003;   |   &#10003;  |   &#10003;   | &#10003;  |  ×  |

## 送受信の原理
あるユーザーのカスタマイズメッセージは音声ビデオデータストリーム内にクリップされ、音声ビデオデータストリームと同時にルーム内の他のユーザーに送信されます。音声ビデオライン自体は100%信頼できるものではないため、信頼性を高めるため、TRTC SDK 内部に信頼性保護メカニズムを実装しています。

![](https://main.qcloudimg.com/raw/cc11b0e81970929ef28d2074c8297753.jpg)

## メッセージの送信

TRTCCloud の `sendCustomCmdMsg` インターフェースを呼び出して送信する場合は、送信時に4つのパラメータを指定する必要があります：


| パラメータ名 | パラメータの説明 |
|:--------:|:--------------|
| cmdID | メッセージID。値の範囲は 1 ~ 10、異なるサービスタイプのメッセージには異なるcmdIDを使用する必要があります。 |
| data | 送信待機メッセージ。最大 1KB（1000バイト）のデータサイズをサポートします。 |
| reliable | 信頼できる送信かどうか。受信者は再送信を待機するため一定時間データを一時的に保存する必要があることから、信頼できる送信の代償として一定のタイムディレイを受け入れます。|
| ordered | 順序要求の有無、つまり受信者が受信するデータの順序と送信者が送信する順序が一致することが要求されるかどうかであり、このことによって、受信側はこれらのメッセージを一時的に保存し並べ替える必要があるため、一定の受信タイムディレイが生じます。 |

>reliable とordered を同時にYES または NOに設定してください。現在のところ、クロス設定はサポートされていません。

- **Objective-C**

``` Objective-C
//カスタマイズメッセージを送信するためのサンプルコード
- (void)sendHello {
    // カスタマイズメッセージのコマンドワードであり、サービスに応じて一連のルールをカスタマイズする必要があります。ここではテキストブロードキャストメッセージの送信を意味する0x1を例示します。
    NSInteger cmdID = 0x1;
    NSData *data = [@"Hello" dataUsingEncoding:NSUTF8StringEncoding];
    // 現在のところ、reliable と ordered を一致させる必要があります。ここではメッセージの送信順の着信を保証する必要があることを例示します
    [trtcCloud sendCustomCmdMsg:cmdID data:data reliable:YES ordered:YES];
}
```

- **Java**

``` java
//カスタマイズメッセージを送信するためのサンプルコード
public void sendHello() {
    try {
        // カスタマイズメッセージのコマンドワードであり、サービスに応じて一連のルールをカスタマイズする必要があります。ここではテキストブロードキャストメッセージの送信を意味する0x1を例示します。
        int cmdID = 0x1;
        String hello = "Hello";
        byte[] data = hello.getBytes("UTF-8");
        // 現在のところ、reliable と ordered を一致させる必要があります。ここではメッセージの送信順の着信を保証する必要があることを例示します
        trtcCloud.sendCustomCmdMsg(cmdID, data, true, true);
				
    } catch (UnsupportedEncodingException e) {
        e.printStackTrace();
    }
}
```

- **C++**

``` C++
// カスタマイズメッセージを送信するためのサンプルコード
void sendHello()
{
    // カスタマイズメッセージのコマンドワードであり、サービスに応じて一連のルールをカスタマイズする必要があります。ここではテキストブロードキャストメッセージの送信を意味する0x1を例示します。

    uint32_t cmdID = 0x1;
    uint8_t* data = { '1', '2', '3' };
    uint32_t dataSize = 3;  // dataの長さ

    // 現在のところ、reliable と ordered を一致させる必要があります。ここではメッセージの送信順の着信を保証する必要があることを例示します
    trtcCloud->sendCustomCmdMsg(cmdID, data, dataSize, true, true);
}
```
- **C#**

```c#
// カスタマイズメッセージを送信するためのサンプルコード
private void sendHello()
{
    // カスタマイズメッセージのコマンドワードであり、サービスに応じて一連のルールをカスタマイズする必要があります。ここではテキストブロードキャストメッセージの送信を意味する0x1を例示します。

    uint cmdID = 0x1;
    byte[] data = { '1', '2', '3' };
    uint dataSize = 3;  // dataの長さ

    // 現在のところ、reliable と ordered を一致させる必要があります。ここではメッセージの送信順の着信を保証する必要があることを例示します
    mTRTCCloud.sendCustomCmdMsg(cmdID, data, dataSize, true, true);
}
```


## メッセージの受信

ルーム内の1人のユーザーが `sendCustomCmdMsg` を介してカスタムメッセージを送信した後、ルーム内の他のユーザーは SDK コールバックの `onRecvCustomCmdMsg` インターフェースを介してこれらのメッセージを受信することができます。

- **Objective-C**

``` Objective-C
//ルーム内の他のユーザーが送信したメッセージの受信および処理
- (void)onRecvCustomCmdMsgUserId:(NSString *)userId cmdID:(NSInteger)cmdId seq:(UInt32)seq message:(NSData *)message
{
	// userId が送信したメッセージの受信
    switch (cmdId)  // 送信者と受信者が承諾済みのcmdId
    {
    case 0:
        // cmdId = 0メッセージを処理
        break;
    case 1:
        // cmdId = 1メッセージを処理
        break;
    case 2:
        // cmdId = 2メッセージを処理
        break;
    default:
        break;
    }
}

```

- **Java**

``` java
//TRTCCloudListenerの継承、onRecvCustomCmdMsg メソッドの実装でルーム内の他のユーザーが送信したメッセージの受信および処理
public void onRecvCustomCmdMsg(String userId, int cmdId, int seq, byte[] message) {
	// userId が送信したメッセージを受信
    switch (cmdId)  // 送信者と受信者が承諾済みのcmdId
    {
    case 0:
        // cmdId = 0メッセージを処理
        break;
    case 1:
        // cmdId = 1メッセージを処理
        break;
    case 2:
        // cmdId = 2メッセージを処理
        break;
    default:
        break;
    
}
```

- **C++**

``` C++
// ルーム内の他のユーザーが送信したメッセージの受信および処理
void TRTCCloudCallbackImpl::onRecvCustomCmdMsg(
                            const char* userId, int32_t cmdId, uint32_t seq, const uint8_t* msg, uint32_t msgSize)
{
    // userId が送信したメッセージを受信
    switch (cmdId)  // 送信者と受信者が承諾済みのcmdId
    {
    case 0:
        // cmdId = 0メッセージを処理
        break;
    case 1:
        // cmdId = 1メッセージを処理
        break;
    case 2:
        // cmdId = 2メッセージを処理
        break;
    default:
        break;
    }
}
```

* **C#**

```c#
// ルーム内の他のユーザーが送信したメッセージの受信および処理
public void onRecvCustomCmdMsg(string userId, int cmdId, uint seq, byte[] msg, uint msgSize)
{
    // userId が送信したメッセージを受信
    switch (cmdId)  // 送信者と受信者が承諾済みのcmdId
    {
    case 0:
        // cmdId = 0メッセージを処理
        break;
    case 1:
        // cmdId = 1メッセージを処理
        break;
    case 2:
        // cmdId = 2メッセージを処理
        break;
    default:
        break;
    }
}
```

## 使用制限

カスタマイズメッセージは音声ビデオデータよりも送信優先度が高いため、カスタマイズデータの送信が多すぎると、音声ビデオデータが干渉を受け、画像がフリーズしたりぼやけたりする可能性があります。以上のことから、カスタマイズメッセージの送信について次の頻度制限を実施しています。

- カスタマイズメッセージはクラウドによってルーム内のすべてのユーザーにブロードキャストされるため、送信可能なメッセージは30通/秒を上限とします。
- 各メッセージパケット（ dataのサイズ）は 1 KBを上限とし、これを超える場合は、中間ルーターまたはサーバーによって破棄される可能性が極めて高くなります。
- 各クライアントが送信可能なデータは最大8 KB /秒とします。つまり、各データパケットがいずれも1KBであれば、最大8個のデータパケット/秒しか送信できません。








