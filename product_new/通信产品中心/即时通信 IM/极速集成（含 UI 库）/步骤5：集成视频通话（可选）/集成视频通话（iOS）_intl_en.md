The following figure illustrates the video call process:
![trtc demo](https://main.qcloudimg.com/raw/d097f4090d52a73c8ca6c82767b49b3d.png)

1. The IM SDK sends and receives custom communication protocol messages.
2. The custom messages are displayed through TUIKit.
3. When users meet the requirements for entering a video room, a video room is created through Tencent Real-Time Communication (TRTC), and then a video call or video conference begins.

## Step 1: Configure the Project File

1. Add the following to podfile.
 ```
pod 'TXLiteAVSDK_TRTC'
```
2. Run the following command to download third-party libraries to the current project.
```
pod install
```

## Step 2: Activate the TRTC Service
1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. Click **Activate Now** in the **Activate TRTC** area.
3. In the "Activate TRTC" dialog that appears, click **OK**.
 The system creates a TRTC account with the same SDKAppID as the current IM app in the [TRTC console](https://console.cloud.tencent.com/trtc). These accounts and their authentications can be reused.

## Step 3: Add a Video Chat Entry
<ol><li>In demo ChatViewController ViewDidLoad, add the following code before _chat.moreMenus = moreMenus to render the entry UI.
<pre style="padding-top: 24px; padding-bottom: 24px;">
<code>[moreMenus addObject:({
            TUIInputMoreCellData *data = [TUIInputMoreCellData new];
            data.image = [UIImage tk_imageNamed:@"more_video"];
            data.title = <span class="hljs-string">@"Video call"</span>;
            data:
        })];
</code></pre></li>
<li>Handle the button response event in the onSelectMoreCell callback.
<pre>
<code>- (void)chatController:(TUIChatController *)chatController onSelectMoreCell:(TUIInputMoreCell *)cell
{
    if ([cell.data.title isEqualToString:<span class="hljs-string">@"Video call"</span>]) {
        [[VideoCallManager shareInstance] setConversationData:self.conversationData];
        [[VideoCallManager shareInstance] videoCall:chatController];
    }
}
</code></pre></li></ol>


## Step 4: Add Communication Logic and Message Display
The Chat/VideoCall folder of the [demo](https://github.com/tencentyun/TIMSDK) contains audio and video communication protocols and code for rendering messages, which can be referenced directly. You can also define a set of audio and video communication protocols and message structures to perform actions such as initiating a video request, accepting or rejecting a user, and the timeout of offline users.

The example in this document references the audio and video communication protocols and code for rendering messages provided in the demo.

1. Copy the Chat/VideoCall folder in the demo to the current project.

```
typedef NS_ENUM(UInt32, videoCallState)
{
    //UserA initiates a call to UserB
		
    VIDEOCALL_REQUESTING = 0,         //Initiate a call request
    VIDEOCALL_USER_CANCEL,            //The initiator cancels the request, that is, [UserA cancels the video call request when UserB does not respond] (in which case, the display for UserA is "Video call is canceled", and the display for UserB is "You missed a video call").
    VIDEOCALL_USER_REJECT,            //The peer declines the call, that is, [UserB declines the call] (in which case, the display for UserA is "Video call is declined", and the display for UserB is "You missed a video call").
    VIDEOCALL_USER_NO_RESP,           //The peer did not respond, that is, [the system timed out waiting for UserB to respond] (in which case, the display for UserA is "Peer did not respond", and the display for UserB is "You missed a video call"). 
    VIDEOCALL_USER_CONNECTTING,       //The peer accepts the request and connects to the video call, that is, [UserB accepts the call] (in which case, UserA performs "enterRoom" and UserB performs "enterRoom").
    VIDEOCALL_USER_HANUGUP,           //A user hangs up, that is, [UserA or UserB hangs up] (in which case, the display for UserA is "Video call has ended", and the display for UserB is "Video call has ended").
    VIDEOCALL_USER_ONCALLING          //The peer is busy, that is [UserB is busy] (in which case, the display for UserA is "Peer is busy", and the display for UserB is "You missed a video call").
};

public class videoCallMessageData {
    int version = 2;                //Message identifier
    requestUser = "xxxx";           //Video call initiator
    roomID = 938283919212;          //Video room ID
    videoState = 5;                 //Video call status
    duration = 20;                  //Video call duration
}
```

2. Register **TUIKitNotification_TIMMessageListener** in **ConversationController** to monitor new messages and filter video call messages to process.

```
[[NSNotificationCenter defaultCenter] addObserver:self
    selector:@selector(onNewMessageNotification:) name:TUIKitNotification_TIMMessageListener object:nil];

- (void)onNewMessageNotification:(NSNotification *)no
{
    NSArray<TIMMessage *> *msgs = no.object;
    for (TIMMessage *msg in msgs) {
        
        TIMElem *elem = [msg getElem:0];
        if ([elem isKindOfClass:[TIMCustomElem class]]) {
            TIMCustomElem *custom = (TIMCustomElem *)elem;
            NSDictionary *param = [TCUtil jsonData2Dictionary:[custom data]];
            if (param != nil && [param[@"version"] integerValue] == 2) {
                [[VideoCallManager shareInstance] onNewVideoCallMessage:msg];
            }
        }
    }
}
```

3. Render custom messages.

```
- (TUIMessageCell *)chatController:(TUIChatController *)controller onShowMessageData:(TUIMessageCellData *)cellData {
    if ([data isKindOfClass:[VideoCallCellData class]]) {
        UInt32 state = [(VideoCallCellData *)data videoState];
        if (state == VIDEOCALL_REQUESTING || state == VIDEOCALL_USER_CONNECTTING) {
            return nil;
        } else {
            VideoCallCell *videoCallCell = [[VideoCallCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"VideoCell"];
            [videoCallCell fillWithData:(VideoCallCellData *)data];
            @weakify(self);
            @weakify(controller);
            [videoCallCell setVidelClick:^{
                @strongify(self);
                @strongify(controller);
                [[VideoCallManager shareInstance] setConversationData:self.conversationData];
                [[VideoCallManager shareInstance] videoCall:controller];
            }];
            return videoCallCell;
        }
    }
    return nil;
}
```

>If a custom message is not processed, it will not be rendered by default.

## Step 5: Enter the Video Room
 The Chat/Meeting folder in the [demo](https://github.com/tencentyun/TIMSDK) contains the logic for entering or quitting video rooms, which can be copied to the current project.

The following shows the sample code for entering a video room. For more information, see [TRTCParams Configuration](https://cloud.tencent.com/document/product/647/32261#trtcparams).

```
- (void)_enterMeetingRoom {
    // Set TRTC parameters
    TRTCParams *param = [[TRTCParams alloc] init];
    param.sdkAppId = sdkAppid;
    param.userId = [self currentUserIdentifier];                         //ID of the current user
    param.roomId = self.currentRoomID;                                   //The server can generate a unique ID. The demo uses a random ID as an example.
    param.userSig = [self genTestUserSig:[self currentUserIdentifier]];  //UserSig of the TRTC app
    param.privateMapKey = @"";

    [[TRTCCloud sharedInstance] setDelegate:self];
    [[TRTCCloud sharedInstance] enterRoom:param appScene:(TRTCAppSceneVideoCall)];
    [[TRTCCloud sharedInstance] startLocalPreview:YES view:self.localVideoView];
}
```
>`param.userSig` must be set as the UserSig of the current TRTC SDKAppID. If the TRTC SDKAppID and IM SDKAppID are the same, the UserSig can be reused. Otherwise, obtain the UserSig specific to the TRTC SDKAppID before authentication. For more information, see [How to Generate UserSig](https://cloud.tencent.com/document/product/647/17275).
 
The following shows the sample code for quitting a video room:

```
-(void)_quitMeetingRoom {
    [self setRoomStatus:TRTC_IDLE];
    [[TRTCCloud sharedInstance] stopLocalPreview];
    [[TRTCCloud sharedInstance] exitRoom];
}
```

For the complete logic for TRTC callbacks and setting rendering pages, see the Chat/Meeting/**VideoCallManager+videoMeeting.h** file in the [demo](https://github.com/tencentyun/TIMSDK).


## FAQs
**1. What should I do if I created the TRTC SDKAppID and IM SDKAppID separately and want to integrate both the IM SDK and TRTC SDK?**

 If you created the TRTC SDKAppID and IM SDKAppID separately, then you have two different SDKAppIDs, and the accounts and their authentications cannot be reused. In this case, you need to generate a UserSig for each SDKAppID for authentication. For more information on how to generate UserSig, see [How to Generate UserSig](https://cloud.tencent.com/document/product/647/17275).
