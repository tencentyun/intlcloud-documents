## 소개

본 문서는 이미지 영구 처리에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 설명                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [이미지 영구 처리](https://cloud.tencent.com/document/product/436/54050) | COS는 업로드 시 처리 기능을 제공하여, 사용자의 업로드 시 이미지 처리 작업 구현을 돕습니다. 또한, 기존 COS에 저장된 이미지에 처리 작업을 진행하고 그 결과를 COS에 저장할 수 있습니다. |

## 업로드 시 처리

#### 기능 설명

CI가 제공하는 업로드 시 처리 기능은 사용자의 업로드 시 이미지 처리 작업 구현을 돕습니다. 요청 패키지 헤더에 Pic-Operations 항목을 추가하고 해당하는 매개변수를 설정하기만 하면 이미지 업로드 시 이미지 처리를 진행하여 원본 이미지와 작업 결과를 COS에 저장할 수 있습니다. 현재 20M 이하의 파일 처리를 지원합니다.

#### 메소드 프로토타입

```
ci_put_object(self, Bucket, Body, Key, EnableMD5=False, **kwargs)
```

#### 요청 예시

```python
with open('local.jpg', 'rb') as fp:
	response, data = client.ci_put_object(
		Bucket='examplebucket-1250000000',
        Body=fp,
        Key=ci_file_name,
        # pic operation json struct
        PicOperations='{"is_pic_info":1,"rules":[{"fileid":"format.png","rule":"imageView2/format/png"}]}')
```

#### 모든 매개변수 요청 예시

```python
response = client.ci_put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False|True,
    ACL='private'|'public-read',  # 이 매개변수는 ACL이 1000개로 제한되어 있으니 신중히 사용하십시오.
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    ContentLength='123',
    ContentMD5='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    },
    TrafficLimit='1048576'
    PicOperations='{"is_pic_info":1,"rules":[{"fileid":"format.png","rule":"imageView2/format/png"}]}'
)
```

#### 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형       | 필수 입력 여부 |
| ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Bucket             | 버킷 이름. BucketName-APPID로 구성                         | String     | 예       |
| Body               | 업로드하는 객체의 콘텐츠. 파일 스트림 또는 바이트 스트림이 될 수 있음                         | file/bytes | 예       |
| key                | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String     | 예       |
| PicOperations      | CI 이미지 처리 매개변수. [이미지 영구 처리](https://cloud.tencent.com/document/product/436/54050)를 참고하십시오. | String     | 예       |
| EnableMD5          | SDK의 Content-MD5 계산 여부. 기본적으로 비활성화 상태이며, 활성화 시 업로드 시간 증가 | Bool       | 아니요       |
| ACL                | 객체 ACL 설정. 예: 'private', 'public-read'                | String     | 아니요       |
| GrantFullControl   | 권한을 부여받은 계정에 모든 권한 부여. 형식: `id="OwnerUin"`               | String     | 아니요       |
| GrantRead          | 권한을 부여받은 계정에 읽기 권한 부여. 형식: `id="OwnerUin"`                 | String     | 아니요       |
| StorageClass       | 객체의 스토리지 유형 설정. STANDARD, STANDARD_IA, ARCHIVE가 있으며, 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참고 | String     | 아니요       |
| Expires            | Expires 설정                                                 | String     | 아니요       |
| CacheControl       | 캐시 정책. Cache-Control 설정                                 | String     | 아니요       |
| ContentType        | 콘텐츠 유형. Content-Type 설정                                  | String     | 아니요       |
| ContentDisposition | 객체 이름. Content-Disposition 설정                           | String     | 아니요       |
| ContentEncoding    | 인코딩 형식. Content-Encoding 설정                              | String     | 아니요       |
| ContentLanguage    | 언어 유형. Content-Language 설정                              | String     | 아니요       |
| ContentLength      | 전송 길이 설정                                                 | String     | 아니요       |
| ContentMD5         | 검증에 사용할 업로드 객체의 MD5 값 설정                                | String     | 아니요       |
| Metadata           | 사용자 정의 객체 메타데이터. 반드시 x-cos-meta로 시작해야 하며, 그렇지 않을 경우 무시됨 | Dict       | 아니요       |
| TrafficLimit       | 단일 링크의 제한 속도. 단위는 bit/s이며 설정 범위는 819200 - 838860800, 즉 100KB/s - 100MB/s | String     | 아니요       |

PicOperations은 json 형식의 문자열이며, 구체적인 매개변수는 다음과 같습니다.

| 매개변수 이름                   | 설명                                     | 유형  | 필수 입력 여부 |
| ----------- | ------------------------------------------------------------ | ----- | -------- |
| is_pic_info | 원본 이미지 정보 반환 여부. 반환하지 않는 경우: 0 반환하는 경우: 1 기본값: 0 | Int   | 아니요       |
| rules     | 처리 규칙. 규칙과 결과가 일대일로 대응(현재는 규칙 5개까지 지원). 비워 놓을 경우 이미지 처리를 진행하지 않음 | Array | 아니요       |

 rules(json 배열)의 각 항목의 구체적인 매개변수는 다음과 같습니다.

| 매개변수 이름                   | 설명                                 | 유형                           | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| bucket   | 스토리지 결과의 타깃 버킷 이름. 형식은 BucketName-APPID이며, 지정하지 않을 경우 기본적으로 현재 버킷에 저장 | String | 아니요       |
| fileid   | 처리 결과의 파일 경로 이름. `/`로 시작하는 경우 지정 폴더에 저장하며, 그렇지 않을 경우 원본 이미지 파일과 동일한 디렉터리에 저장 | String | 예       |
| rule     | 처리 매개변수. CI의 이미지 처리 API를 참고. 지정 양식으로 처리할 경우, `style/`로 시작하고, 그 뒤에 양식 이름을 추가. 예: 양식 이름이 `test`일 경우, rule 필드는 `style/test` | String | 예       |

#### 반환 결과 설명

원본 이미지 및 처리 정보 가져오기, 유형은 dict:

```python
{
	'OriginalInfo': {
		'Key': 'local.jpg',
		'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/local.jpg',
		'ETag': '"aff1b996bcc63a0f0259df0de2fa989f38c5ce7e"',
		'ImageInfo': {
			'Format': 'JPEG',
			'Width': '300',
			'Height': '168',
			'Quality': '74',
			'Ave': '0x1a3451',
			'Orientation': '0'
		}
	},
	'ProcessResults': {
		'Object': {
			'Key': 'format.png',
			'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/format.png',
			'Format': 'png',
			'Width': '300',
			'Height': '168',
			'Size': '77063',
			'Quality': '74',
			'ETag': '"a07dc5bcfa238e7d23d2d5884da4ac328aaaa9c6"'
		}
	}
}
```

응답 패킷의 구체적인 데이터 콘텐츠는 다음과 같습니다.

| 매개변수 이름     | 유형      | 설명     |
| ------------ | --------- | -------- |
| UploadResult | Container | 원본 이미지 정보 |

 UploadResult 노드 콘텐츠:

| 매개변수 이름     | 유형      | 설명         |
| -------------- | --------- | ------------ |
| OriginalInfo   | Container | 원본 이미지 정보     |
| ProcessResults | Container | 이미지 처리 결과 |

 OriginalInfo 노드 콘텐츠:

| 노드 이름  | 유형      | 설명                                                      |
| --------- | --------- | ---------------------------------------------------------- |
| Key       | String    | 원본 이미지 파일 이름                                                 |
| Location  | String    | 이미지 경로                                                   |
| ImageInfo | Container | 원본 이미지 정보                                               |
| ETag      | String    | 원본 이미지 ETag 정보(처리한 이미지로 원본 이미지를 덮어쓰는 경우, 처리한 이미지의 ETag 정보 |

 ImageInfo 노드 콘텐츠:

| 노드 이름    | 유형   | 설명         |
| ----------- | ------ | ------------ |
| Format      | String | 형식         |
| Width       | Int    | 이미지 폭     |
| Height      | Int    | 이미지 높이     |
| Quality     | Int    | 이미지 품질     |
| Ave         | String | 이미지 메인 컬러   |
| Orientation | Int    | 이미지 회전 각도 |

 ProcessResults 노드 콘텐츠:

| 노드 이름           | 유형      | 설명                            |
| -------- | --------- | ------------------ |
| Object   | Container | 모든 이미지 처리 결과 |

 Object 노드 콘텐츠:

| 노드 이름           | 유형      | 설명                            |
| -------- | ------ | -------------------- |
| Key      | String | 파일 이름               |
| Location | String | 이미지 경로             |
| Format   | String | 이미지 형식             |
| Width    | Int    | 이미지 폭             |
| Height   | Int    | 이미지 높이             |
| Size     | Int    | 이미지 크기             |
| Quality  | Int    | 이미지 품질             |
| ETag     | String | 처리한 이미지의 ETag 정보 |

## 클라우드 데이터 처리

#### 기능 설명

이미지 영구 처리 API는 COS에 저장된 이미지에 처리 작업을 진행하고 그 결과를 COS에 저장할 수 있습니다.

#### 메소드 프로토타입

```
ci_image_process(self, Bucket, Key, **kwargs)
```

#### 요청 예시

```python
response, data = client.ci_image_process(
	Bucket='examplebucket-1250000000',
 	Key=ci_file_name,
    # pic operation json struct
    PicOperations='{"is_pic_info":1,"rules":[{"fileid":"format.png","rule":"imageView2/format/png"}]}')
```

#### 모든 매개변수 요청 예시

```python
response, data = client.ci_image_process(
    Bucket='examplebucket-1250000000',
    Key=ci_file_name,
    # pic operation json struct
    PicOperations='{"is_pic_info":1,"rules":[{"fileid":"format.png","rule":"imageView2/format/png"}]}')
```

#### 매개변수 설명

| 매개변수 이름      | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| ------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket        | 버킷 이름. BucketName-APPID로 구성                         | String | 예       |
| Key           | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String     | 예       |
| PicOperations      | CI 이미지 처리 매개변수. [이미지 영구 처리](https://cloud.tencent.com/document/product/436/54050)를 참고하십시오. | String     | 예       |

PicOperations은 json 형식의 문자열이며, 구체적인 매개변수는 다음과 같습니다.

| 매개변수 이름    | 설명                                                         | 유형  | 필수 입력 여부 |
| ----------- | ------------------------------------------------------------ | ----- | -------- |
| is_pic_info | 원본 이미지 정보 반환 여부. 반환하지 않는 경우: 0 반환하는 경우: 1 기본값: 0 | Int   | 아니요       |
| rules     | 처리 규칙. 규칙과 결과가 일대일로 대응(현재는 규칙 5개까지 지원). 비워 놓을 경우 이미지 처리를 진행하지 않음 | Array | 아니요       |

 rules(json 배열)의 각 항목의 구체적인 매개변수는 다음과 같습니다.

| 매개변수 이름 | 설명                                                         | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| bucket   | 스토리지 결과의 타깃 버킷 이름. 형식은 BucketName-APPID 이며, 지정하지 않을 경우 기본적으로 현재 버킷에 저장 | String | 아니요       |
| fileid   | 처리 결과 파일 경로 이름. `/`로 시작하는 경우 지정 폴더에 저장하며, 그렇지 않을 경우 원본 이미지 파일과 동일한 디렉터리에 저장 | String | 예       |
| rule     | 처리 매개변수. CI의 이미지 처리 API를 참고. 지정 양식으로 처리할 경우, `style/`로 시작하고, 그 뒤에 양식 이름을 추가. 예: 양식 이름이 `test`일 경우, rule 필드는 `style/test` | String | 예       |

#### 반환 결과 설명

가져온 객체의 메타 정보(dict 형식):

```python
{
	'OriginalInfo': {
		'Key': 'local.jpg',
		'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/local.jpg',
		'ETag': '"aff1b996bcc63a0f0259df0de2fa989f38c5ce7e"',
		'ImageInfo': {
			'Format': 'JPEG',
			'Width': '300',
			'Height': '168',
			'Quality': '74',
			'Ave': '0x1a3451',
			'Orientation': '0'
		}
	},
	'ProcessResults': {
		'Object': {
			'Key': 'format.png',
			'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/format.png',
			'Format': 'png',
			'Width': '300',
			'Height': '168',
			'Size': '77063',
			'Quality': '74',
			'ETag': '"a07dc5bcfa238e7d23d2d5884da4ac328aaaa9c6"'
		}
	}
}
```

응답 패킷의 구체적인 데이터 콘텐츠는 다음과 같습니다.

| 매개변수 이름     | 유형      | 설명     |
| ------------ | --------- | -------- |
| UploadResult | Container | 원본 이미지 정보 |

 UploadResult 노드 콘텐츠:

| 매개변수 이름       | 유형      | 설명         |
| -------------- | --------- | ------------ |
| OriginalInfo   | Container | 원본 이미지 정보     |
| ProcessResults | Container | 이미지 처리 결과 |

 OriginalInfo 노드 콘텐츠:

| 노드 이름  | 유형      | 설명                                                       |
| --------- | --------- | ---------------------------------------------------------- |
| Key       | String    | 원본 이미지 파일 이름                                                 |
| Location  | String    | 이미지 경로                                                   |
| ImageInfo | Container | 원본 이미지 정보                                              |
| ETag      | String    | 원본 이미지 ETag 정보(처리한 이미지로 원본 이미지를 덮어쓰는 경우, 처리한 이미지의 ETag 정보 |

 ImageInfo 노드 콘텐츠:

| 노드 이름    | 유형   | 설명         |
| ----------- | ------ | ------------ |
| Format      | String | 형식         |
| Width       | Int    | 이미지 폭     |
| Height      | Int    | 이미지 높이     |
| Quality     | Int    | 이미지 품질     |
| Ave         | String | 이미지 메인 컬러   |
| Orientation | Int    | 이미지 회전 각도 |

 ProcessResults 노드 콘텐츠:

| 노드 이름 | 유형      | 설명               |
| -------- | --------- | ------------------ |
| Object   | Container | 모든 이미지 처리 결과 |

 Object 노드 콘텐츠:

| 노드 이름 | 유형   | 설명                  |
| -------- | ------ | -------------------- |
| Key      | String | 파일 이름               |
| Location | String | 이미지 경로             |
| Format   | String | 이미지 형식             |
| Width    | Int    | 이미지 폭              |
| Height   | Int    | 이미지 높이             |
| Size     | Int    | 이미지 크기             |
| Quality  | Int    | 이미지 품질             |
| ETag     | String | 처리한 이미지의 ETag 정보 |

