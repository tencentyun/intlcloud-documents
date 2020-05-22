

### Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?

Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [legacy algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). If you have upgraded the version, you can switch between the new and old algorithms as needed.

Upgrade/Switch operation:
 1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc).
 2. Select **Application Management** on the left sidebar and click **Application Info** on the row of the target application.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.

### What are the restrictions of the firewall?
As TRTC uses UDP for audio/video transmission, it cannot be used in office networks that block UDP. If you encounter such a problem, please see [Dealing with Organizational Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) for assistance.

### The demo is running on two devices, but why can't they display the images of each other?
Please make sure that the two devices use different `UserID` values when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously, unless different `SDKAppID` values are used.

### When I watch live streaming over CDN, there is only one user in the room, but the video image is lagging and blurry. Why?
Please specify the `TRTCAppScene` parameter in `enterRoom` as **`TRTCAppSceneLIVE`**.
The `VideoCall` mode is optimized for video calls, so when there is only one user in the room, the video image will maintain a low bitrate and frame rate to reduce network traffic usage, which will look lagging and blurry.

### Why can't I enter any online room?

This may be because that room permission control has been enabled. Once room permission control is enabled, all rooms under the current `SDKAppID` can be entered only after `privateMapKey` is set in `TRTCParamEnc`, so if your online business is in operation and the relevant logic of `privateMapKey` has not been added to it, please do not enable this feature. For more information, please see [Restricting Room Entry Permissions](https://intl.cloud.tencent.com/document/product/647/35157).
