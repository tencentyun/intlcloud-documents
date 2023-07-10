## Feature Description

This API (`GeneratePrivateM3U8`) is used to get the download authorization for M3U8 and TS resources.

## Request

#### Sample request

```plaintext
GET /pm3u8?expires=&object= HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-type: application/xml
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Request parameters

The parameters are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| :----------------- | :----- | :---------------------------------- | :-------- | :------- | :------|
| object            | None     | Object name of the M3U8 file | String | Yes       | None |
| expires            | None     | Relative validity period of the download credential for the private TS resource URL in seconds. | String | Yes       | [3600,43200] |


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request does not have a request body.



## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns binary streams. The following example contains all the M3U8 file content:

```plaintext
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:11
#EXT-X-MEDIA-SEQUENCE:0
#EXTINF:11.333333,
test-00000.ts?q-sign-algorithm=sha1&q-ak=&q-sign-time=&q-key-time=&q-header-list=host&q-url-param-list=&q-signature=&x-cos-security-token=
#EXTINF:9.416667,
test-00001.ts?q-sign-algorithm=sha1&q-ak=&q-sign-time=&q-key-time=&q-header-list=host&q-url-param-list=&q-signature=&x-cos-security-token=
#EXTINF:9.375000,
test-00002.ts?q-sign-algorithm=sha1&q-ak=&q-sign-time=&q-key-time=&q-header-list=host&q-url-param-list=&q-signature=&x-cos-security-token=
#EXTINF:11.291667,
test-00003.ts?q-sign-algorithm=sha1&q-ak=&q-sign-time=&q-key-time=&q-header-list=host&q-url-param-list=&q-signature=&x-cos-security-token=
#EXTINF:3.500000,
test-00004.ts?q-sign-algorithm=sha1&q-ak=&q-sign-time=&q-key-time=&q-header-list=host&q-url-param-list=&q-signature=&x-cos-security-token=
#EXT-X-ENDLIST
```


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
GET /pm3u8?expires=3600&object=test.m3u8 HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-type: application/xml
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-ci
x-ci-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZm****

#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:11
#EXT-X-MEDIA-SEQUENCE:0
#EXTINF:11.333333,
test-00000.ts?q-sign-algorithm=sha1&q-ak=AKIDIJinagBeqYfuCEWtH_uG7psMUd7KwrOCNVt9BcEVtxZyh5xHaQLe5YUDpHjfGrfT&q-sign-time=1630396953%3B1630397953&q-key-time=1630396953%3B1630397953&q-header-list=host&q-url-param-list=&q-signature=8a276a2ffd0916e3cd20eea6b1e27e4d76cfebad&x-cos-security-token=vNezC3DD9EDD0zq4uCYCL0F6G7fAvADa726dc8d25238537889b30b03908c3f63vCUb2WUG0VL9dV8ZyypuNd5NOq0jbHoLS22CVn02nT2DohbRGhFlhy3BabKIhp57Ygh-tPeMmwI4HyvjK4RLolrC7kGnYKpCZnwm-j-Np_6RdGU6lsSyrdWXn867w1jUdQVfmillQiLz_dourCyHkTpC4p1yhnmON93WyWsxCzPDKBYCJn03vxW-3HuvPZ_EXdagHcVA21TYU_6AI6Ul6mAby8TVKh1ATl0cHUGh3DZGCPgax9eZyfqhvliAr2OLqEbIexT1qPFDIni4gZytbGCJPUF1C-h-WBLkdEU4sZR7S_PnOhhF6wbvIHCgFlzA6mIb3c5F_FonsHBmk97R-nFegDd5W21hqesT_1fy5JE8qbkYR5jsVKLKVppqsHZZ4xkW62oe5yeoQAA75-NhpfmZtopvWII91Wpen6F9360
#EXTINF:9.416667,
test-00001.ts?q-sign-algorithm=sha1&q-ak=AKIDIJinagBeqYfuCEWtH_uG7psMUd7KwrOCNVt9BcEVtxZyh5xHaQLe5YUDpHjfGrfT&q-sign-time=1630396953%3B1630397953&q-key-time=1630396953%3B1630397953&q-header-list=host&q-url-param-list=&q-signature=f57ad61c6c5b2402b24e35109682a7e107a1b4c3&x-cos-security-token=vNezC3DD9EDD0zq4uCYCL0F6G7fAvADa726dc8d25238537889b30b03908c3f63vCUb2WUG0VL9dV8ZyypuNd5NOq0jbHoLS22CVn02nT2DohbRGhFlhy3BabKIhp57Ygh-tPeMmwI4HyvjK4RLolrC7kGnYKpCZnwm-j-Np_6RdGU6lsSyrdWXn867w1jUdQVfmillQiLz_dourCyHkTpC4p1yhnmON93WyWsxCzPDKBYCJn03vxW-3HuvPZ_EXdagHcVA21TYU_6AI6Ul6mAby8TVKh1ATl0cHUGh3DZGCPgax9eZyfqhvliAr2OLqEbIexT1qPFDIni4gZytbGCJPUF1C-h-WBLkdEU4sZR7S_PnOhhF6wbvIHCgFlzA6mIb3c5F_FonsHBmk97R-nFegDd5W21hqesT_1fy5JE8qbkYR5jsVKLKVppqsHZZ4xkW62oe5yeoQAA75-NhpfmZtopvWII91Wpen6F9360
#EXTINF:9.375000,
test-00002.ts?q-sign-algorithm=sha1&q-ak=AKIDIJinagBeqYfuCEWtH_uG7psMUd7KwrOCNVt9BcEVtxZyh5xHaQLe5YUDpHjfGrfT&q-sign-time=1630396953%3B1630397953&q-key-time=1630396953%3B1630397953&q-header-list=host&q-url-param-list=&q-signature=c38952fae80f9aa22005315c913c8154a780e6a8&x-cos-security-token=vNezC3DD9EDD0zq4uCYCL0F6G7fAvADa726dc8d25238537889b30b03908c3f63vCUb2WUG0VL9dV8ZyypuNd5NOq0jbHoLS22CVn02nT2DohbRGhFlhy3BabKIhp57Ygh-tPeMmwI4HyvjK4RLolrC7kGnYKpCZnwm-j-Np_6RdGU6lsSyrdWXn867w1jUdQVfmillQiLz_dourCyHkTpC4p1yhnmON93WyWsxCzPDKBYCJn03vxW-3HuvPZ_EXdagHcVA21TYU_6AI6Ul6mAby8TVKh1ATl0cHUGh3DZGCPgax9eZyfqhvliAr2OLqEbIexT1qPFDIni4gZytbGCJPUF1C-h-WBLkdEU4sZR7S_PnOhhF6wbvIHCgFlzA6mIb3c5F_FonsHBmk97R-nFegDd5W21hqesT_1fy5JE8qbkYR5jsVKLKVppqsHZZ4xkW62oe5yeoQAA75-NhpfmZtopvWII91Wpen6F9360
#EXTINF:11.291667,
test-00003.ts?q-sign-algorithm=sha1&q-ak=AKIDIJinagBeqYfuCEWtH_uG7psMUd7KwrOCNVt9BcEVtxZyh5xHaQLe5YUDpHjfGrfT&q-sign-time=1630396953%3B1630397953&q-key-time=1630396953%3B1630397953&q-header-list=host&q-url-param-list=&q-signature=b7fed1e31254da2be9c25a662dc4eead2d4dbae7&x-cos-security-token=vNezC3DD9EDD0zq4uCYCL0F6G7fAvADa726dc8d25238537889b30b03908c3f63vCUb2WUG0VL9dV8ZyypuNd5NOq0jbHoLS22CVn02nT2DohbRGhFlhy3BabKIhp57Ygh-tPeMmwI4HyvjK4RLolrC7kGnYKpCZnwm-j-Np_6RdGU6lsSyrdWXn867w1jUdQVfmillQiLz_dourCyHkTpC4p1yhnmON93WyWsxCzPDKBYCJn03vxW-3HuvPZ_EXdagHcVA21TYU_6AI6Ul6mAby8TVKh1ATl0cHUGh3DZGCPgax9eZyfqhvliAr2OLqEbIexT1qPFDIni4gZytbGCJPUF1C-h-WBLkdEU4sZR7S_PnOhhF6wbvIHCgFlzA6mIb3c5F_FonsHBmk97R-nFegDd5W21hqesT_1fy5JE8qbkYR5jsVKLKVppqsHZZ4xkW62oe5yeoQAA75-NhpfmZtopvWII91Wpen6F9360
#EXTINF:3.500000,
test-00004.ts?q-sign-algorithm=sha1&q-ak=AKIDIJinagBeqYfuCEWtH_uG7psMUd7KwrOCNVt9BcEVtxZyh5xHaQLe5YUDpHjfGrfT&q-sign-time=1630396953%3B1630397953&q-key-time=1630396953%3B1630397953&q-header-list=host&q-url-param-list=&q-signature=aedf39d58f5669367f3f6b709238956efe2b9b2f&x-cos-security-token=vNezC3DD9EDD0zq4uCYCL0F6G7fAvADa726dc8d25238537889b30b03908c3f63vCUb2WUG0VL9dV8ZyypuNd5NOq0jbHoLS22CVn02nT2DohbRGhFlhy3BabKIhp57Ygh-tPeMmwI4HyvjK4RLolrC7kGnYKpCZnwm-j-Np_6RdGU6lsSyrdWXn867w1jUdQVfmillQiLz_dourCyHkTpC4p1yhnmON93WyWsxCzPDKBYCJn03vxW-3HuvPZ_EXdagHcVA21TYU_6AI6Ul6mAby8TVKh1ATl0cHUGh3DZGCPgax9eZyfqhvliAr2OLqEbIexT1qPFDIni4gZytbGCJPUF1C-h-WBLkdEU4sZR7S_PnOhhF6wbvIHCgFlzA6mIb3c5F_FonsHBmk97R-nFegDd5W21hqesT_1fy5JE8qbkYR5jsVKLKVppqsHZZ4xkW62oe5yeoQAA75-NhpfmZtopvWII91Wpen6F9360
#EXT-X-ENDLIST
```

