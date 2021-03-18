## Voice Chat

### How is GME voice chat service billed?

GME voice chat supports pay-as-you-go billing mode. It is billed by the duration of audio generated and settled on a daily basis. 

### When does the billing of the voice chat start?

The voice duration starts when the `EnterRoom` API is called for room entering and stops when the `ExitRoom` API is called for room exiting.

### Does the initialization incur fees?

No.

### Is the data generated in SDK initialization collected to DAU?

No. The data is not collected to DAU as the initialization is not over GME servers.

### Will the billing continue if the client is disconnected from the server when using the voice chat?

In case the client is disconnected when using the voice chat, then:
1. The server keeps a heartbeat connection with the client. If the heartbeat pauses for 90 seconds, the server will remove the client and the billing will stop.
2. If the client process is not ended, the client keeps trying to reconnect to the server for 60 minutes. If the process is ended, it does not try to reconnect.

### Are there any differences among the billing of three GME sound qualities (smooth, standard, and HQ)?

No. The voice quality does not affect the billing.


## Speech-to-text Conversion

### What are the billing modes for GME voice message and speech-to-text conversion services?

The GME voice message and speech-to-text conversion services are billed by voice message DAU. For more information, please see [Daily Pay-as-You-Go Billing Mode](https://intl.cloud.tencent.com/zh/document/product/607/36276).
