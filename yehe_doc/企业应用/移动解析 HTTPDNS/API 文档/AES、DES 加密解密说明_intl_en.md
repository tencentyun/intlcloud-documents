## Overview
This document describes how to use the DES and AES encryption algorithms. They can be used to encrypt the request parameters and decrypt the response data so as to prevent requests in plaintext from being maliciously altered during transfer.

>? If you make a query with an HTTPS request method, the transferred data will be protected through encryption because of the TLS channel, so you don't need to encrypt the data passed in.
## Prerequisites
- You [have activated HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461) and obtained the configuration information such as authorization ID, encryption key, and HTTPS token. For more information, see [Configuration Information Description](https://intl.cloud.tencent.com/document/product/1130/44467).
- You have added the domain to be queried in the HTTPDNS console as instructed in [Adding a Domain](https://intl.cloud.tencent.com/document/product/1130/44465).

## Directions

**Step 1. Determine the encryption method.**
Currently, HTTP requests to HTTPDNS can be encrypted with DES or AES.
>? 
>- If you make a query with an HTTPS request method, see [Querying with HTTPS Request Methods](https://intl.cloud.tencent.com/document/product/1130/44469).
>- Encrypt the domain to be resolved with the corresponding key and algorithm (if you want to use the `ip` parameter, you also need to encrypt it) and use the encrypted result and ID (which does not need to be encrypted) as the request parameters.
>
**Step 2. Send an encrypted request.**
**Step 3. Receive an encrypted response.**
**Step 4. Decrypt the result.**


## Encryption and Decryption Algorithm Use Instructions[](id:state)

### DES algorithm
>? For encryption and decryption with DES, the key is 8 characters in length, the block cipher mode is `ECB`, and the padding algorithm is `PKCS5Padding`.
>
The encrypted data is encoded by using `Hex(Base16)` to convert the binary data into a visible hexadecimal ID, and the length of the encoded data will double. The detailed process is as shown below:
![](https://main.qcloudimg.com/raw/325fd677d99012440bdd12cb1dbed180.png)

Decryption of the response data involves decoding the data to binary data with `Hex` first and then decrypting the binary data with the DES algorithm into plaintext data. The detailed process is as shown below:
![](https://main.qcloudimg.com/raw/6eff04fd43aba6643408cb1f89ebbcce.png)

For example, if your domain is `www.dnspod.cn` and the encryption key is `dnspodpass`, the process will be as follows:
1. Add the domain in the [HTTPDNS console](https://console.cloud.tencent.com/httpdns/domain).
2. Encrypt the domain with the encryption algorithm `DES-ECB-PKCS5` and [DES encryption key](https://intl.cloud.tencent.com/document/product/1130/44467) `dnspodpass`, and you will get the encrypted string `87ae992c1321f299da3c0210a9900ae7`.
3. Call the `curl "http://119.29.29.98/d?dn=87ae992c1321f299da3c0210a9900ae7&id={authorization ID}"` API to request the A record.
You will get an encrypted string with a doubled length, such as `55915a682ea20840ff74aa6e7bebf11454ed0f4050a63e93e6e89521553a01a8`.
4. Decrypt the encrypted string with the encryption algorithm `DES-ECB-PKCS5` and [DES encryption key](https://intl.cloud.tencent.com/document/product/1130/44467) `dnspodpass`, and you will get the plaintext data `121.12.53.35;106.227.19.35`.

>?The above strings are used as an example only and cannot be used for normal requests.


### AES algorithm
>?For encryption and decryption with AES, the key is 16 characters in length, the block cipher mode is `CBC`, and the padding algorithm is `PKCS7`.
>
The CBC mode requires a random `IV` as the initial input for encryption and decryption, so the `IV` will also be carried in the request and response. The encrypted data along with the `IV` is encoded by using `Hex` and converted into a visible hexadecimal ID. The detailed process is as shown below:
![](https://main.qcloudimg.com/raw/15f106152b9294a6115900d7c95db63e.png)
During decryption, the data is decoded to binary data by using `Hex`, where the first 16 bytes is the `IV` value, and the bytes after `IV` is the data to be decrypted with the AES algorithm. The plaintext data will be obtained after decryption. The detailed process is as shown below:
![](https://main.qcloudimg.com/raw/af3b12e5945a0336ca85ca02d3005a5a.png)





