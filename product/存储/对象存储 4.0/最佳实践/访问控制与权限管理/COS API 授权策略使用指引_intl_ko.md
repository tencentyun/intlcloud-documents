## 개요
COS에서 임시 키 서비스를 사용할 경우, 서로 다른 COS API 작업은 서로 다른 권한이 필요하며, 하나의 작업 또는 시스템 작업 순서를 동시에 지정할 수 있습니다.

COS API 라이센싱 정책(policy)은 json 문자열입니다. 예를 들어 APPID를 1253653367로, 지역을 `ap-beijing`으로, 버킷을 `example-1253653367`로, 경로 접두사를 `tes`로 업로드 작업 권한을 부여하였다면, 경로 접두사가 `tes2`인 다운로드 작업 권한에 대한 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObject",
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListParts",
        "name/cos:UploadPart",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"
      ]
    }
  ]
}
```

<a id="policy"></a>
#### 라이센싱 정책 요소 설명

| 이름  | 설명 |
| -------- | ------------------------------------------------------------ |
| version  | 정책 문법 버전, 기본으로 2.0입니다. |
| effect   | allow(허용)과 deny(명시적 거부) 두 가지 경우가 있습니다. |
| resource | 라이센싱 작업의 구체적인 데이터는 임의의 리소스, 지정된 경로 접두사의 리소스, 지정된 절대 경로의 리소스 또는 이들의 조합일 수 있습니다. |
| action   | 여기는 필요에 따라 하나 또는 일련의 작업 또는 모든 작업(*)을 지정하는 COS API입니다.       |
|Condition| 제약 조건으로 입력하지 않아도 됩니다. 세부 내용은 [condition](https://intl.cloud.tencent.com/document/product/598/10603#6..E7.94.9F.E6.95.88.E6.9D.A1.E4.BB.B6(condition)) 설명을 참조하십시오.  |

다음과 같이 COS API에 따른 라이센싱 정책을 자세히 소개합니다.

## 서비스 API

### 버킷 리스트 획득

버킷 리스트 획득: Get Service. 작업 권한을 부여하면, 정책의 `action`은 `name/cos:GetService`이고, `resource`는 `*`입니다.

#### 예시

버킷 리스트를 획득 권한을 부여하는 정책에 대한 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetService"
      ],
      "effect": "allow",
      "resource": [
        "*"
      ]
    }
  ]
}
```

## 버킷 API

버킷 API 정책의 `resource`는 다음과 같이 여러 상황으로 요약할 수 있습니다.

- 임의 지역의 버킷을 조작할 수 있습니다. 정책의 `resource`는 `*`입니다.
- 지정된 지역의 버킷만 조작할 수 있습니다. 예를 들어 APPID가 1253653367이고, 지역은 `ap-beijing`인 버킷만 조작할 수 있으면, 정책의 `resource`는 `qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/*`입니다.
- 지정된 지역에 이름을 지정된 버킷만 조작할 수 있습니다. 예를 들어 APPID가 1253653367이고, 지역은 `ap-beijing`이며 이름이 `example-1253653367`인 버킷만 조작할 수 있으면, 정책의 `resource`는 `qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/`입니다.



버킷 API 정책의 `action`은 작업에 따라 값이 달라집니다. 모든 버킷 API 라이센싱 정책은 다음과 같습니다.

### 버킷 생성

버킷 생성: Put Bucket, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:PutBucket`입니다.

#### 예시

APPID가 1253653367이고, `ap-beijing`인 지역에서 임의의 이름의 버킷을 생성할 수 있는 작업 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/*"
      ]
    }
  ]
}
```

### 버킷 조회  

버킷 검색: Head Bucket, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:HeadBucket`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 버킷에 대한 검색 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:HeadBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷 지역 정보 조회

버킷 지역 정보 조회: Get Bucket Location, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:GetBucketLocation`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 버킷의 지역 정보에 대한 조회 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketLocation"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷 객체 리스트 획득

버킷 객체 리스트 획득: Get Bucket, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:GetBucket`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 객체 리스트에 대한 획득 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/*"
      ]
    }
  ]
}
```

### 버킷 삭제

버킷 삭제: Delete Bucket, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:DeleteBucket`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 버킷에 대한 삭제 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteBucket"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷 ACL 설정

버킷 ACL 설정: Put Bucket ACL, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:PutBucketACL`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 ACL에 대한 설정 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucketACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷 ACL 획득

버킷 ACL 획득: Get Bucket ACL, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:GetBucketACL`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 ACL에 대한 획득 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷 CORS 구성 설정

버킷 CORS 구성 설정: Put Bucket CORS, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:PutBucketCORS`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 버킷 크로스 도메인 구성에 대한 설정 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucketCORS"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷 CORS 구성 획득

버킷 CORS 구성 획득: Get Bucket CORS, 해당 권한을 부여하면, 정책의 `action`은 `name/cos:GetBucketCORS`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 버킷 CORS 구성에 대한 획득 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketCORS"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷 CORS 구성 삭제

버킷 CORS 구성 삭제: Delete Bucket CORS, 삭제 권한을 부여하면, 정책의 `action`은 `name/cos:DeleteBucketCORS`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 버킷 크로스 도메인 구성에 대한 삭제 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteBucketCORS"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷 수명 주기 설정

버킷 수명 주기 설정: Put Bucket Lifecycle, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:PutBucketLifecycle`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 수명 주기 구성에 대한 설정 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutBucketLifecycle"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷 수명 주기 획득

버킷 수명 주기 획득: Get Bucket Lifecycle, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:PutBucketLifecycle`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 수명 주기 구성에 대한 획득 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetBucketLifecycle"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷 수명 주기 삭제

버킷 수명 주기 삭제: Delete Bucket Lifecycle, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:DeleteBucketLifecycle`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 수명 주기 구성에 대한 삭제 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteBucketLifecycle"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```

### 버킷에 실행 중인 멀티파트 업로드 정보 획득

버킷에 실행 중인 멀티파트 업로드 정보를 획득: List Multipart Uploads, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:ListMultipartUploads`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`인 버킷에 실행 중인 멀티파트 업로드 정보에 대한 획득 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:ListMultipartUploads"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/"
      ]
    }
  ]
}
```



## 객체 API

객체 API 정책의 `resource`는 다음과 같이 여러 상황으로 요약할 수 있습니다.<br>

- 임의의 객체를 조작할 수 있습니다. 정책의 `resource`는 `*`입니다.
- 지정된 버킷의 임의 객체만 조작할 수 있습니다. 예를 들어 APPID가 1253653367이고, 지역은 `ap-beijing`이며 이름이 `example-1253653367`인 버킷의 임의 객체만 조작할 수 있으면, 정책의 `resource`는 `qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/*`입니다.
- 지정된 버킷과 지정된 경로 접두사에 있는 임의의 객체만 조작할 수 있습니다. 예를 들어 APPID가 1253653367이고, 지역이 `ap-beijing`이며, 버킷이 `example-1253653367`이며, 경로 접두사가 `test`에 있는 임의의 객체만 조작할 수 있다면, 정책의 `resource`는 `qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*`입니다.
- 지정된 절대 경로의 객체만 작업할 수 있습니다. 예를 들어 APPID가 1253653367이고, 지역이 `ap-beijing`이며, 버킷이 `example-1253653367`이며, 경로 경로가 `test/audio.mp3`인 객체만 작업하면, 정책의 `resource`는`qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/audio.mp3`입니다.



객체 API 정책의 `action`은 작업에 따라 값이 달라집니다. 모든 객체 API 라이센싱 정책은 다음과 같습니다.

### 간편 업로드

간편 업로드: Put Object, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:PutObject`가 됩니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사가 `test`인 경우에만 간편 업로드를 할 수 있는 작업 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
 {
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### 멀티파트 업로드

멀티파트 업로드: Initiate Multipar tUpload, List Parts, Upload Part, Complete Multipart Upload, Abort Multipart Upload. 작업 권한을 부여하면, 정책의 `action`은 `"name/cos:InitiateMultipartUpload","name/cos:ListParts","name/cos:UploadPart","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`의 집합이 됩니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사가 `test`인 경우에만 멀티파트 업로드를 할 수 있는 작업 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListParts",
        "name/cos:UploadPart",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Post로 업로드

Post로 업로드: Post Object, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:PostObject`입니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사가 `test`인 경우에만 Post로 업로드를 할 수 있는 작업 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PostObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### 객체 조회

객체 검색: Head Object, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:HeadObject`입니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사가 `test`인 객체에만 검색 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:HeadObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### 객체 다운로드

객체 다운로드: Get Object, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:GetObject`입니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사가 `test`인 객체에만 다운로드 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

##### 간편 복사

간편 복사: Put Object Copy. 작업 권한을 부여하면, 정책의 목표 대상 `action`은 `name/cos:PutObject`이고, 오리진 객체의 `action`은 `name/cos:GetObject`입니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사가 `test` 및 경로 접두사가 `test2` 사이에 간편 업로드를 할 수 있는 작업 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"
      ]
    }
  ]
}
```

그 중 `"qcs::cos:ap-beijing:uid/1253653367 : prefix//1253653367/example/test2/*"`는 오리진 객체입니다.

### 멀티파트 복사

멀티파트 복사: Upload Part Copy, 작업 권한을 부여하면, 정책의 목표 객체 `action`은 `action`: `"name/cos:InitiateMultipartUpload","name/cos:ListParts","name/cos:PutObject", "name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`의 집합이 되고 기존 객체의 `action`은 `name/cos:GetObject`이 됩니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사 `test` 및 경로 접두사 `test2` 사이에 멀티파트 복사를 할 수 있는 작업 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListParts",
        "name/cos:PutObject",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test2/*"
      ]
    }
  ]
}
```

그 중 `"qcs::cos:ap-beijing:uid/1253653367 : prefix//1253653367/example/test2/*"`는 소스 객체입니다.

### 객체 ACL 설정

객체 ACL 설정: Put ObjectACL, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:PutObjectACL`입니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사가 `test`인 객체 ACL에만 설정 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PutObjectACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### 객체 ACL 획득

객체 ACL 획득: Get Object ACL, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:GetObjectACL`입니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사가 `test`인 객체 ACL에만 획득 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:GetObjectACL"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### Options 요청

Options 요청: Options Object, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:OptionsObject`입니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사가 `test`인 경우에만 Options 요청을 할 수 있는 작업 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:OptionsObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### 보관 파일 복구

보관 파일 복구: Post Object Restore, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:PostObjectRestore`입니다.

#### 예시

APPID가 1253653367이며, 지역이 `ap-beijing`이고, 버킷이 `example-1253653367`이며, 경로 접두사가 `test`인 경우에만 보관 복구를 할 수 있는 작업 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:PostObjectRestore"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/test/*"
      ]
    }
  ]
}
```

### 객체 삭제

객체 삭제: Delete Object, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:DeleteObject`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`의 `audio.mp3` 객체에 대한 삭제 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/audio.mp3"
      ]
    }
  ]
}
```

### 객체 배치 삭제

배치로 객체 삭제: Delete Multiple Objects, 작업 권한을 부여하면, 정책의 `action`은 `name/cos:DeleteObject`입니다.

#### 예시

APPID가 1253653367이고, 지역이 `ap-beijing`이며 `example-1253653367`의 `audio.mp3` 및 `video.mp4` 객체에만 대한 배치로 삭제 권한을 부여하며, 세부 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:DeleteObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/audio.mp3",
        "qcs::cos:ap-beijing:uid/1253653367:prefix//1253653367/example/video.mp4"
      ]
    }
  ]
}
```

## 일반 시나리오의 라이센싱 정책

### 모든 리소스에 대해 전체 읽기/쓰기 권한 부여
모든 리소스에 대해 전체 읽기/쓰기 권한을 부여하며, 세부 내용은 다음과 같습니다.
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "*"
      ],
      "effect": "allow",
      "resource": [
        "*"
      ]
    }
  ]
}
```

### 모든 리소스에 대해 전체 읽기 전용 권한 부여
모든 리소스에 대해 전체 읽기 전용 권한을 부여하며, 세부 내용은 다음과 같습니다.
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:Head*",
        "name/cos:Get*",
        "name/cos:List*",
        "name/cos:OptionsObject"
      ],
      "effect": "allow",
      "resource": [
        "*"
      ]
    }
  ]
}
```

### 지정된 경로 접두사에 대해 읽기/쓰기 작업 부여
사용자는 버킷 example-1253653367에 경로 접두사가 userID123456인 파일만 접근할 수 있고, 다른 경로의 파일에 대해서는 작업 권한이 없습니다. 세부 내용은 아래와 같습니다.
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "*"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-shanghai:uid/1253653367:prefix//1253653367/example/userID123456/*"
      ]
    }
  ]
}
```
