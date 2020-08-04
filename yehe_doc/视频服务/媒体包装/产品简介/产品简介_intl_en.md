Tencent Cloud MediaPackage (MDP) provides professional, stable and secure video packaging and delivery services for global users. It leverages Tencent Cloud’s globally deployed compute resources and independently developed audiovisual technologies to simplify video packaging and distribution, while enhancing origin resiliency. MDP enables video providers to stream videos safely and stably on a global scale.

## Key Features

### HLS and DASH input redundancy
MediaPackage supports HLS and DASH input types. It will generate two input streams for each channel. **You can push both streams at the same time. If one input stream fails due to unstable network or other exceptions, MediaPackage will switch over to the other input stream seamlessly so the service is not interrupted.** It is stable and reliable in protecting your video assets.

### Diverse output methods
MediaPackage supports pulling streams from the origin server through multiple endpoints. Its quick integration with Tencent Cloud LVB CDN distribution allows you to build your own origin servers, ensuring safe and reliable video stream distribution on a global scale.

### High security

MediaPackage supports multiple authentication methods throughout the entire input and output process. **You can verify an input stream using a username and password in HTTP-authentication mode. You can authenticate an output stream using an IP blocklist/allowlist (CIDR block supported), Authkey, and the X-TENCENT-PACKAGE field in the HTTP header.**

### Built-in scalability and easy integration with Tencent Cloud services

MediaPackage helps you build your own origin servers for video delivery, simplifying video packaging and distribution. You can also integrate MediaPackage with other Tencent Cloud products (MediaLive, MediaConnect, LVB CDN, etc.) to implement large-scale, broadcast-grade, and one-stop media services.

### High-availability cache protection

MediaPackage provides multi-level cache protection. When a server has an exception, the built-in monitoring system of MediaPackage can automatically remove the node to ensure the high reliability of regional resources. MediaPackage also supports input redundancy, where input streams can be switched seamlessly to ensure high stability and availability during push.
