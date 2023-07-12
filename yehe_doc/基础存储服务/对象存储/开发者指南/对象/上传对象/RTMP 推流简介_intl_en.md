## Overview

The RTMP API provided by COS can directly push audio/video content to the specified COS bucket and save it in the specified format.

Before pushing a stream, you need to call the LiveChannel HTTP API provided by COS to create a channel and get the push address of the object first.

In addition, COS provides various LiveChannel APIs such as query, management, and VOD, making it easier for you to use, manage, and share audio/video content in COS.


## Use Cases

Audio/Video push and upload scenarios such as home surveillance and security surveillance.


## How to Use

#### Using RESTful APIs

Call RESTful APIs to use LiveChannel APIs as instructed in the following API documents:

- [PUT LiveChannel](https://intl.cloud.tencent.com/document/product/436/39047)
- [List LiveChannels](https://intl.cloud.tencent.com/document/product/436/39046)
- [DELETE LiveChannel](https://intl.cloud.tencent.com/document/product/436/39049)



## Restrictions

- The RTMP protocol can be used only for stream push but not pull.
- Video streams are required and must be in H.264 format.
- Audio streams are optional and can be in AAC format only. Audio streams in other formats will be discarded.
- Only the HLS protocol is supported for dump.
- Only one client can push a stream through a channel at a time.

