
## 소개

비동기화 풀링 기능은 사용자가 지정한 원본 서버에서 지정한 파일을 가져와 COS에 데이터를 저장할 수 있도록 설계되었습니다. COS의 서비스 역할을 통해 작업을 진행할 수 있으나 그 전에 사용자가 COS 서비스 역할에 해당하는 권한을 부여해야 합니다.

## COS 서비스 역할에 대한 라이선스 

비동기화 풀링 기능으로 특정 원본 서버의 데이터를 지정한 버킷에 업로드하려면 COS 서비스 역할에 대한 라이선스가 필요하며, 사용자는 이에 상응하는 버킷 정책 구문을 버킷에 추가해야 합니다. 정책 구문은 다음과 같습니다.

```
{
      "Statement": [
        {
          "Principal": {
             "service": "cos.qcloud.com"
          },
          "Effect": "Allow",
          "Action": [
             "name/cos:PutObject",
             "name/cos:InitiateMultipartUpload",
             "name/cos:UploadPart",
             "name/cos:CompleteMultipartUpload"
          ],
          "Resource": [
             "qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/*"
          ]
        }
      ],
      "version": "2.0"
}
```

>? 정책 구문에서 수정해야 하는 입력 매개변수는 Resource 필드의 6단식 리소스입니다. Region은 사용자 버킷이 속한 리전으로, APPID는 사용자의 APPID로, BucketName은 사용자의 버킷 이름으로 수정하십시오.
>

광저우 리전의 examplebucket-12500000000을 예로 들면, 루트 디렉터리에 파일을 업로드할 수 있는 라이선스에 다음과 같은 정책 구문을 사용할 수 있습니다.

```
"Resource": [
         "qcs::cos:ap-guangzhou:uid/12500000000:examplebucket-12500000000/*"
]
```

prefix 디렉터리에 파일을 업로드할 수 있는 라이선스에 다음과 같은 정책 구문을 사용할 수 있습니다.

```
"Resource": [
         "qcs::cos:ap-guangzhou:uid/12500000000:examplebucket-12500000000/prefix/*"
]
```

## 사용 방법

### REST API 사용

REST API를 사용해 비동기화 풀링 요청을 보낼 수 있습니다. 자세한 내용은 쿼리 진행률과 오프라인 Origin-pull을 참조하십시오.

### SDK 사용

SDK를 호출하여 비동기화 풀링 작업을 진행할 수 있습니다. 자세한 내용은 [Github 예시](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/demo/fetch_demo.py)를 참조하십시오.

