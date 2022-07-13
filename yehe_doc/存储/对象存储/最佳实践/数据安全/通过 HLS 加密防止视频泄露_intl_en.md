## Overview

COS data processing offers the encryption feature for HTTP Live Streaming (HLS) videos. The encrypted video is not available for users without access permissions. HLS encryption must be used together with Key Management Service (KMS) and the Token service. This document describes a solution suitable for services that can build a complete set of authentication and KMS.

>! It supports only HLS encryption.
>

## How It Works

![](https://qcloudimg.tencent-cloud.cn/raw/fe49915c6d9de74677b6ef4f03ac5158.jpg).

>? In this solution, COS is connected to KMS.
>

### Encryption procedure

1. Upload a video to COS and request HLS encryption.
2. COS requests an encryption key from KMS.
3. COS encrypts the HLS video through transcoding.
4. After encryption, COS will deliver the encrypted video file through Content Delivery Network (CDN).

### Decryption procedure

1. The end user logs in to the player terminal and is identified by the service side. After the identity verification is successful, the service side will assign a token to the player terminal and return the tokenized playback URL to the player.
2. After obtaining the URL, the player parses the URI of the M3U8 file and request the key from URI.
3. Risk Control Management Service verifies the validity of the request, and then queries the key by calling KMS APIs.
4. KMS returns the decryption key to the player terminal. The player decrypts the M3U8 file by using the key for playback.

## Encryption Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket where you want to store the video.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Audio/Video Transcoding** and click **Create Transcoding Template**.
6. In the **Create Transcoding Template** window, configure the following items:

 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Encapsulation Format: Select HLS.
 - Transcoding Duration: You can select the input file duration or custom configuration.
 - Advanced configuration: 
    - Video Encryption: Enable.
    - UriKey: KMS URL built by users. 
7. Click **OK**, and then you can apply this template to encrypt videos when [configuring workflow](https://intl.cloud.tencent.com/document/product/436/46408) or [configuring job](https://intl.cloud.tencent.com/document/product/436/46409).
