>! 서브 계정 또는 협업 파트너에게 API 작업 권한 부여 시, 반드시 작업 필요에 따라 최소 권한의 원칙으로 권한을 부여해야 합니다. 서브 계정 또는 협업 파트너에게 직접 모든 리소스`(resource:*)` 또는 모든 작업`(action:*)` 권한을 부여하는 경우 권한 범위가 너무 커 데이터 보안 리스크가 발생할 수 있습니다.
>


## 개요

Cloud Object Storage(COS)에서 임시 키 서비스를 사용할 때 각 COS API 작업 별로 서로 다른 작업 권한이 필요하며, 동시에 1개 작업 또는 일련의 작업을 지정할 수 있습니다.

COS API 권한 부여 정책(policy)은 일종의 JSON 문자열입니다. 예를 들어, APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사가 doc인 업로드 작업(간편 업로드, 폼 업로드, 멀티파트 업로드 등의 작업 포함) 권한을 부여한 경우, 경로 접두사가 doc2인 다운로드 작업 권한의 정책 내용은 다음과 같습니다.
```shell
{
	"version": "2.0",
	"statement": [{
			"action": [
				//간편 업로드 작업 
				"name/cos:PutObject",
				//폼을 사용한 객체 업로드 
				"name/cos:PostObject",
				//멀티파트 업로드: 파트 초기화 작업 
				"name/cos:InitiateMultipartUpload",
				//멀티파트 업로드: List에서 진행 중인 멀티파트 업로드
				"name/cos:ListMultipartUploads",
				//멀티파트 업로드: List에서 업로드 완료한 파트 작업 
				"name/cos:ListParts",
				//멀티파트 업로드: 멀티파트 업로드 작업 
				"name/cos:UploadPart",
				//멀티파트 업로드: 모든 멀티파트 업로드 작업 완료 
				"name/cos:CompleteMultipartUpload",
				//멀티파트 업로드 작업 취소 
				"name/cos:AbortMultipartUpload"
			],
			"effect": "allow",
			"resource": [
				"qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
			]
		},
		{
			"action": [
				//다운로드 작업 
				"name/cos:GetObject"
			],
			"effect": "allow",
			"resource": [
				"qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc2/*"
			]
		}
	]
}
```

<a id="policy"></a>

## 권한 부여 정책(policy) 요소 설명

| 이름     | 설명                                                         |
| -------- | ------------------------------------------------------------ |
| version  | 정책 구문 버전으로, 기본값은 2.0입니다.                                      |
| effect   | allow(허용), deny(명시적 거부) 두 가지 상태가 있습니다.                |
| resource | 모든 리소스, 지정된 경로 접두사가 있는 리소스, 지정된 절대 경로의 리소스 또는 이들의 조합이 될 수 있는 권한 부여된 작업의 특정 데이터입니다.<br><b>참고: </b>경로가 중국어인 경우 중국어 입력을 그대로 유지하십시오. 예: `examplebucket-1250000000/폴더/파일명.txt`. |
| action   | 여기에서는 COS API를 지칭하며, 필요에 따라 1개 또는 일련의 작업 조합이나 모든 작업(`*`)을 지정합니다. 예: `name/cos:GetService`, **영어 대소문자 구분에 유의하십시오**.       |
|condition|규제 조건으로, 입력하지 않아도 됩니다. 자세한 설명은 [condition](https://intl.cloud.tencent.com/document/product/598/10603)을 참고하십시오.  |

각 COS API 별 권한 정책 설정 예시는 다음과 같습니다.

## Service API

### 버킷 리스트 조회

API는 GET Service이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:GetService로 설정하고 resource는 `*`로 설정합니다.

#### 예시 

버킷 리스트 조회 권한을 부여하는 정책의 자세한 내용은 다음과 같습니다.

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

## Bucket API

Bucket API 정책의 resource는 다음과 같을 수 있습니다.

- 모든 리전의 버킷에 대한 작업
정책의 resource를 `*`로 설정하며, **해당 정책에서 한정하는 리소스 범위의 권한 범위가 너무 커 데이터 보안 리스크가 발생할 수 있으므로 설정에 유의하십시오**.
- 특정 리전 버킷의 작업만 허용
APPID가 1250000000이고, 리전이 베이징(ap-beijing)인 버킷 examplebucket-1250000000의 작업만 허용하는 경우, 정책의 resource는 `qcs::cos:ap-beijing:uid/1250000000:*`가 됩니다.
- 특정 리전의 특정 이름 버킷 작업만 허용
APPID가 1250000000이고, 리전이 ap-beijing이며, 이름이 examplebucket-1250000000인 버킷의 작업만 허용하는 경우, 정책의 resource는 `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`가 됩니다.

Bucket API 정책의 action은 작업에 따라 값이 달라집니다. 다음은 Bucket API 권한 부여 정책에 관한 예시로, 기타 Bucket API 권한 부여 정책에 참고할 수 있습니다.

### 버킷 생성 

API는 PUT Bucket이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:PutBucket으로 설정합니다.

#### 예시 

사용자 APPID 1250000000에 버킷 생성 권한을 부여하고, 리전이 베이징 리전이며 버킷 이름이 examplebucket-1250000000인 버킷을 생성할 경우 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

>? 버킷 이름은 이름 생성 규칙에 부합해야 하며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오.
>

### 버킷 및 해당 권한 인덱스  

API는 HEAD Bucket이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:HeadBucket으로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷에 대한 인덱스 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```


### 객체 리스트 쿼리

API는 GET Bucket이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:GetBucket으로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 객체 리스트 조회 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### 버킷 삭제

API는 Delete Bucket이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:DeleteBucket으로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷에 대한 삭제 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### 버킷 ACL 설정 

API는 Put Bucket ACL이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:PutBucketACL로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 ACL 설정 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### 버킷 ACL 조회

API는 GET Bucket acl이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:GetBucketACL로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 ACL 획득 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### 크로스 도메인 구성 설정

API는 PUT Bucket cors이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:PutBucketCORS로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 크로스 도메인 구성 설정 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### 크로스 도메인 설정 조회

API는 GET Bucket cors이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:GetBucketCORS로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 크로스 도메인 설정 조회 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### 크로스 도메인 설정 삭제

API는 DELETE Bucket cors이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:DeleteBucketCORS로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 크로스 도메인 설정 삭제 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### 라이프사이클 설정

API는 PUT Bucket lifecycle이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:PutBucketLifecycle로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 라이프사이클 설정 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### 라이프사이클 조회

API는 GET Bucket lifecycle이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:GetBucketLifecycle로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 라이프사이클 설정 조회 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```

### 라이프사이클 삭제

API는 DELETE Bucket lifecycle이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:DeleteBucketLifecycle로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 라이프사이클 설정 삭제 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```


## Object API

Object API 정책의 resource는 다음과 같을 수 있습니다.

- 모든 객체에 대한 작업을 허용할 경우 정책의 resource를 `*`로 설정합니다.
- 특정 버킷의 모든 객체만 작업할 수 있도록 설정하는 경우, 즉 APPID가 1250000000이고, 리전이 ap-beijing이며, 이름이 examplebucket-1250000000인 버킷의 모든 객체의 작업만 허용하는 경우, 정책의 resource는 `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`가 됩니다.
- 특정 버킷의 특정 경로 접두사의 모든 객체 객체만 작업할 수 있도록 설정하는 경우, 즉 APPID가 1250000000이고, 리전이 ap-beijing이며, 이름이 examplebucket-1250000000인 버킷의 경로 접두사가 doc인 모든 객체의 작업만 허용하는 경우, 정책의 resource는 `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*`가 됩니다.
- 특정 절대 경로의 객체만 작업할 수 있도록 설정하는 경우, 즉 APPID가 1250000000이고, 리전이 ap-beijing이며, 이름이 examplebucket-1250000000인 버킷의 절대 경로가 `doc/audio.mp3`인 객체의 작업만 허용하는 경우, 정책의 resource는 `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/audio.mp3`가 됩니다.


Object API 정책의 action은 작업에 따라 값이 달라지며, 모든 Object API 권한 부여 정책은 다음과 같습니다.

### 객체 간편 업로드

API는 PUT Object이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:PutObject로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc에서의 간편 업로드 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### 멀티파트 업로드 

멀티파트 업로드에는 Initiate Multipart Upload, List Multipart Uploads, List Parts, Upload Part, Complete Multipart Upload, Abort Multipart Upload가 포함되며, 해당 작업 권한을 부여할 경우 정책의 action을 `"name/cos:InitiateMultipartUpload","name/cos:ListMultipartUploads","name/cos:ListParts","name/cos:UploadPart","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`의 집합으로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc에서 멀티파트 업로드 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListMultipartUploads",
        "name/cos:ListParts",
        "name/cos:UploadPart",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### 멀티파트 업로드 조회

버킷의 현재 멀티파트 업로드 중인 정보를 조회하며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:ListMultipartUploads로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 현재 멀티파트 업로드 중인 정보에 대한 조회 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ]
}
```


### HTML 양식을 사용한 객체 업로드

API는 POST Object이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:PostObject로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc에서 POST 업로드 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### 객체 추가 업로드

API는 Append Object이며, 해당 작업 권한을 부여할 경우 정책의 action은 name/cos:AppendObject입니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc에서 추가 업로드 작업 권한을 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

```shell
 {
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:AppendObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### 객체 메타데이터 쿼리

API는 HEAD Object이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:HeadObject로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc의 객체 조회 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### 객체 다운로드

API는 GET Object이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:GetObject로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc의 객체 다운로드 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### 객체 복사

API는 Put Object Copy이며, 해당 작업 권한을 부여할 경우 정책의 타깃 객체의 action을 name/cos:PutObject로 설정하고, 원본 객체의 action을 name/cos:GetObject로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc와 경로 접두사 doc2 간의 멀티파트 복사 작업 권한을 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc2/*"
      ]
    }
  ]
}
```

이 중에서, `"qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc2/*"`는 원본 객체입니다.

### 멀티파트 복사

API는 Upload Part - Copy이며, 해당 작업 권한을 부여할 경우 정책의 타깃 객체의 action은 `"name/cos:InitiateMultipartUpload","name/cos:ListMultipartUploads","name/cos:ListParts","name/cos:PutObject","name/cos:CompleteMultipartUpload","name/cos:AbortMultipartUpload"`의 집합으로 설정하고, 원본 객체의 action은 name/cos:GetObject로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc와 경로 접두사 doc2 간의 멀티파트 복사 작업 권한을 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:InitiateMultipartUpload",
        "name/cos:ListMultipartUploads",
        "name/cos:ListParts",
        "name/cos:PutObject",
        "name/cos:CompleteMultipartUpload",
        "name/cos:AbortMultipartUpload"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    },
    {
      "action": [
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc2/*" 
      ]
    }
  ]
}
```

이 중에서, `"qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc2/*"`는 원본 객체입니다.

### 객체 ACL 설정

API는 Put Object ACL이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:PutObjectACL로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc의 객체 ACL 설정 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### 객체 ACL 조회

API는 Get Object ACL이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:GetObjectACL로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc의 객체 ACL 조회 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### CORS 구성 확인

API는 OPTIONS Object이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:OptionsObject로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc에서 Options 요청 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### 아카이브된 객체 복구

API는 Post Object Restore이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:PostObjectRestore로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 경로 접두사 doc에서 보관 객체 복구 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

### 단일 객체 삭제

API는 DELETE Object이며, 해당 작업 권한을 부여할 경우 정책의 action을 name/cos:DeleteObject로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 audio.mp3 객체에 대한 삭제 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/audio.mp3"
      ]
    }
  ]
}
```

### 다수의 객체 삭제

API는 DELETE Multiple Objects이며, 해당 작업 권한을 부여할 경우 정책의 `action`을 `name/cos:DeleteObject`로 설정합니다.

#### 예시 

APPID가 1250000000이고 리전이 ap-beijing이며 버킷 이름이 examplebucket-1250000000인 버킷의 audio.mp3와 video.mp4 두 가지 객체에 대한 일괄 삭제 작업 권한만 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.

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
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/audio.mp3",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/video.mp4"
      ]
    }
  ]
}
```

## 일반적인 시나리오 권한 부여 정책

### 모든 리소스에 대한 완전한 읽기 권한 부여
모든 리소스에 대한 완전한 읽기 권한을 부여하는 정책의 자세한 내용은 다음과 같습니다.
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

### 모든 리소스에 대한 읽기 전용 권한 부여
모든 리소스에 대한 읽기 전용 권한을 부여하는 정책의 자세한 내용은 다음과 같습니다.
```shell
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "name/cos:HeadObject",
        "name/cos:GetObject",
        "name/cos:GetBucket",
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

### 특정 경로 접두사에 대한 읽기 권한 부여
사용자에게 examplebucket-1250000000 버킷의 경로 접두사 doc 아래의 파일만 액세스할 수 있고 다른 경로의 파일은 작업할 수 없도록 권한을 부여할 경우 해당 정책의 자세한 내용은 다음과 같습니다.
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
        "qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/*"
      ]
    }
  ]
}
```

