Tencent Cloud MediaPackage (MDP) provides professional, stable, and secure video packaging and delivery services for global users. Leveraging the compute resources in Tencent Cloud's abundant AZs deployed around the globe and proprietary world-leading audiovisual technologies, MediaPackage simplifies video packaging and delivery and enhances the origin resiliency, which enables video providers to stream videos securely and stably on a large scale.

## Key Features

### Multiprotocol primary/backup stream inputs

MediaPackage supports HLS and DASH input streams. It generates primary and backup stream input addresses for each channel and allows you to push both streams at the same time, thus protecting your video assets stably and reliably.

### Flexible disaster recovery mechanism for output

MediaPackage supports a flexible disaster recovery mechanism for output. When you input primary and backup streams at the same time, if the primary input fails due to unstable network connection or other exceptions, MediaPackage will switch to the backup input seamlessly for uninterrupted push. You can customize related parameters such as the switch time.

### Secure and stable origin server protection

MediaPackage supports pulling streams from the origin server through multiple endpoints. This enables you to build your own origin servers, thus ensuring secure and reliable video stream delivery on a large scale.

### Quick connection with CDN

MediaPackage allows you to quickly connect to LVB CDN and add your own playback domain name for delivery. The edge servers deployed around the world help deliver your videos stably and efficiently.

### Comprehensive security protection

MediaPackage supports multiple authentication modes throughout the entire input and output process. You can authenticate an input stream with a username and password in HTTP-authentication mode and authenticate an output stream with an IP blocklist/allowlist, Authkey, the X-TENCENT-PACKAGE field in the HTTP header, or a CIDR block-level protection policy.

### High scalability for standalone or mix-and-match use
MediaPackage helps you build your own origin servers with speed and ease to deliver video content to high numbers of viewers. It simplifies video packaging and delivery and can be integrated with other Tencent Cloud services such as MediaLive, MediaConnect, and LVB CDN to implement a full linkage of large-scale broadcast-grade one-stop media services.
