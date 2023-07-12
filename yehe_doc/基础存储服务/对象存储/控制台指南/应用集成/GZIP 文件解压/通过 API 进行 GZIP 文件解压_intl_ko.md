## 준비 작업

1. GZIP 파일 압축 해제 기능은 SCF(Serverless Cloud Function)를 통해 구현됩니다. 사용하기 전에 COS 콘솔[애플리케이션 통합 - GZIP 파일 압축 해제](https://console.cloud.tencent.com/cos5/application/cosGunzipApi)에서 **GZIP 파일 압축 해제** 함수를 생성해야 합니다. 생성 가이드는 [GZIP 파일 압축 해제](https://intl.cloud.tencent.com/document/product/436/46202)를 참고하십시오.
2. 함수 생성 후 함수 리스트 작업 열의 **사용 안내**에 따라 함수 매개변수 설정을 완료합니다. 구체적인 함수 매개변수 설정은 다음을 참고하십시오. 형식은 **JSON 문자열**입니다.
 - SCF 인증을 선택한 함수의 경우 SCF에서 제공하는 실행 함수(Invoke) 인터페이스를 호출하여 SCF를 실행해야 하며, 그 중 ClientContext 매개변수는 JSON 형식으로 전달됩니다. [함수 매개변수 설정 예시](#1)를 참고하십시오.
 - 인증 면제를 선택한 함수의 경우 해당 API 게이트웨이에 HTTP 요청을 통해 함수를 호출할 수 있습니다.


<span id=1></span>
## 함수 매개변수 예시

>? 실제 사용 시에는 코드에서 주석을 제거해야 합니다.
>

```plaintext
{
    "bucket": "examplebucket-1250000000",    // GZIP 패키지용 원본 버킷
    "region": "ap-guangzhou",         // GZIP 패키지를 보관하는 원본 버킷의 리전
    "key": "example.txt.gz",              //  GZIP 패키지 이름
    "targetBucket": "examplebucket-1250000000",    // 압축 해제 산출이 최종적으로 전송되는 대상 버킷
    "targetRegion": "ap-guangzhou",         // 압축 해제 산출이 최종적으로 전송되는 대상 버킷의 리전
    "targetPrefix": "target/",              // 최종적으로 전송되는 압축 해제 산출물의 접두사
}
```

매개변수 설명은 다음과 같습니다.

| 매개변수 이름                 | 매개변수 설명                                                     | 유형             | 필수 입력 여부 |
| ----------------------- | ------------------------------------------------------------ | ------- | -------- |
| bucket                  | GZIP 패키지를 저장할 원본 버킷. 이름 형식은 BucketName-APPID이며, examplebucket-1250000000과 같은 형식이어야 합니다. | String | Yes       |
| region                  | GZIP 패키지가 저장되어 있는 원본 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes       |
| key                     |  GZIP 패키지 이름(Object의 이름)으로, 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String    | Yes   |
| targetBucket                  | 압축 해제 산출이 최종적으로 전송되는 대상 버킷. 이름 형식은 BucketName-APPID이며, examplebucket-1250000000과 같은 형식이어야 합니다. | String | Yes       |
| targetRegion                  | 압축 해제 산출이 최종적으로 전송되는 대상 버킷의 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes       |
| targetPrefix                     | 최종적으로 전송되는 압축 해제 산출물의 접두사. 지정된 디렉터리로 전달할 때 슬래시 /로 끝나야 합니다. 기본 값 또는 빈 문자열은 루트 경로로 전송되는 것으로 간주됩니다. | String | No       |

## 함수 응답 결과 예시
```plaintext
{
    "code": 0,
    "message": "cos gunzip file success",
    "data":{
        "Bucket": "examplebucket-1250000000",
        "Region": "ap-guangzhou"
    }
}
```

응답 매개변수 설정 설명:

| 매개변수 이름                    | 매개변수 설명                                                     | 유형        |
| ------- | ------------------------------------------------------ | ---------------- |
| code    | 비즈니스 오류 코드. 0이면 실행 성공, 그렇지 않으면 실행 실패    | Number           |
| message | 실행 결과의 텍스트 설명. null일 수 있음                        | String           |
| data    | 실행 성공 정보. 실행이 성공하면 압축 해제된 산출물의 최종 전송 대상 버킷 정보 포함 | Object           |
| error   | 실행 오류 메시지. 실행 성공 시 null                    | Object or String |

## 실제 사례

### 사례1: *.gz 파일 압축 해제

#### 매개변수 설정

```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "example.txt.gz",
  "targetBucket": "examplebucket-1250000000",
  "targetRegion": "ap-guangzhou",
  "targetPrefix": "target/"
}
```

#### 최종 압축 해제 산출물 위치

```plaintext
target/example.txt
```

### 사례2: *.tar.gz 및 *.tgz 파일 압축 해제

#### 매개변수 설정
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "example.tar.gz",
  "targetBucket": "examplebucket-1250000000",
  "targetRegion": "ap-guangzhou",
  "targetPrefix": "target/"
}
```

#### 압축 패키지 구조

```
example.tar.gz
    ├── example-subfile-1.txt
    ├── example-subfile-2.png
    └── example-subfile-3.mp4
```

#### 최종 압축 해제 산출물 위치

```plaintext
target/example-subfile-1.txt
target/example-subfile-2.png
target/example-subfile-3.mp4
```
