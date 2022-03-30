You can use `secret_id` and `secret_key` for authentication management of your APIs. As `secret_id` and `secret_key` appear in pairs, they are called `secret_id/secret_key` pair.
You need to create a secret_id/secret_key pair before the authentication.

## Key Pair Authentication for API
When creating an API, you can choose the authentication type as "key pair authentication". Then, after the API is released, only access requests to it initiated with the correct key pair can pass the authentication by API Gateway, while requests without the key or correct key pair cannot.
After the API is created, you need to use the "usage plan" feature to bind the key pair to the API or the service where the API resides. For more information on the configuration, please see [Usage Plan](https://intl.cloud.tencent.com/document/product/628/11815).

## Key Content
Sample **secret_id**: `AKIDCg*****j548pN`. It is used to identify which key is used, participates in signature computation, and is reflected in the transfer process.
Sample **secret_key**: `ZxF2wh*****N2oPrC`. It is used for signature computation, but is not reflected in the transfer process.

## Signature Computation
### Content to be delivered at last
The HTTP request delivered at last contains at least two headers: Date/X-Date and Authorization. More headers such as source in a request are also workable.

The value of Date header is the time constructed by HTTP request in GMT, for example: Fri, 09 Oct 2015 00:00:00 GMT.

The value of X-Date header is the time constructed by HTTP request in GMT, for example: Mon, 19 Mar 2018 12:08:40 GMT. The value for timeout is 15 minutes.

Source header represents the signature watermark value. You can enter any value for it or leave it empty.

The `Authorization` header is in the format of `Authorization: hmac id="secret_id", algorithm="hmac-sha1", headers="date source", signature="Base64(HMAC-SHA1(signing_str, secret_key))"`.

The various parts of Authorization are explained as follows:
**hmac**: a fixed part used to indicate the computation method.
**ID**: the value of secret_id in the key.
**algorithm**: the encryption algorithm. hmac-sha1 is supported now.
**headers**: refer to headers that involve in signature computation, sorting by the order of actual computation.
**signature**: the signature obtained after signature computation is completed, with `signing_str` as its content.

### Signature computation method
A signature has 2 parts and is computed according to the specified encryption algorithm. Take hmac-sha1 algorithm as an example:

#### Signature content
First, generate the signature content, which consists of custom headers. It is recommended to include "date" at least in the header. But you can also include more headers.

Headers are converted according to the following requirements and then sorted in sequence:
1. The header name is converted to lowercase and followed by the **ASCII character `:`** and then **an ASCII space character**.
2. Attach the value of the header.
3. If it is not the last header that needs to construct a signature, attach **ASCII new-line character `\n`**.

For example, if there are two headers involved in constructing the signature content (this example is for your reference only. Please fill in the fields as needed):
```plaintext
Date:Fri, 09 Oct 2015 00:00:00 GMT
Source:AndriodApp
```
The generated signature content is as follows:
```plaintext
date: Fri, 09 Oct 2015 00:00:00 GMT
source: AndriodApp
```

#### Computing a signature
Base64(HMAC-SHA1(signing_str, secret_key)) algorithm is used to compute the signature content generated in the previous step to generate a signature, that is:
* Using the signature content as input information, and secret_key content as the key, compute according to HMAC-SHA1 algorithm to get the encrypted signature content.
* Convert the computed encrypted signature content to deliverable signature content using Base64.

#### Using a signature
As shown in **Content to be delivered at last**, at "signature" in the Authorization header, enter the signature computed in the last step.

## Notes

### header matching
The headers in `Authorization` are the ones involved in signature computation. We recommend you convert them to lowercase and separate them by ASCII spaces. For example, if the headers involved in the computation are `date` and `source`, the format should be `headers="date source"`; if only the `x-date` header participates in the computation, the format should be `headers="x-date"`.

### Signature content generation
When arranging the content, please pay extra attention to the colon and space after the header name. If they are missing, the verification may fail. `SecretId`, `SecretKey`, URL, and `Host` should be replaced with your real information. 

>? For signature demos for common programming languages, please see [Developer Guide - Generating Signatures in Multiple Programming Languages](https://intl.cloud.tencent.com/document/product/628/40460).
