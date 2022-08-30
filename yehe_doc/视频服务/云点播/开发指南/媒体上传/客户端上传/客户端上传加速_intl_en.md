Client upload acceleration provides a higher-quality upload service. Based on Tencent Cloud's globally deployed acceleration network, this feature intelligently selects the optimal access point and linkage based end users' requests, increasing the upload speed and success rate. In addition, it supports data transfer over the QUIC protocol to improve the data transfer efficiency and the stability under poor network conditions.

## Major Factors Affecting the Upload Quality
### Long-distance transfer
VOD deploys storage centers in many regions globally. You can enable them as needed for nearby storage during video upload. For more information, see [How to Increase the Speed and Success Rate of Media File Upload](https://intl.cloud.tencent.com/document/product/266/37548). However, some end users may still be too far away from storage centers, and some customers have cross-region and even overseas upload. Long-distance upload means a longer network linkage and transfer latency. Moreover, once a problem such as network jitter and packet loss occurs at one stage, the upload speed and success rate of the entire linkage will be lowered.
### Poor network conditions
Poor network conditions mean a high latency and high packet loss rate. Nowadays, mobile networks have a wide coverage, and upload requests from mobile devices account for a large proportion. However, mobile networks usually experience poor network conditions; for example, the end user is in a region where the base station signal is weak or the device network frequently switches when the end user moves. In this case, how to guarantee stable data transfer under poor network conditions is a challenge for improving the upload quality.
### Inefficient network protocol
Most files uploaded by VOD users are large video files. However, the most frequently used network protocol for upload is still HTTP 1.1. This protocol is essentially based on the serial model and has problems such as head-of-line (HOL) blocking, so it can easily encounter a performance bottleneck when a massive amount of data is transferred.


## Client Upload Acceleration Scheme
### Global linkage acceleration over reliable channels
To address the problem of poor upload quality due to a long network linkage in long-distance transfers, VOD provides a set of global linkage acceleration channels, allowing data to be uploaded and transferred via Tencent Cloud's globally deployed acceleration network and edge nodes. By leveraging Tencent Cloud's smart global traffic management platform, VOD sends the upload request from an end user to the edge node nearest to the user to implement nearby user data reception. Then, VOD selects the optimal linkage based on the acceleration network to send the data to the storage center.
### Faster and more stable QUIC protocol
In view of poor network conditions and inefficient network protocols, VOD supports the QUIC protocol for client upload. The QUIC protocol is a UDP-based low-latency and high-reliability communication protocol. The current standard HTTP/3 protocol is implemented based on QUIC. QUIC supports 0-RTT connection establishment and non-HOL blocking multiplexing to transfer more data with a lower bandwidth. This enables high-quality data transfer, even under poor network conditions with high packet loss rate and network latency. QUIC also supports connection migration, enabling smooth network switching even for mobile devices that frequently switch networks, guaranteeing an uninterrupted network connection.
### Easy-to-use smart channel selection
VOD provides an easy-to-use upload acceleration solution, which can be enabled simply in the console. When you use the SDK for upload, it intelligently compares the speed of the general channel and acceleration channel and automatically selects the better channel. It also automatically detects the connection conditions and determines whether to upload the data over the QUIC protocol. 
![](https://qcloudimg.tencent-cloud.cn/raw/7366fe0fa9050bf06551938e2b9485a8.jpg)

## How to Use
You can enable the client upload acceleration feature with the following steps:
1. Enable **Global Linkage Acceleration** as instructed in [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874) and enable **QUIC-based Transfer** as needed.
2. Make sure that [pre-upload](https://intl.cloud.tencent.com/document/product/266/37548) is called during application startup on Android or iOS. To enable **QUIC-based Transfer**, you must use the SDK for Android 9.6 or later or SDK for iOS 10.4 or later.

>?
>- Currently, the SDK for web doesn't support upload acceleration.
>- Currently, the SDK for mini program doesn't support QUIC-based transfer.

## Billing
The client upload acceleration feature involves the following fees:
- Global linkage acceleration fees: Upload acceleration traffic fees incurred while using global linkage acceleration.
- QUIC-based transfer fees: Upload acceleration traffic fees incurred while using QUIC-based transfer.
For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/266/2838).
