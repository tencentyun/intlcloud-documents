Local search is implemented in the TUISearch component of TUIKit. It allows users to quickly find the expected information from massive amounts of complex data, such as the chat history, contacts, and group chats. It can also be used as an operations tool to easily and efficiently navigate to extensive content.

>! The local search feature is only available on the IM Ultimate edition. To use it, [purchase the Ultimate edition](https://intl.cloud.tencent.com/document/product/1047/34577). For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).


## Feature Demonstration
The search API UI consists of three parts: the first part is for friend search, the second part is for group and group member search, and the third part is for message search, where messages are classified by conversation.


## Integration Guide
The following introduces how to integrate the TUISearch component.

### Purchasing the package
[Purchase the Ultimate edition](https://intl.cloud.tencent.com/document/product/1047/34577).

### Integrating TUISearch
Add dependencies on `tuisearch` to the `build.gradle` file in `APP`:
```groovy
api project(':tuisearch')
```

### Logging in to TUIKit
You need to call `TUILogin` of `TUICore` to log in to TUIKit. Initialization is implemented inside the login API by default, and no additional call to the initialization API is required.
```
TUILogin.login(this, SDKAPPID, userID, userSig, new TUICallback() {
    @Override
    public void onError(final int code, final String desc) {
        // Login fails.
    }

    @Override
    public void onSuccess() {
        // Login succeeded
    }
});
```

### Starting the search UI
If you have integrated the TUIConversation and TUISearch components, no additional processing is required at this point and searchBar is displayed above the conversation list by default.
If you have integrated only TUISearch, you need to add your own search view and click to start SearchMainActivity.


## FAQs
1. How do I search for custom messages?
For custom messages created and sent via the [createCustomMessage (byte[] data, String description, byte[] extension)](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a313b1ea616f082f535946c83edd2cc7f) API, specify the text to search in the `description` parameter.
Custom messages created via the [createCustomMessage (byte[] data)](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5c2495d4b7ecd66e5636aeb865c17efd) API cannot be searched because binary data streams are saved locally.

If you configure the offline push feature and the `description` parameter, custom messages will also be pushed offline, and the content specified in the `description` parameter will be displayed in the notification bar.
If you do not need the offline push feature, use [disablePush](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a5d0ea30668513f45eda447875528b9c7) in [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) of the [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) API to disable it.
If you don't want to display the content pushed on the notification bar as the text to be searched for, you can use [setDesc](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) in [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) to set the push content.

2. How do I search for rich media messages?
Rich media messages include file, image, audio, and video messages.
For a file message, the filename is usually displayed on the UI. Therefore, you can set the `fileName` parameter as the searched content when creating a file message. If `fileName` is not set, the system gets the filename from `filePath` and saves it to both the local device and the server.
For an image, audio, or video message, the thumbnail or duration is usually displayed on the UI. In this case, you can specify the message type for search but cannot specify keywords for search.

[](id:feedback)
