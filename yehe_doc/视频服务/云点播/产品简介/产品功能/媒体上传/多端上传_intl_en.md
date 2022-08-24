## Overview

The multi-end upload feature allows users to upload media files such as audio, video, and images to VOD through various methods, including upload via client, server, public network URL, and live recording.

Specifically, VOD supports the following upload methods:

| Feature | Description |
| -- | -- |
| Upload from client | Upload media files on the client to VOD. It supports SDKs for various platforms, including iOS, Android, web, and mini program, and you can implement this feature simply by integrating the corresponding SDK.  |
| Upload from server | Upload media files on a server to VOD. It supports SDKs for various programming languages, including Java, C#, PHP, Python, Node.js, and Go.  |
| Upload through console | Upload media files directly from the VOD console after logging in. |
| Pull from URL | Pull media resources on the network to VOD via URL.  |
| Live recording upload | Record live media directly to VOD when recording is enabled in CSS.  |
| Upload through origin server migration tool | Upload media files from other cloud vendors to VOD through a tool provided by VOD. |

The upload methods of VOD cover almost all media sources, so you can upload files from any source.

## Use Cases

| Feature | Description |
| -- | -- |
| Upload from client | In UGC and PGC scenarios, most media files are created by general users. After a user creates content using a device like their mobile phone or PC, the user can upload the media on the client to VOD. |
| Upload from server | Large video portals or platforms that own the copyright of their media usually store media on their own servers. In this case, they can upload the media files on their servers to VOD in batches.|
| Upload through console | If you want to upload a local media file on your PC, you can quickly upload it from the console. |
| Pull from URL | If the video you want to upload is already available on the network, you can upload it to VOD directly using the media URL of the video. |
| Upload through origin server migration tool | If you want to migrate all existing videos from another cloud vendor or migrate a large number of videos from local storage, you can use the origin server migration tool to upload them to VOD. |

## Directions

* [Upload from client](https://intl.cloud.tencent.com/document/product/266/33921)
* [Upload from server](https://intl.cloud.tencent.com/document/product/266/33912)
* [Upload from the console](https://intl.cloud.tencent.com/document/product/266/33890)
* [Pull from URL](https://intl.cloud.tencent.com/document/product/266/37550)
* [Live recording upload](https://intl.cloud.tencent.com/document/product/266/39562)
* [Upload through the origin server migration tool](https://intl.cloud.tencent.com/document/product/266/37551)
