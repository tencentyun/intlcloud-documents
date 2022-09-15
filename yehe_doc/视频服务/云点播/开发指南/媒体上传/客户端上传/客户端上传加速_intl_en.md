Based on Tencent Cloud's globally deployed acceleration network, client upload acceleration intelligently selects the optimal access point and transfer linkage based on end users' requests, increasing their upload speed and upload success rate. In addition, it supports data transfer over the QUIC protocol to improve the efficiency and stability of data transfers under poor network conditions.

## Major Factors Affecting Upload Quality
### Long-distance transfer
VOD deploys storage centers in many regions globally. You can enable them as needed for nearby storage during upload. For more information, see [How to Increase the Speed and Success Rate of Media File Upload](https://intl.cloud.tencent.com/document/product/266/37548). However, some end users are still too far away from storage centers, and some users need to upload content across regions or even overseas. Long-distance upload means a longer network linkage and higher transfer latency. Moreover, once a problem such as network jitter and packet loss occurs at one part of the linkage, the upload speed and success rate of the entire linkage will be lowered.
### Poor network conditions
Poor network conditions lead to high latency and high packet loss rate. Today, mobile networks have a wide coverage, and upload requests from mobile devices account for a large proportion of network usage. However, mobile devices often experience poor network conditions; for example, when the mobile device is in a region with poor mobile network coverage or the user frequently switches between network devices while moving around. In this case, guaranteeing stable data transfer and upload quality is a difficult challenge.
### Inefficient network protocols
Most files uploaded by VOD users are large video files. However, the most frequently used network protocol for upload is still HTTP/1.1. This protocol is essentially based on the serial model and has problems such as head-of-line (HOL) blocking, which can lead to a performance bottleneck when a massive amount of data is transferred.


## Acceleration Scheme for Upload from Client
### Global linkage acceleration enabled by high-availability channels
To address the problem of poor upload quality due to a long network linkage in long-distance transfers, VOD provides a set of global acceleration channels based on Tencent Cloud's globally deployed acceleration network and edge nodes. By leveraging Tencent Cloud's smart global traffic management platform, VOD sends the upload request from an end user to the edge node nearest to the user. Then, VOD selects the optimal linkage to send data to the storage center via the acceleration network, which is continuously optimized by Tencent Cloud.
### Faster and more stable QUIC protocol
To help overcome poor network conditions and inefficient network protocols, VOD supports the QUIC protocol for upload from the client. The QUIC protocol is a UDP-based low-latency and high-reliability communication protocol. The current standard HTTP/3 protocol is implemented based on QUIC. QUIC supports 0-RTT connection establishment and non-HOL blocking multiplexing to transfer more data with a lower bandwidth, enabling high-quality data transfer even under poor network conditions with a high packet loss rate and network latency. It also supports connection migration to enable a smooth network switch even if the network of a mobile device is switched frequently, guaranteeing an uninterrupted network connection.
### Easy-to-use smart channel selection
VOD provides an easy-to-use upload acceleration solution that can be enabled simply in the console. When you use the SDK for upload, it intelligently compares the speed of the general channel and acceleration channel and automatically selects the better channel. It also automatically detects the connection conditions and determines whether to upload the data over the QUIC protocol. 
![](https://qcloudimg.tencent-cloud.cn/raw/7366fe0fa9050bf06551938e2b9485a8.jpg)

## How to Use
You can enable the client upload acceleration feature with the following steps:
1. Enable **Global Linkage Acceleration** as instructed in [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874) and enable **QUIC-based Transfer** as needed.
2. Make sure that [pre-upload](https://intl.cloud.tencent.com/document/product/266/37548) is called during application startup on Android or iOS. To enable **QUIC-based Transfer**, you must use the SDK for Android 9.6 or later or SDK for iOS 10.4 or later.
>?
>- The SDKs for Android and iOS support both upload acceleration and QUIC-based transfer.
>- Currently, the SDKs for web and mini program support only upload acceleration but not QUIC-based transfer.

## Billing
The client upload acceleration feature involves the following fees:
- Global linkage acceleration fees: Upload acceleration traffic fees incurred while using global linkage acceleration.
- QUIC-based transfer fees: Upload acceleration traffic fees incurred while using QUIC-based transfer.
For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/266/2838).
