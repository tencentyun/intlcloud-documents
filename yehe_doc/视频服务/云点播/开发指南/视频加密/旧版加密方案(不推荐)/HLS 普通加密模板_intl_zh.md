云点播转码平台在对视频进行 HLS 普通加密时，会将获取解密密钥的 URL 写入 M3U8 视频文件的`EXT-X-KEY`标签中，详细请参见 [HLS 普通加密](https://intl.cloud.tencent.com/document/product/266/33968)。

HLS 普通加密模板，包含`definition`（唯一的模板 ID）和`get_key_url`（获取解密密钥的 URL）参数。
