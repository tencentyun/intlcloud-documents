> !
>1. This document applies only to push requests over RTMP.
>2. This document is not applicable to other COS HTTP requests.

## Push Request

A push request over the RTMP protocol is in the following format:

```plaintext
rtmp://[BucketName-APPID].[host]/live/[channel]?[params]
```

A complete request with signing information is as follows:

```plaintext
rtmp://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/live/test-channel?q-sign-algorithm=sha1&q-ak=ak&q-sign-time=1606445586;1606545646&q-key-time=1606445586;1606545646&q-signature=signature
```

- **rtmp**: RTMP protocol (fixed)
- **examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com**: an endpoint that carries the bucket name and `APPID`. It is similar to other COS HTTP requests.
- **live**: name of the app for RTMP. For COS, it is fixed to `live`.
- **test-channel**: channel name, which can be customized during channel creation.
- **params**: push parameters, which are in `q-sign-algorithm=sha1&q-ak=ak... ...` order after the question mark (?). Currently, these parameters are used to deliver the signing information. The following describes how to generate the signature parameters:

## Signature Parameters in a Push Request

The following table describes the signature parameters in a push request:

| Signature Parameter | Description |
| ---------------- | :----------------------------------------------------------- |
| q-sign-algorithm | Signature algorithm. Currently, it is fixed to `sha1`. |
| q-ak | `SecretId`, which can be obtained at [Manage API Key](https://console.cloud.tencent.com/cam/capi) |
| q-sign-time | Start timestamp and end timestamp (in Unix format) of the signature validity period (e.g., `1557902800;1557910000`) |
| q-key-time | Start timestamp and end timestamp (in Unix format) of the key validity period. |
| Other parameters | Other parameters will be extended in the future. You are advised to leave it empty for the time being. |
| q-signature | The signature calculated with signature parameters |



## Calculating a Signature for a Push Request

The value of `q-signature` in the push request is calculated as follows:

```plaintext
Signaure=hmac-sha1(SecretKey , "sha1\n" + KeyTime + "\n" + sha1Hex(RtmpString) + "\n")
```

The following describes the directions:

### Step 1. Generate KeyTime
1. Get the Unix timestamp "StartTimestamp" for the current time, which is the total number of seconds starting from January 1, 1970, 00:00:00 UTC (January 1, 1970, 08:00:00 Beijing time).
2. Calculate the Unix `EndTimestamp` for the signature to expire according to `StartTimestamp` and the expected validity period of the signature.
3. Generate `KeyTime` by splicing the two timestamps above in `StartTimestamp;EndTimestamp` format (e.g., `1557902800;1557910000`).

### Step 2. Generate RtmpString
Generate `RtmpString` in `CanonicalizedResource\nCanonicalizedParams\n` format according to the resource information and parameters (empty currently) in the request.

Where:
- `CanonicalizedResource` is information about the requested resource. RTMP push requests take `/[BucketName-APPID]/[channel]`.
- `CanonicalizedParams` is the request parameter information. Currently, you can leave it empty.
- `\n` is a line break. If a string is empty, the line breaks before and after it need to be retained, for example, `/examplebucket-1250000000/test-channel\n\n`.


### Step 3. Generate StringToSign

Generate `StringToSign` with `KeyTime` and `RtmpString`, in `sha1\nKeyTime\nsha1Hex(RtmpString)\n` format.
Where:

- `sha1` is a fixed string.
- `\n` is a line break.
- `sha1Hex(RtmpString)` is the message digest of the RTMP string. It is a hexadecimal string (lowercase), for example, `54ecfe22f59d3514fdc764b87a32d8133ea611e6`.

### Step 4. Generate the signature

Use the [HMAC-SHA1](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C) algorithm with `SecretKey` as the key and [StringToSign](#stringtosign) as the message to calculate the message digest, that is, the `Signature` (for example, `01681b8c9d798a678e43b685a9f1bba0f6c0e012`).

### Step 5. Generate complete signature parameters

After `SecretId`, `KeyTime`, and `Signature` are generated, generate the complete signing information in the following format:

```plaintext
q-sign-algorithm=sha1
&q-ak=SecretId
&q-sign-time=KeyTime
&q-key-time=KeyTime
&q-signature=Signature
```

>! Line breaks in the sample above are for easier reading only and are not included in the actual signature.

Pass the information above to the RTMP request parameters. Unlike HTTP, RTMP does not involve headers. Therefore, you can only pass the signing information via the request parameters.

## Sample Code

### Pseudocode

```plaintext
KeyTime = [Now];[Expires]
RtmpString = [CanonicalizedResource]\n\n
StringToSign = sha1\nKeyTime\nSHA1(RtmpString)\n
Signature = HMAC-SHA1(SignKey, StringToSign)
```

### Sample of the message digest algorithm

For more information about how to call `HMAC-SHA1` using your preferred programming language, please see the **Sample Code** section in [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

## Use Cases

### Preparations

1. Log in to the CAM console and go to [Manage API Key](https://console.cloud.tencent.com/cam/capi) to obtain `APPID`, `SecretId`, and `SecretKey`. The following values are examples:

| APPID      | SecretId                             | SecretKey                        |
| ---------- | ------------------------------------ | -------------------------------- |
| 1250000000 | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q | BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz |

2. Create a bucket in the COS console and obtain the following information:

| Region | Bucket Name | Channel Name |
| ------------ | --------------------- | ------------ |
| ap-guangzhou | examplebucket-1250000000 | test-channel |



### Intermediate variables involved during signature generation

- **KeyTime** = `1606550430;1606554030`
- **CanonicalizedResource**=`/examplebucket-1250000000/test-channel`
- **RtmpString** = `/examplebucket-1250000000/test-channel\n\n`
- **StringToSign** = `sha1\n1606550430;1606554030\n44bb35a2713324b40406f7b4b457e33df378a346\n`<span id="stringtosign"></span>
- **Signature** = `d3b294bdf047228fca13291dea70a28e563ce4e2`

  

Push the local video to COS through FFmpeg with the request below:

```plaintext
ffmpeg -re -i /data/example.mp4 -vcodec h264 -acodec aac -f flv -y  "rtmp://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/live/test-channel?q-sign-algorithm=sha1&q-ak=AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q&q-sign-time=1606550430;1606554030&q-key-time=1606550430;1606554030&q-signature=d3b294bdf047228fca13291dea70a28e563ce4e2"
```

> !Since the signing information in the push request contains ampersands (&) and semicolons (;), please enclose the whole request with quotation marks (") to avoid request failure due to missing escape characters.
