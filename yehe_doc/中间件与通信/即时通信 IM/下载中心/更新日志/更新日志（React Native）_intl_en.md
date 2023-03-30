## Chat React Native SDK 0.1.9 @2022.12.05

- New: Multimedia message online URLs (`url`) will no longer be no longer returned by default. They need to be obtained by calling the `getMessageOnlineUrl` API.
- New: Multimedia message local URLs (`localurl`) will no longer be returned by default. They will be returned only after you download messages successfully by calling the `downloadMessage` API.
- New: The `onMessageDownloadProgressCallback` callback is added for `advanceMessageListener` and will be triggered when the multimedia message download progress is updated.
- New: The message extension feature is added. For details, see Message > Message Extension.
- Improvement: The underlying native SDK has been upgraded to 6.9.3557.

>?Major changes have been made to multimedia messages and file messages. Please modify your existing logic for obtaining and rendering such messages according to the first three updates. Otherwise, the messages will not be displayed. If you have any questions in the process of modification, please feel free to contact us.(https://cloud.tencent.com/online-service?from=doc_269).

## Chat React Native SDK 0.1.0 @2022.07.14
- Officially open to users

>? This is the first release of the Chat SDK for React Native, and it will be improved in future versions.
