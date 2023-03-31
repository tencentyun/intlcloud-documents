## Feature Description
* The API for pulling historical messages is in the `V2TIMManager` and `V2TIMManager+Message (for iOS and macOS)` and `V2TIMMessageManager (Android and Windows)` classes.
* In addition to the support for pulling historical one-to-one and group messages, an advanced API is provided to pull messages by sequence, start point, or time range.
* Both local and cloud historical messages can be pulled.
  
> ? When historical messages are pulled from the cloud and a network exception is noticed, the SDK will return the locally stored historical messages.

Locally stored historical messages are not subject to time limits, but those stored in the cloud are subject to the following time limits:
* Free edition: The free storage period is 7 days and cannot be extended.
* Pro edition: The free storage period is 7 days and can be extended.
* Ultimate edition: The free storage period is 30 days and can be extended.

> ? 
> * It is a value-added service to extend the storage period of historical messages. You can log in to the [IM console](https://console.cloud.tencent.com/im) to modify relevant configuration. For information about billing, see [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). 
> * Rich media messages (such as images, files, and audios) have the same storage periods as historical messages.

[](id:c2c)
## Pulling Historical One-to-One Messages

Call the `getC2CHistoryMessageList` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#afedccbe0e5229ae15e0e07b722ea39df) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#abca63ad64f69aa4f424cf11849a9b89e)) to get historical one-to-one messages.
When the network is normal, the latest cloud data will be pulled; when it is abnormal, the SDK will return the locally stored historical messages.

If you want to pull only local historical messages, see [Advanced API](#advance).
This API supports pulling by page. For more information, see [Pulling by page](#advance_page).

Sample code:
<dx-tabs>
::: Android
```java
// Pull historical one-to-one messages
// Set `lastMsg` to `null` for the first pull
// `lastMsg` can be the last message in the returned message list for the second pull.
V2TIMManager.getMessageManager().getC2CHistoryMessageList(#your user id#, 20, null, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "fail, " + code + ", " + desc);
    }

    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        // Record the `lastMsg` for the next pull
        V2TIMMessage lastMsg = v2TIMMessages.get(v2TIMMessages.size() - 1);
        Log.i("imsdk", "success");
    }
});
```
:::
::: iOS and macOS
```objectivec
// Pull historical one-to-one messages
// Set `lastMsg` to `nil` for the first pull
// `lastMsg` can be the last message in the returned message list for the second pull.
[V2TIMManager.sharedInstance getC2CHistoryMessageList:#your user id# count:20 lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    // Record the `lastMsg` for the next pull
    V2TIMMessage *lastMsg = msgs.lastObject;
    NSLog(@"success, %@", msgs);
} fail:^(int code, NSString *desc) {
    NSLog(@"fail, %d, %@", code, desc);
}];
```
:::
</dx-tabs>


[](id:group)
## Pulling Historical Group Messages

Call the `getGroupHistoryMessageList` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) to get historical group messages.
When the network is normal, the latest cloud data will be pulled; when it is abnormal, the SDK will return the locally stored historical messages.

If you want to pull only local historical messages, see [Advanced API](#advance).
This API supports pulling by page. For more information, see [Pulling by page](#advance_page).

> ! 
> * Only the historical messages of meeting groups (Meeting) can be pulled. For more information on group message limits, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).
> * This API does not apply to audio-video groups (AVChatRoom), as their messages are not stored on the cloud roaming server or in the local database. If you use the Ultimate edition, you can configure **Message History for New Members** in the [IM console](https://console.cloud.tencent.com/im) to get historical messages in the `onRecvNewMessage` callback after successfully joining the audio-video group. New members of an audio-video group can view up to 20 messages in the past 24 hours before they join the group. For console configuration details, see [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

Sample code:
<dx-tabs>
::: Android
```java
// Pull historical group messages
// Set `lastMsg` to `null` for the first pull
// `lastMsg` can be the last message in the returned message list for the second pull.
V2TIMManager.getMessageManager().getGroupHistoryMessageList(#your group id#, 20, null, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "fail, " + code + ", " + desc);
    }

    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        // Record the `lastMsg` for the next pull
        V2TIMMessage lastMsg = v2TIMMessages.get(v2TIMMessages.size() - 1);
        Log.i("imsdk", "success");
    }
});
```
:::
::: iOS and macOS
```objectivec
// Pull historical group messages
// Set `lastMsg` to `null` for the first pull
// `lastMsg` can be the last message in the returned message list for the second pull.
[V2TIMManager.sharedInstance getGroupHistoryMessageList:#your group id# count:20 lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    // Record the `lastMsg` for the next pull
    V2TIMMessage *lastMsg = msgs.lastObject;
    NSLog(@"success, %@", msgs);
} fail:^(int code, NSString *desc) {
    NSLog(@"fail, %d, %@", code, desc);
}];
```
:::
</dx-tabs>

## Advanced Features

[](id:advance)
### Advanced API

If the ordinary API above cannot meet your needs to pull historical messages, you can use the advanced API `getHistoryMessageList` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a99e8f00ee60df12e346548b743523218) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a4bbdbdd063d5dad2d164059e1f5d7851)).

In addition to pulling historical one-to-one and group messages, this API supports the following advanced features:
* Set the start point for message pull
* Set the time range for message pull
* Set the source for message pull: pull from the local database or the cloud
* Specify the sequence for message pull: pull in reverse chronological order or in chronological order
* Specify the message type for local pull: text, image, audio, video, file, emoji, group tip, merged, or custom message

API prototype:
<dx-tabs>
::: Android
```java
public abstract void getHistoryMessageList(V2TIMMessageListGetOption option, V2TIMValueCallback<List<V2TIMMessage>> callback);
```
:::
::: iOS and macOS
```objectivec
- (void)getHistoryMessageList:(V2TIMMessageListGetOption *)option
                         succ:(V2TIMMessageListSucc)succ
                         fail:(V2TIMFail)fail;
```
:::
::: Windows
```cpp
virtual void GetHistoryMessageList(const V2TIMMessageListGetOption& option,
                                   V2TIMValueCallback<V2TIMMessageVector>* callback) = 0;
```
:::
</dx-tabs>

The parameters of the `V2TIMMessageListGetOption`class are as described below:

| Parameter       | Description                                                  | Valid for One-to-One Chat   | Valid for Group Chat        | Required | Remarks                                                      |
| --------------- | ------------------------------------------------------------ | --------------------------- | --------------------------- | -------- | ------------------------------------------------------------ |
| getType         | Source and sequence of the message pull, which can be set to **local/cloud** and **reverse chronological order/chronological order** respectively. | YES                         | YES                         | YES      | When the pull source is set to the cloud, the local message list and cloud message list will be merged and returned. If there is no network connection, the local message list will be returned. |
| userID          | The specified user ID with which to pull historical one-to-one messages | YES                         | <font color="red">NO</font> | NO       | To pull one-to-one messages with a certain user, you need to specify only the `userID`. |
| groupID         | The specified group ID with which to pull historical group messages | <font color="red">NO</font> | YES                         | NO       | To pull group messages from a certain group, you need to specify only the `groupID`. |
| count           | Number of messages per pull                                  | YES                         | YES                         | YES      | We recommend you set it to `20`; otherwise, the pull speed may be affected. |
| messageTypeList | Pulled message type set                                      | YES                         | YES                         | NO       | 1. It is supported only for local pull, that is, it is valid only when `getType` is `V2TIM_GET_LOCAL_OLDER_MSG` or `V2TIM_GET_LOCAL_NEWER_MSG`.<br/>2. If this field is left empty, messages of all types will be pulled.<br/>3. For more information on the supported message types, see `V2TIMElemType` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#a00455865d1a14191b8c612252bf20a1c) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a849af0e4698e8db9f227f9c8e54215b8) / [Windows](https://im.sdk.qcloud.com/doc/en/V2TIMMessage_8h.html#a6854ecfbc6f3b65ed381d8a2e14e2377)). |
| lastMsg         | Last message                                                 | YES                         | YES                         | NO       | This parameter applies to historical message pull.<br/>1. It can be used for both one-to-one and group chats.<br/>2. If it is set as the start point for the message pull, the message will **not be included** in the returned message list.<br/>3. If it is left empty, the latest message in the conversation will be used as the start point for pull. |
| lastMsgSeq      | `seq` of the last message                                    | <font color="red">NO</font> | YES                         | NO       | This parameter applies to historical message pull or locating.<br/>1. It can be used only for group chats.<br/>2. If it is set as the start point for the message pull, the message will be **included** in the returned message list.<br/>3. If both `lastMsg` and `lastMsgSeq` are specified, the SDK will use `lastMsg`.<br/>4. If neither `lastMsg` nor `lastMsgSeq` is specified, the start point for pull will be determined based on whether the `getTimeBegin` is set. If yes, the set range will be used as the start point; if no, the latest message will be used as the start point. |
| getTimeBegin    | Start time for the message pull. It is a UTC timestamp in seconds. | YES                         | YES                         | NO       | It defaults to `0`, indicating to pull messages from the current time. |
| getTimePeriod   | Time range for the message pull in seconds.                  | YES                         | YES                         | NO       | 1. It defaults to `0`, indicating that there is no time range limit.<br/>2. It is a closed range including the start and end time:<br/>* If `getType` specifies the reverse chronological order, the time range is [getTimeBegin - getTimePeriod, getTimeBegin].<br/>* If `getType` specifies the chronological order, the time range is [getTimeBegin, getTimeBegin + getTimePeriod]. |


[](id:advance_page)
### Pulling by page

Historical one-to-one message pull, historical group message pull, and pull via the advanced API can all be paged by using `lastMsg` and `count`:
1. For the first pull, leave `lastMsg` empty. In this case, the SDK will pull the latest message.
2. If it is not the first pull, use the last message in the message list from the last pull as the `lastMsg`. In this case, the `lastMsg` will not be included in the returned message list.
3. The pulled message list displays messages from the most recent to the oldest.

> ? We recommend you set `count` to `20` to enhance the loading efficiency and save network traffic.

If you use `lastMsgSeq` to pull historical messages, the message corresponding to `lastMsgSeq` will be **included** in the returned message list.
Therefore, we recommend you not use `lastMsgSeq` if you are not pulling historical group messages for the first time (subsequent pull); otherwise, the same message may be pulled repeatedly.
For example, there are eight historical messages: `msg1`, `msg2`, `msg3`, `msg4`, `msg5`, `msg6`, `msg7`, and `msg8`.
If four messages are pulled each time, you will get `msg1`, `msg2`, `msg3`, and `msg4` for the first pull. If you use the `lastMsgSeq` of `msg4` to start another pull, `msg4`, `msg5`, `msg6`, and `msg7` will be pulled. In this case, `msg4` is pulled twice.
If you need to use `lastMsgSeq` for subsequent pulls, we recommend you set the logic of message deduplication.


[](id:advance_timerange)
### Pulling by time range

You can set `getTimeBegin` and `getTimePeriod` to specify the time range for the message pull.
The start and end timestamps of the time range are related to `getType`, as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/a7e863b901fad1ab9edabca872677d55.jpeg)

The following sample code demonstrates the process of pulling cloud group messages of the whole day from 2022-01-01 00:00:00 (the timestamp is `1640966400`) in reverse chronological order.
<dx-tabs>
::: Android
```java
V2TIMMessageListGetOption option = new V2TIMMessageListGetOption();
option.setGetType(V2TIMMessageListGetOption.V2TIM_GET_CLOUD_OLDER_MSG); // Pull older cloud messages
option.setGetTimeBegin(1640966400);         // Start from 2022-01-01 00:00:00
option.setGetTimePeriod(1 * 24 * 60 * 60);  // Pull the messages of the whole day
option.setCount(Integer.MAX_VALUE);         // Return all the messages within the time range
option.setGroupID(#you group id#);          // Pull group messages
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
::: iOS and macOS
```objectivec
V2TIMMessageListGetOption *option = [[V2TIMMessageListGetOption alloc] init];
option.getType = V2TIM_GET_CLOUD_OLDER_MSG; // Pull cloud messages in reverse chronological order
option.getTimeBegin = 1640966400;        // Start from 2022-01-01 00:00:00
option.getTimePeriod = 1 * 24 * 60 * 60; // Pull the messages of the whole day
option.count = INT_MAX;                  // Return all the messages within the time range
option.groupID = #your group id#;        // Pull group messages
[V2TIMManager.sharedInstance getHistoryMessageList:option succ:^(NSArray<V2TIMMessage *> *msgs) {
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];
```
:::
::: Windows
```cpp
template <class T>
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T& value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMMessageListGetOption option;
option.getType = V2TIMMessageGetType::V2TIM_GET_CLOUD_OLDER_MSG;  // Pull older cloud messages
option.getTimeBegin = 1640966400;        // Start from 2022-01-01 00:00:00
option.getTimePeriod = 1 * 24 * 60 * 60;                          // Pull the messages of the whole day
option.count = std::numeric_limits<uint64_t>::max();              // Return all the messages within the time range
option.groupID = "your group id";                                 // Pull group messages

auto callback = new ValueCallback<V2TIMMessageVector>{};
callback->SetCallback(
    [=](const V2TIMMessageVector& messageList) {
        std::cout << "success" << std::endl;
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        std::cout << "error" << std::endl;
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->GetHistoryMessageList(option, callback);
```
:::
</dx-tabs>


[](id:advance_timerange_page)
### Pulling by page within the time range

You can specify both the time range and `lastMsg`/`lastMsgSeq` for the message pull at the same time. And the SDK will respond as follows:
1. If both `getTimeBegin`/`getTimePeriod` and `lastMsg`/`lastMsgSeq` are set, the overlapping part of the messages pulled based on the start message and the messages pulled based on the time range will be returned.
2. If neither `getTimeBegin`/`getTimePeriod` nor `lastMsg`/`lastMsgSeq` is set, messages will be pulled from the latest message based on the sequence and method specified by `getType`.

The following sample code demonstrates the process of pulling cloud group messages by page (20 messages per page) from 2022-01-01 00:00:00 (the timestamp is `1640966400`) in reverse chronological order.
<dx-tabs>
::: Android
```java
// Define a variable to record the cursor of each pull
private V2TIMMessage m_lastMsg = null;  // It is `null` for the first pull.

// Logic of pulling by page
V2TIMMessageListGetOption option = new V2TIMMessageListGetOption();
option.setGetType(V2TIMMessageListGetOption.V2TIM_GET_CLOUD_OLDER_MSG); // Pull older cloud messages
option.setGetTimeBegin(1640966400);         // Start from 2022-01-01 00:00:00
option.setGetTimePeriod(1 * 24 * 60 * 60);  // Pull the messages of the whole day
option.setCount(20);                        // 20 messages per page
option.setLastMsg(m_lastMsg);               // Position of the last pull (the last message in the returned message list each time)
option.setGroupID(#you group id#);          // Pull group messages
V2TIMManager.getMessageManager().getHistoryMessageList(option, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        Log.i("imsdk", "success");
        // Record the `lastMsg` for the next pull
        m_lastMsg = v2TIMMessages.get(v2TIMMessages.size() - 1);
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
// Define a variable to record the cursor of each pull
@property (nonatomic, copy) V2TIMMessage *lastMsg;

// Logic of pulling by page
V2TIMMessageListGetOption *option = [[V2TIMMessageListGetOption alloc] init];
option.getType = V2TIM_GET_CLOUD_OLDER_MSG; // Pull cloud messages in reverse chronological order
option.getTimeBegin = 1640966400;        // Start from 2022-01-01 00:00:00
option.getTimePeriod = 1 * 24 * 60 * 60; // Pull the messages of the whole day
option.count = 20;                       // 20 messages per page
option.lastMsg = self.lastMsg;           // Position of the last pull (the last message in the returned message list each time)
option.groupID = #your group id#;        // Pull group messages
__weak typeof(self) weakSelf = self;
[V2TIMManager.sharedInstance getHistoryMessageList:option succ:^(NSArray<V2TIMMessage *> *msgs) {
    NSLog(@"success");
    // Record the `lastMsg` for the next pull
    weakSelf.lastMsg = msgs.lastObject;
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];
```
:::
::: Windows
```cpp
template <class T>
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T& value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

// Define a variable to record the cursor of each pull
V2TIMMessage lastMsg;

// Logic of pulling by page
V2TIMMessageListGetOption option;
option.getType = V2TIMMessageGetType::V2TIM_GET_CLOUD_OLDER_MSG;  // Pull older cloud messages
option.getTimeBegin = 1640966400;        // Start from 2022-01-01 00:00:00
option.getTimePeriod = 1 * 24 * 60 * 60;                          // Pull the messages of the whole day
option.count = 20;                                                // 20 messages per page
option.lastMsg = First pull? nullptr : &lastMsg;  // Position of the last pull (the last message in the returned message list each time)
option.groupID = "your group id";  // Pull group messages

auto callback = new ValueCallback<V2TIMMessageVector>{};
callback->SetCallback(
    [=](const V2TIMMessageVector& messageList) mutable {
        std::cout << "success" << std::endl;
        // Record the `lastMsg` for the next pull
        lastMsg = messageList[messageList.Size() - 1];
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        std::cout << "error" << std::endl;
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->GetHistoryMessageList(option, callback);
```
:::
</dx-tabs>


[](id:advance_local)
### Pulling only local messages

Set `getType` to pull only local messages:

* When `getType` is set to `V2TIM_GET_LOCAL_OLDER_MSG`, locally stored messages will be pulled in reverse chronological order.
* When `getType` is set to `V2TIM_GET_LOCAL_NEWER_MSG`, locally stored messages will be pulled in chronological order.

The following sample code demonstrates the process of pulling 20 one-to-one messages from the local database in reverse chronological order, starting from the latest message:
<dx-tabs>
::: Android
```java
V2TIMMessageListGetOption option = new V2TIMMessageListGetOption();
option.setGetType(V2TIMMessageListGetOption.V2TIM_GET_LOCAL_OLDER_MSG); // Pull local messages in reverse chronological order
option.setLastMsg(null);            // Set to pull from the latest message
option.setCount(20);                // Pull 20 messages
option.setUserID(#you user id#);    // Pull one-to-one messages
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
::: iOS and macOS
```objectivec
V2TIMMessageListGetOption *option = [[V2TIMMessageListGetOption alloc] init];
option.getType = V2TIM_GET_LOCAL_OLDER_MSG; // Pull local messages in reverse chronological order
option.lastMsg = nil;            // Set to pull from the latest message
option.count = 20;               // Pull 20 messages
option.userID = #your user id#;  // Pull one-to-one messages
[V2TIMManager.sharedInstance getHistoryMessageList:option succ:^(NSArray<V2TIMMessage *> *msgs) {
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];
```
:::
::: Windows
```cpp
template <class T>
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T& value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMMessageListGetOption option;
option.getType = V2TIMMessageGetType::V2TIM_GET_LOCAL_OLDER_MSG;  // Pull older local messages
option.count = 20;                                                // Pull 20 messages
option.userID = "you user id";                                    // Pull one-to-one messages

auto callback = new ValueCallback<V2TIMMessageVector>{};
callback->SetCallback(
    [=](const V2TIMMessageVector& messageList) mutable {
        std::cout << "success" << std::endl;
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        std::cout << "error" << std::endl;
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->GetHistoryMessageList(option, callback);
```
:::
</dx-tabs>


[](id:advance_messagetype)
### Pulling messages of a specified type

The SDK defines common message types, such as text, image, and video messages. For more information, see `V2TIMElemType` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#a00455865d1a14191b8c612252bf20a1c) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a849af0e4698e8db9f227f9c8e54215b8) / [Windows](https://im.sdk.qcloud.com/doc/en/V2TIMMessage_8h.html#a6854ecfbc6f3b65ed381d8a2e14e2377)). The advanced API `getHistoryMessageList` allows setting `messageTypeList` to specify the message type for pull.

> !
> 1. When `messageTypeList` is left empty, messages of all types will be pulled.
> 2. The message type can be specified only for the local pull but not for the cloud pull.


The following sample code demonstrates the process of pulling 20 text and image messages in reverse chronological order, starting from the current time:
<dx-tabs>
::: Android
```java
// Pull image and text messages
ArrayList<Integer> messageTypeList = new ArrayList<Integer>();
messageTypeList.add(V2TIM_ELEM_TYPE_IMAGE);
messageTypeList.add(V2TIM_ELEM_TYPE_TEXT);

V2TIMMessageListGetOption option = new V2TIMMessageListGetOption();
option.setGetType(V2TIMMessageListGetOption.V2TIM_GET_CLOUD_OLDER_MSG); // Pull older cloud messages
option.setCount(20);
option.setMessageTypeList(messageTypeList);
option.setGroupID("you group id");
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
::: iOS and macOS
```objectivec
V2TIMMessageListGetOption *option = [[V2TIMMessageListGetOption alloc] init];
option.getType = V2TIM_GET_CLOUD_OLDER_MSG;
// Pull image and text messages
option.messageTypeList = @[@(V2TIM_ELEM_TYPE_IMAGE), @(V2TIM_ELEM_TYPE_TEXT)];
option.count = 20;
option.groupID = @"your group id";
[V2TIMManager.sharedInstance getHistoryMessageList:option succ:^(NSArray<V2TIMMessage *> *msgs) {
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];
```
:::
::: Windows
```cpp
template <class T>
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T& value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMMessageListGetOption option;
option.getType = V2TIMMessageGetType::V2TIM_GET_CLOUD_OLDER_MSG;  // Pull older cloud messages
option.count = 20;                                                // Pull 20 messages
option.messageTypeList.PushBack(V2TIMElemType::V2TIM_ELEM_TYPE_IMAGE);  // Pull image messages
option.messageTypeList.PushBack(V2TIMElemType::V2TIM_ELEM_TYPE_TEXT);   // Pull text messages
option.userID = "you group id";                                         // Pull group messages

auto callback = new ValueCallback<V2TIMMessageVector>{};
callback->SetCallback(
    [=](const V2TIMMessageVector& messageList) mutable {
        std::cout << "success" << std::endl;
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        std::cout << "error" << std::endl;
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->GetHistoryMessageList(option, callback);
```
:::
</dx-tabs>


[](id:advance_group_at)
### Quick redirection to a group @ message

After a user receives a group @ message in a group conversation, the user generally needs to click the @ bar to go to the message and pull the neighboring messages for display.
As the group @ message also needs to be displayed, you can set its `sequence` as the `lastMsgSeq` and use the advanced API `getHistoryMessageList` to pull messages.

The following sample code demonstrates the process of clicking the @ bar, redirecting to the group @ message, and pulling the first 20 messages earlier and later than that message for display:

<dx-tabs>
::: Android
```java
// Get the `sequence` of the group @ message
long atSequence = 1081;

// Pull the group @ message and earlier messages
V2TIMMessageListGetOption beforeOption = new V2TIMMessageListGetOption();
beforeOption.setGetType(V2TIMMessageListGetOption.V2TIM_GET_CLOUD_OLDER_MSG); // Pull messages earlier than the group @ message
beforeOption.setCount(20);                        // Pull 20 messages
beforeOption.setLastMsgSeq(atSequence);           // Start the pull from the group @ message, which is included in the pull list
beforeOption.setGroupID(#you group id#);          // Pull group messages
V2TIMManager.getMessageManager().getHistoryMessageList(beforeOption, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        // The group @ message is included in the returned message list.
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});

// Pull messages later than the group @ message
V2TIMMessageListGetOption afterOption = new V2TIMMessageListGetOption();
afterOption.setGetType(V2TIMMessageListGetOption.V2TIM_GET_CLOUD_NEWER_MSG); // Pull messages later than the group @ message
afterOption.setCount(20);                        // Pull 20 messages
afterOption.setLastMsgSeq(atSequence + 1);       // Start the pull from the first message later than the group @ message, which is not included in the pull list
afterOption.setGroupID(#you group id#);          // Pull group messages
V2TIMManager.getMessageManager().getHistoryMessageList(afterOption, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        // The group @ message is not included in the returned message list.
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
// Get the `sequence` of the group @ message
NSInteger atSequence = 1081;

// Pull the group @ message and earlier messages
V2TIMMessageListGetOption *beforeOption = [[V2TIMMessageListGetOption alloc] init];
beforeOption.getType = V2TIM_GET_CLOUD_OLDER_MSG; // Pull messages earlier than the group @ message
beforeOption.count = 20;                          // Pull 20 messages
beforeOption.lastMsgSeq = atSequence;             // Start the pull from the group @ message, which is included in the pull list
beforeOption.groupID = #your group id#;           // Pull group messages
[V2TIMManager.sharedInstance getHistoryMessageList:beforeOption succ:^(NSArray<V2TIMMessage *> *msgs) {
    // The group @ message is included in the returned message list.
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];

// Pull messages later than the group @ message
V2TIMMessageListGetOption *afterOption = [[V2TIMMessageListGetOption alloc] init];
afterOption.getType = V2TIM_GET_CLOUD_NEWER_MSG; // Pull messages later than the group @ message
afterOption.count = 20;                          // Pull 20 messages
afterOption.lastMsgSeq = atSequence + 1;         // Start the pull from the first message later than the group @ message, which is not included in the pull list
afterOption.groupID = #your group id#;           // Pull group messages
[V2TIMManager.sharedInstance getHistoryMessageList:afterOption succ:^(NSArray<V2TIMMessage *> *msgs) {
    // The group @ message is not included in the returned message list.
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];
```
:::
::: Windows
```cpp
template <class T>
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T& value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

// Get the `sequence` of the group @ message
uint64_t atSequence = 1081;

// Pull the group @ message and earlier messages
V2TIMMessageListGetOption beforeOption;
beforeOption.getType = V2TIMMessageGetType::V2TIM_GET_CLOUD_OLDER_MSG;  // Pull messages earlier than the group @ message
beforeOption.count = 20;                                                // Pull 20 messages
beforeOption.lastMsgSeq = atSequence;             // Start the pull from the group @ message, which is included in the pull list
beforeOption.userID = "you group id";  // Pull group messages

auto beforeCallback = new ValueCallback<V2TIMMessageVector>{};
beforeCallback->SetCallback(
    [=](const V2TIMMessageVector& messageList) mutable {
        // The group @ message is included in the returned message list.
        std::cout << "success" << std::endl;
        delete beforeCallback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        std::cout << "error" << std::endl;
        delete beforeCallback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->GetHistoryMessageList(beforeOption, beforeCallback);

// Pull the group @ message and earlier messages
V2TIMMessageListGetOption afterOption;
afterOption.getType = V2TIMMessageGetType::V2TIM_GET_CLOUD_NEWER_MSG;  // Pull messages later than the group @ message
afterOption.count = 20;                                                 // Pull 20 messages
afterOption.lastMsgSeq = atSequence + 1;         // Start the pull from the first message later than the group @ message, which is not included in the pull list
afterOption.userID = "you group id";       // Pull group messages

auto afterCallback = new ValueCallback<V2TIMMessageVector>{};
afterCallback->SetCallback(
    [=](const V2TIMMessageVector& messageList) mutable {
        // The group @ message is not included in the returned message list.
        std::cout << "success" << std::endl;
        delete afterCallback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        std::cout << "error" << std::endl;
        delete afterCallback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->GetHistoryMessageList(afterOption, afterCallback);
```
:::
</dx-tabs>


[](id:advance_assign_message)
### Message locating for searches

When a user gets the `V2TIMMessage` object after the local search and clicks the message, you need to redirect the user to the position of the message and display neighboring messages.
At this point, you can set `lastMsg` to the message object and use the advanced API `getHistoryMessageList` to pull neighboring messages.

The following sample code demonstrates the process of pulling the first 20 messages earlier and later than the located message for display.

<dx-tabs>
::: Android
```java
// Get the current message object
V2TIMMessage lastMsg = #The located message#;

// Pull messages earlier than the specified message
V2TIMMessageListGetOption beforeOption = new V2TIMMessageListGetOption();
beforeOption.setGetType(V2TIMMessageListGetOption.V2TIM_GET_CLOUD_OLDER_MSG); // Pull messages earlier than the specified message
beforeOption.setCount(20);                        // Pull 20 messages
beforeOption.setLastMsg(lastMsg);                 // Start the pull from the specified message, which is not included in the pull list
beforeOption.setGroupID(#you group id#);          // Pull group messages
V2TIMManager.getMessageManager().getHistoryMessageList(beforeOption, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        // `lastMsg` is not included in the returned message list.
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});

// Pull messages later than the specified message
V2TIMMessageListGetOption afterOption = new V2TIMMessageListGetOption();
afterOption.setGetType(V2TIMMessageListGetOption.V2TIM_GET_CLOUD_NEWER_MSG); // Pull messages later than the specified message
afterOption.setCount(20);                        // Pull 20 messages
afterOption.setLastMsg(lastMsg);                 // Start the pull from the specified message, which is not included in the pull list
afterOption.setGroupID(#you group id#);          // Pull group messages
V2TIMManager.getMessageManager().getHistoryMessageList(afterOption, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        // `lastMsg` is not included in the returned message list.
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
// Get the current message object
V2TIMMessage *lastMsg = #The located message#;

// Pull messages earlier than the specified message
V2TIMMessageListGetOption *beforeOption = [[V2TIMMessageListGetOption alloc] init];
beforeOption.getType = V2TIM_GET_CLOUD_OLDER_MSG; // Pull messages earlier than the specified message
beforeOption.count = 20;                          // Pull 20 messages
beforeOption.lastMsg = lastMsg;                   // Start the pull from the specified message, which is not included in the pull list
beforeOption.groupID = #your group id#;           // Pull group messages
[V2TIMManager.sharedInstance getHistoryMessageList:beforeOption succ:^(NSArray<V2TIMMessage *> *msgs) {
    // The specified message is not included in the returned message list.
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];

// Pull messages later than the specified message
V2TIMMessageListGetOption *afterOption = [[V2TIMMessageListGetOption alloc] init];
afterOption.getType = V2TIM_GET_CLOUD_NEWER_MSG; // Pull messages later than the specified message
afterOption.count = 20;                          // Pull 20 messages
afterOption.lastMsg = lastMsg;                   // Start the pull from the specified message, which is not included in the pull list
afterOption.groupID = #your group id#;           // Pull group messages
[V2TIMManager.sharedInstance getHistoryMessageList:afterOption succ:^(NSArray<V2TIMMessage *> *msgs) {
    // The specified message is not included in the returned message list.
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];
```
:::
::: Windows
```cpp
template <class T>
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T& value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

// Get the current message object
V2TIMMessage lastMsg = The located message;

// Pull messages earlier than the specified message
V2TIMMessageListGetOption beforeOption;
beforeOption.getType = V2TIMMessageGetType::V2TIM_GET_CLOUD_OLDER_MSG;  // Pull messages earlier than the specified message
beforeOption.count = 20;                                                // Pull 20 messages
beforeOption.lastMsg = lastMsg;                   // Start the pull from the specified message, which is not included in the pull list
beforeOption.userID = "you group id";  // Pull group messages

auto beforeCallback = new ValueCallback<V2TIMMessageVector>{};
beforeCallback->SetCallback(
    [=](const V2TIMMessageVector& messageList) mutable {
        // `lastMsg` is not included in the returned message list.
        std::cout << "success" << std::endl;
        delete beforeCallback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        std::cout << "error" << std::endl;
        delete beforeCallback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->GetHistoryMessageList(beforeOption, beforeCallback);

// Pull messages later than the specified message
V2TIMMessageListGetOption afterOption;
afterOption.getType = V2TIMMessageGetType::V2TIM_GET_CLOUD_NEWER_MSG;  // Pull messages later than the specified message
afterOption.count = 20;                                                 // Pull 20 messages
afterOption.lastMsg = lastMsg;                   // Start the pull from the specified message, which is not included in the pull list
afterOption.userID = "you group id";       // Pull group messages

auto afterCallback = new ValueCallback<V2TIMMessageVector>{};
afterCallback->SetCallback(
    [=](const V2TIMMessageVector& messageList) mutable {
        // `lastMsg` is not included in the returned message list.
        std::cout << "success" << std::endl;
        delete afterCallback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        std::cout << "error" << std::endl;
        delete afterCallback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->GetHistoryMessageList(afterOption, afterCallback);
```
:::
</dx-tabs>

[](id:advance_parse_signaling)
### Parsing a signaling message
If you use the IM SDK's signaling API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html)), when you call `invite/inviteInGroup` and set `onlineUserOnly ` to `false` (Android) / `NO` (iOS), a custom message will be generated for each signaling operation (including `invite`, `cancel`, `accept`, `reject`, and `timeout`). The message will be delivered to the user in the `onRecvNewMessage` callback of `V2TIMAdvancedMsgListener` and can also be pulled from historical messages.

If you want to customize the display text based on the signaling information, you can use the signaling parsing API `getSignalingInfo` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ab303f20f53de134e6f6ebe5f9f9bcad0) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a0b149836793b8f2d54889b1c3ae40362) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMSignalingManager.html#afc6d9c1e14e05f87e7ea108711095cb8)) to get the signaling information.

**API prototype**

<dx-tabs>
::: Android
```java
/**
 * Get the signaling information
 *
 * If `onlineUserOnly` is set to `false` in the `invite` operation, a custom message is generated for each signaling operation (including the `invite`, `cancel`, `accept`, `reject`, and `timeout` operations).
 The message will be delivered to users via `V2TIMAdvancedMsgListener` -> `onRecvNewMessage` and can be pulled by users via historical message pulling. If you want to customize the display text based on the signaling information, call the following API to get the signaling information.
 *
 * @param msg // Message object
 * @return V2TIMSignalingInfo //Signaling information. If the value is null, `msg` is not a signaling message.
 */
public abstract V2TIMSignalingInfo getSignalingInfo(V2TIMMessage msg);
```
:::
::: iOS and macOS
```objectivec
/**
 * Get the signaling information
 *
 * If `onlineUserOnly` is set to `NO` in the `invite` operation, a custom message will be generated for each signaling operation (including `invite`, `cancel`, `accept`, `reject`, and `timeout`). The message will be delivered to the user via `V2TIMAdvancedMsgListener` > `onRecvNewMessage` and can be pulled from historical messages. To customize the display text based on the signaling information, call the following API to get the signaling information.
 *
 *  @param msg // Message object
 *  @return V2TIMSignalingInfo //Signaling information. If the value is nil, `msg` is not a signaling message.
 */
- (V2TIMSignalingInfo *)getSignallingInfo:(V2TIMMessage *)msg;
```
:::
::: Windows
```cpp
/**
 * Get the signaling information
 *
 * If `onlineUserOnly` is set to `false` in the `invite` operation,
 * a custom message is generated for each signaling operation (including the `Invite`, `Cancel`, `Accept`, `Reject`, and `Timeout` operations). The message will be delivered to the user via
 * `V2TIMAdvancedMsgListener` -> `onRecvNewMessage`
 * and can be pulled from historical messages. To customize the display text based on the signaling information, call the following API to get the signaling information.
 *
 * @param msg // Message object
 * @return V2TIMSignalingInfo //Signaling information. If `V2TIMSignalingInfo::inviteID` is an empty string, `msg` is not a signaling message.
 */
virtual V2TIMSignalingInfo GetSignalingInfo(const V2TIMMessage& msg) = 0;
```
:::
</dx-tabs>

The following sample code demonstrates the process of pulling historical messages and parsing the display text of the signaling message.
<dx-tabs>
::: Android
```java
/// Custom text of the signaling message
public String getCallSignalingContentWithMessage(V2TIMMessage message) {
    if (message == null) {
        Log.e(TAG, " invalid param ");
        return "";
    }

    V2TIMSignalingInfo signalingInfo = V2TIMManager.getSignalingManager().getSignalingInfo(message);
    if (signalingInfo == null) {
        Log.e(TAG, " signalingInfo is null ");
        return "";
    }

    String content = "";
    Gson gson = new Gson();
    Object businessIdObj = null;
    String businessId = null;
    try {
        HashMap signalDataMap = gson.fromJson(signalingInfo.getData(), HashMap.class);
        if (signalDataMap != null) {
            businessIdObj = signalDataMap.get(TUIConstants.Message.CUSTOM_BUSINESS_ID_KEY);
        } else {
            Log.e(TAG, " signalDataMap is null ");
            return "";
        }
    } catch (JsonSyntaxException e) {
        Log.e(TAG, " get signalingInfoCustomJsonMap error ");
    }

    if (businessIdObj instanceof String) {
        businessId = (String) businessIdObj;
    }

    if (TextUtils.equals(businessId, "av_call")) {
        if (signalingInfo.getActionType() == V2TIMSignalingInfo.SIGNALING_ACTION_TYPE_INVITE) {
            // Make a call
            content = "@Make a call";
        } else if (signalingInfo.getActionType() == V2TIMSignalingInfo.SIGNALING_ACTION_TYPE_ACCEPT_INVITE) {
            // Answer the call
            content = "@Answer the call";
        } else {
            // Other
            // ...
        }
    }

    return content;
}
```
:::
::: iOS and macOS
```objectivec
/// Custom text of the signaling message
+ (NSString *)getCallSignalingContentWithMessage:(V2TIMMessage *)message
{
    V2TIMSignalingInfo *info = [[V2TIMManager sharedInstance] getSignallingInfo:message];
    if (!info) {
        return nil
    }
    // Parse the `data` field passed through
    NSError *err = nil;
    NSDictionary *param = nil;
    if (info.data != nil) {
        param = [NSJSONSerialization JSONObjectWithData:[info.data dataUsingEncoding:NSUTF8StringEncoding] options:NSJSONReadingMutableContainers error:&err];
    }
    if (!param || ![param isKindOfClass:[NSDictionary class]]) {
        return nil
    }
    
    // Identify the business type
    NSArray *allKeys = param.allKeys;
    if (![allKeys containsObject:@"businessID"]) {
        return nil
    }
    NSString *businessId = [param objectForKey:@"businessID"];

    // Determine whether it is an audio/video call signaling
    NSString *content = nil;
    if ([businessId isEqualToString:@"av_call"]) {
        if (info.actionType == SignalingActionType_Invite) {
            // Make a call
            content = @"Make a call";
        } else if (info.actionType == SignalingActionType_Accept_Invite) {
            // Answer the call
            content = @"Answer the call";
        } else {
            // Other
            // ...
        }
    }
    return content;
}
```
:::
::: Windows
```cpp
Custom text of the signaling message
std::string GetCallSignalingContentWithMessage(const V2TIMMessage& message) {
   V2TIMSignalingInfo signalingInfo =
       V2TIMManager::GetInstance()->GetSignalingManager()->GetSignalingInfo(message);
   if (signalingInfo.inviteID.Empty()) {
       // If `V2TIMSignalingInfo::inviteID` is empty, `message` is not a signaling message.
       return {};
   }

   // Parse the `data` field passed through, using the open source library RapidJSON at https://github.com/Tencent/rapidjson/
   rapidjson::Document document;
   document.Parse(signalingInfo.data.CString(), signalingInfo.data.Size());
   if (!document.HasMember("businessId") || !document["businessId"].IsString()) {
       return {};
   }
   const char* businessId = document["businessId"].GetString();

   // Determine whether it is an audio/video call signaling
   std::string content;
   if (businessId == "av_call") {
       if (signalingInfo.actionType == V2TIMSignalingActionType::SignalingActionType_Invite) {
           // Make a call
           content = u8"Make a call";
       } else if (signalingInfo.actionType == 2TIMSignalingActionType::SignalingActionType_Accept_Invite) {
           // Answer the call
           content = u8"Answer the call";
       } else {
           // Others
       }
   }

   return content;
}
```
:::
</dx-tabs>


[](id:qa)
## FAQs

[](id:qa1)
### 1. What should I do if "total count of request cloud message exceed max limit" is displayed in the log when I am pulling historical messages?

Currently, the SDK policy is as described below:
1. When `getType` is set to pull cloud historical messages and the number of messages to be pulled is set to `count`, the SDK will pull `count` messages from the cloud.
2. The SDK will filter out invalid messages, such as deleted messages and those irrelevant to the current user.
3. If there are too many invalid historical messages in the cloud, the SDK will perform multiple paged pulls.
To ensure the system stability and robustness, the SDK will perform up to three automatic paged pulls. After this limit is exceeded, the "total count of request cloud message exceed max limit" message will be displayed in the log.

To minimize the impact of such a limit mechanism on the business layer, you can take the following measures to reduce invalid messages:
* You can use online messages, that is, set `onlineUserOnly` to `YES/true` when sending messages.
* For group messages, you can use targeted group messages to specify the receiver.

[](id:qa2)
### 2. What should I do if messages are "lost" during cloud historical message pull?
When `getType` is set to pull cloud historical messages and the number of messages is `count`, the SDK will perform the following operations:
1. Pull `count` messages from the local database.
2. Pull `count` messages from the cloud and filter out invalid messages such as deleted messages. If the number is smaller than `count`, the paged pull will be triggered.
3. Merge local and cloud messages and update information such as the message status.
4. Return `count` messages from the merged message list.

Generally speaking, message loss indicates that too many invalid messages are pulled in step 2, which triggers the limit mechanism in question 1 and leads to an insufficient number of messages actually pulled from the cloud.
We recommend you fix this issue as instructed in question 1. If the issue persists, contact us for assistance.

[](id:qa3)
### 3. What should I do if group member information such as the group name card is not updated in real time when historical messages are pulled?
* When messages are generated, the SDK will update the current group member information such as the group name card and role and store it in the local database.
* When historical group messages are pulled, the SDK will directly query the group member information when the messages were generated and will not request updates from the backend in real time.

If you want to get the latest group member information, you can use the `getGroupMembersInfo` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ab303f20f53de134e6f6ebe5f9f9bcad0) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a6db2fcfd78bbd71003ae31584c88c672)).


[](id:qa4)
### 4. What should I do if I get a lag while pulling historical messages?
The SDK has been optimized for message pull. If a lag occurs, you can reduce the number of pulled messages (`count`). If the issue persists, contact us for assistance.
