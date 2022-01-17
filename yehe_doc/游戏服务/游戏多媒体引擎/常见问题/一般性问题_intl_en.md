## General Issues

### Does the so library for Android provide the x86_64 version?
No.

### What should I pay attention to when hot-updating GME?

To hot-update the GME SDK, you need to update the modules depending on the SDK together by including all GME-related code in the hot update.

### What gaming scenarios does the voice chat service support?

There are mainly three types of applicable scenarios:
- **Mic sequence:** Users take turns to speak. This mode allows a high sound quality and fluency and is suitable for such scenarios as Werewolf.
- **Free audio call:** This mode allows multiple players to speak at the same time with ultra-low latency, which is suitable for competitive games such as multi-player team chat.
- **Command:** Suitable for one-to-many commanding, audio interaction with host, and other scenarios in large-scale commander games.

Voice chat features provided by the Tencent Cloud SDK can meet the needs of the above-mentioned scenarios. However, the specific mode (such as mic sequence) is something that should be implemented in your own product's application layer through a delivery protocol, for example.

## APIs

### The error code 7015 is returned in the initialization. How to fix it?

- If it happened during development, please check whether all the SDK files are of the same version, as you might have upgraded SDKs but not in a comprehensive manner.
- If it happened after the executable file is exported, you can ignore it, as the packaging program of Unity and a third-party reinforcement program might modify the MD5 value of the SDK files.

### Is there a requirement for the value of `OpenId`?

Only a 64-bit unsigned integer is allowed for `OpenId`. Please convert it to a string before passing it to SDK.

### Can one `OpenId` be used to enter multiple rooms at the same time?

No. Each `OpenId` can only exist in one single room at a time.

### When should the Poll function in the GME SDK be called?

Please call the Poll function periodically after initializing the SDK.

### As calling the Poll function periodically is required for triggering events, can I start a new thread, wake it up periodically, and then call the Poll function?

Theoretically, all of our APIs need to be called in the same thread. If you choose to call them in a child thread, make sure to call them in the same child thread, especially for the Init and Poll function.

### How often should I call the Poll function?

If you don't have other special requirements, please call it as instructed in the sample code of the demo. You can see the `EnginePollHelper.m` of the demo, the recommended frequency is every 1/30 seconds.

### I periodically called the Poll function before finishing recording and the interface was stuck. How to fix it?

Please check whether the Poll function is called in the main thread.

### Is uninitialization required after I exited a voice chat room?

No. The operation is only required when you do not use SDK or switch accounts.
