## Overview

StreamPackage is a premium high-quality video muxing and origin-pull platform newly launched by Tencent Cloud, which provides professional, stable, and secure video muxing and delivery services for global users. Leveraging the compute resources in Tencent Cloud's abundant AZs deployed around the globe and proprietary world-leading audiovisual technologies and featuring a 24/7 availability, it simplifies video packaging and delivery and enhances the origin resiliency, which enables video content providers to stream videos securely and stably on a large scale.

![img](https://main.qcloudimg.com/raw/4a892b3997e8b86ff17ca6fe26f223ba.png)

## Feature

**Multi-Protocol Primary/Backup Inputs**

StreamPackage supports HLS and DASH input streams. It generates primary and backup stream input addresses for each channel (with dual-channel configuration) and allows you to push both streams at the same time, thus protecting your video assets stably and reliably.

**Flexible and Stable Disaster Recovery Mechanism**

When you input primary and backup streams at the same time, if the primary input fails due to unstable network connection or other exceptions, StreamPackage will switch to the backup input seamlessly for uninterrupted push. You can customize related parameters such as the switch time.

**High Security**

StreamPackage supports multiple authentication modes throughout the entire input and output process. You can authenticate an input stream with a username and password in HTTP-authentication mode and authenticate an output stream with an IP blocklist/allowlist, Authkey, the X-TENCENT-PACKAGE field in the HTTP header, or a CIDR block-level protection policy.

**Quick Connection with CDN**

StreamPackage supports quickly connecting to LVB CDN and adding your own playback domain name for delivery. The edge servers deployed around the world help ensure the delivery stability and efficiency of your videos.

**High-Availability Cache Protection**

StreamPackage provides multi-level cache protection. When a server has an exception, the built-in monitoring system of StreamPackage can automatically remove the node to ensure the high reliability of regional resources. StreamPackage also supports input redundancy, where input streams can be switched seamlessly to ensure high stability and availability during push.

**Architecture and Failover**

StreamPackage supports dual-pipeline configuration where pipeline A and pipeline B can input live streams at the same time. It also supports automatic failover, so that when the primary pipeline (pipeline A) detects that the live stream is interrupted for a certain period of time (which can be set through the "Max Segment Duration" parameter), it will automatically switch to the backup pipeline (pipeline B) for output.

StreamPackage channels support multi-endpoint pull configuration, which means that a channel can have multiple endpoints for output.

![img](https://main.qcloudimg.com/raw/b8d01ade821b7ed659ab65a4617ed6e1.png)