このドキュメントでは、主に現在のTRTCからの自発的な退室方法を紹介し、どのような状況で強制的に退室するかについても紹介します：
![](https://qcloudimg.tencent-cloud.cn/raw/2de2f23672af65132b09d78d031d6c2d.png)

## 呼び出しガイド


[](id:step1)
### 手順1：事前手順の完了
[SDKのプロジェクトへのインポート](https://intl.cloud.tencent.com/document/product/647/35092)を参照して、SDKのインポートおよびApp権限の設定を完了します。
ドキュメント[入室](https://intl.cloud.tencent.com/document/product/647/47645)を参照して、入室プロセスを完了してください。

[](id:step2)
### 手順2：現在のルームからの自発的な退室
exitRoomインターフェースを呼び出すことで現在のルームから退室できます。SDKは、退室後にonExitRoom(int reason)コールバックイベントを介して通知します。
<dx-codeblock>
::: Android java
// 現在のルームから退室します
mCloud.exitRoom();
:::
::: iOS&Mac  swift
self.trtcCloud = [TRTCCloud sharedInstance];
// 現在のルームから退室します
[self.trtcCloud exitRoom];
:::
::: Windows  C++
trtc_cloud_ = getTRTCShareInstance();
// 現在のルームから退室します
trtc_cloud_->exitRoom();
:::
</dx-codeblock>

exitRoomインターフェースを呼び出すと、SDKは、退室プロセスに入ります。これには、2つの非常に重要なタスクがあります：
- **キータスク1：退室の公開**
ルーム内の他のユーザーに、現在のルームを離れようすることを通知します。ルーム内の他のユーザーは、ユーザーから**onRemoteUserLeaveRoom**コールバックを受け取ります。そうでない場合には、他のユーザーは当該ユーザーが「デッドロック」していると誤解する可能性があります。
- **キータスク2：デバイス権限のリリース**
ユーザーが退室する前にオーディオビデオストリームを公開している場合、退室プロセスでは、カメラとマイクをオフにしたり、デバイスの使用権をリリースしたりする必要もあります。

したがって、TRTCCloudインスタンスをリリースしたい場合は、onExitRoomコールバックを受信してからリリースすることをお勧めします。


[](id:step3)
### 手順3：現在のルームからの強制退出
ユーザーの自発的な退室を除いて、onExitRoom(int reason)コールバックを受け取る2つのケースがあります：
- **ケース1：現在のルームからの強制退室**
サービス側の[RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) | [RemoveUserByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39630)インターフェースを介して、特定のユーザーを特定のTRTCルームから強制退室させます。当該ユーザーを強制退室させると、当該ユーザーはonExitRoom(1)のコールバックを受け取ります。

- **ケース2：現在のルームが解散される**
サーバー側の[DismissRoom](https://intl.cloud.tencent.com/document/product/647/34269) | [DismissRoomByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39631)インターフェースを介して、特定のTRTCルームを解散できます。ルームを解散すると、ルーム内のすべてのユーザーはonExitRoom(2)のコールバックを受け取ります。


<dx-codeblock>
::: Android java
// onExitRoomコールバックを監視することで、退室の理由を確認できます
@Override
public void onExitRoom(int reason) {
    if (reason == 0) {
        Log.d(TAG, "Exit current room by calling the 'exitRoom' api of sdk ...");
    } else if (reason == 1) {
        Log.d(TAG, "Kicked out of the current room by server through the restful api...");
    } else if (reason == 2) {
        Log.d(TAG, "Current room is dissolved by server through the restful api...");
    }
}
:::
::: iOS&Mac  ObjC
// onExitRoomコールバックを監視することで、退室の理由を確認できます
- (void)onExitRoom:(NSInteger)reason {
    if (reason == 0) {
        NSLog(@"Exit current room by calling the 'exitRoom' api of sdk ...");
    } else if (reason == 1) {
        NSLog(@"Kicked out of the current room by server through the restful api...");
    } else if (reason == 2) {
        NSLog(@"Current room is dissolved by server through the restful api...");
    }
}
:::
::: Windows  C++
// onExitRoomコールバックを監視することで、退室の理由を確認できます
void onExitRoom(int reason) {
    if (reason == 0) {
        printf("Exit current room by calling the 'exitRoom' api of sdk ...");
    } else if (reason == 1) {
        printf("Kicked out of the current room by server through the restful api...");
    } else if (reason == 2) {
        printf("Current room is dissolved by server through the restful api...");
    }
}
:::
</dx-codeblock>
