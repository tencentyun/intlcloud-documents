When the VOD transcoding platform performs HLS common encryption on a video file, it will write the URL used to get the decryption key into the `EXT-X-KEY` tag of the M3U8 file. For more information, please see [HLS Common Encryption](https://cloud.tencent.com/document/product/266/9638).

An HLS common encryption template contains `definition` (unique template ID) and `get_key_url` (URL used to get the decryption key) parameters. If you need to add, modify, or query this type of templates, please see the following template management APIs:

* [Create an HLS common encryption template](https://cloud.tencent.com/document/product/266/35167)
* [Update an HLS common encryption template](https://cloud.tencent.com/document/product/266/35168)
* [Query an HLS common encryption template](https://cloud.tencent.com/document/product/266/35169)

> Only VOD APIs 2017 are available for management of HLS common encryption templates.
