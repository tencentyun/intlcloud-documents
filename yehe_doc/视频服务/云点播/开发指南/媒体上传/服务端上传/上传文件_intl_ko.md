## API 설명

- 작은 파일(5MB 미만)을 업로드하는 데 사용되는 API는 [단순 파일 업로드](https://intl.cloud.tencent.com/document/product/436/7749)를 참고하십시오.
- 대용량 파일(5MB 이상)을 업로드하는 데 사용되는 API에 대해서는 [멀티파트 업로드 초기화](https://intl.cloud.tencent.com/document/product/436/7746), [파트 하나씩 업로드](https://intl.cloud.tencent.com/document/product/436/7750) 및 [멀티파트 업로드 종료](https://intl.cloud.tencent.com/document/product/436/7742)를 참고하십시오.

## 기능 설명
1. 미디어(및 커버) 파일을 업로드합니다.
2. API를 사용하여 클라이언트에서 업로드하는 방법은 [클라이언트 업로드 개요](https://intl.cloud.tencent.com/document/product/266/33910)를 참고하십시오.

## SDK 방식
[캡슐화된 SDK](https://intl.cloud.tencent.com/document/product/436/6474)를 사용하여 API를 호출하는 것이 좋습니다.

## API 방식

사용법은 상기 API 링크의 문서를 참고하십시오. 각 API의 구문은 다음과 같습니다.
```
PUT <ObjectName> HTTP/1.1
Host: <BucketName>-<APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

구문의 다음 변수는 [ApplyUpload API](https://intl.cloud.tencent.com/document/product/266/34120)의 반환 결과 값을 사용합니다.  

- `<ObjectName>`은 **MediaStoragePath**(또는 커버 파일용**CoverStoragePath**)입니다.
- `<BucketName>-<APPID>`는 **StorageBucket**입니다.
- `<Region>`는 **StorageRegion**입니다.

API 요청의 경우 다음 사항에 유의하십시오.

- Authorization 서명의 경우 [ApplyUpload API](https://intl.cloud.tencent.com/document/product/266/34120)의 반환 결과에서 **TempCertificate**의 SecretId 및 SecretKey를 사용합니다. 계산 방법은 [서명 요청](https://intl.cloud.tencent.com/document/api/436/7778)을 참고하십시오.
- HTTP 헤더 또는 POST 요청 패킷의 form-data에 **x-cos-security-token** 필드(요청에 사용된 보안 토큰 식별)를 전달하고 **TempCertificate**의 Token 필드 값을 할당합니다.
