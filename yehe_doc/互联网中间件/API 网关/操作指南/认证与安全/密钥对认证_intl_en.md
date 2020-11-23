You can use `secret_id` and `secret_key` for authentication management of your APIs. As `secret_id` and `secret_key` appear in pairs, they are called `secret_id/secret_key` pair.
`secret_id/secret_key` pair needs to be created first before authentication.

## Key Pair Authentication for API
When creating an API, you can choose the authentication type as "key pair authentication". Then, after the API is published, only access requests to it initiated with the correct key pair can pass the authentication by API Gateway, while requests without the key or correct key pair cannot.
After the API is created, you need to use the "usage plan" feature to bind the key pair to the API or the service where the API resides. For more information on the configuration, please see [Usage Plan](https://intl.cloud.tencent.com/document/product/628/11815).

## Key Content
Sample **secret_id**: `AKIDCg*****j548pN`. It is used to identify which key is used, participates in signature calculation, and is reflected in the transfer process.
Sample **secret_key**: `ZxF2wh*****N2oPrC`. It is used for signature calculation but is not reflected in the transfer process.

## Calculation Method
### Eventually delivered content
The eventually delivered HTTP request contains at least two headers: `Date` or `X-Date` and `Authorization`. More optional headers can be added in the request.

The value of `Date` header is the construction time of the HTTP request in GMT format, such as Fri, 09 Oct 2015 00:00:00 GMT.

The value of `X-Date` header is the construction time of the HTTP request in GMT format, such as Mon, 19 Mar 2018 12:08:40 GMT. It will time out in 15 minutes.

The `Authorization` header is in the format of `Authorization: hmac id="secret_id", algorithm="hmac-sha1", headers="date source", signature="Base64(HMAC-SHA1(signing_str, secret_key))"`.

All parts of `Authorization` are as detailed below:
**hmac** is fixed and used to indicate the calculation method.
**ID** is the value of the `secret_id` in the key.
**algorithm** is the encryption algorithm. HMAC-SHA1 is supported currently.
**headers** refers to headers involved in signature calculation and are sorted by the order in actual calculation.
**signature** is the signature obtained after signature calculation is completed, with `signing_str` as its content.

### Signature calculation method
A signature consists of two parts and is calculated by the specified encryption algorithm. The following uses the HMAC-SHA1 algorithm as an example:

#### Signature content
First, generate the signature content composed of custom headers. You are recommended to at least include `date` in the header. You can also include other headers as desired.

Headers are converted according to the following requirements and then sorted in sequence:
* The header name is converted to lowercase and followed by **ASCII characters** and **ASCII space characters**.
* Then, append the value of the header.
* If it is not the last header that needs to construct the signature, append an **ASCII newline character `\n`**.

For example, if there are two headers involved in constructing the signature content (this example is for your reference only. Please fill in the fields according to your actual business conditions):
```
Date:Fri, 09 Oct 2015 00:00:00 GMT
Source:AndriodApp
```
Then, the generated signature content will be as follows:
```
date: Fri, 09 Oct 2015 00:00:00 GMT
source: AndriodApp
```

#### Signature calculation
The Base64(HMAC-SHA1(signing_str, secret_key)) algorithm is used to calculate the signature content generated in the previous step to generate a signature, that is:
* Use the signature content as input information and `secret_key` as the key to calculate the encrypted signature content through the HMAC-SHA1 algorithm.
* Convert the calculated encrypted signature content to deliverable signature content with Base64.

#### Signature use
As shown in **Eventually delivered content**, enter the signature generated in the previous step in the `signature` field in the `Authorization` header.

## Precautions

### Header alignment
The headers in `Authorization` are the ones involved in signature calculation. You are recommended to convert them to the lowercase and separate them by ASCII spaces.

### Signature content generation
When arranging the content, please pay extra attention to the colon and space after the header name. If they are missing, the verification may fail. `SecretId`, `SecretKey`, URL, and `Host` should be replaced with your real information. 

>?For signature demos for common programming languages, please see [Developer Guide - Generating Signatures in Multiple Programming Languages](https://intl.cloud.tencent.com/document/product/628/35260).
