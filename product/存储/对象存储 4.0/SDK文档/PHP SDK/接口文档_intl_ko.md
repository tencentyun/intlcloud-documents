## 기본 API 설명
> 본문에서 나오는 SecretId, SecretKey, Bucket 등과 같은 이름의 의미 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

### 버킷 리스트 획득
#### 방식 프로토타입
```php
public Guzzle\Service\Resource\Model listBucket(array $args = array())
```

#### 요청 예시

```php
//버킷 리스트 획득
$result = $cosClient->listBuckets();
```
#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [Owner] => Array
                (
                    [ID] => qcs::cam::uin/3210232098:uin/3210232098
                    [DisplayName] => 3210232098
                )

            [Buckets] => Array
                (
                    [0] => Array
                        (
                            [Name] => accesslog-10055004
                            [Location] => ap-shanghai
                            [CreationDate] => 2016-07-29T03:09:54Z
                        )

                    [1] => Array
                        (
                            [Name] => accesslogbj-10055004
                            [Location] => ap-beijing
                            [CreationDate] => 2017-08-02T04:00:24Z
                        )

                )

            [RequestId] => NWE3YzgxZmFfYWZhYzM1MGFfMzc3MF9iOGY5OQ==
        )

)
```
### 버킷 생성

#### 방식 프로토타입

```php
// 버킷 생성
public Guzzle\Service\Resource\Model createBucket(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :---------: |    :-----------------: | :--------:   | :-------------: |
| Bucket   |      버킷 이름    |    string     |  예         |
| Acl      |         ACL 권한 제어        |    string     | 아니요           |

#### 요청 예시

```php
//버킷 생성
//bucket의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다
$result = $cosClient->createBucket(array('Bucket' => 'testbucket-125000000'));
```
#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [Location] =>
            [RequestId] => NWE3YzgzMTZfMTdiMjk0MGFfNTQ1OF8xNjEyYmE=
        )
)
```
### 버킷 삭제

#### 방식 프로토타입

```php
// 버킷 삭제
public Guzzle\Service\Resource\Model deleteBucket(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: |    :------------: |  :--------:   | :----------------------------------: |
| Bucket  |  버킷 이름        |     string         |         예                     |

#### 요청 예시

```php
//버킷 삭제
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다.
$result = $cosClient->deleteBucket(array('Bucket' => 'testbucket-125000000'));
```
#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestId] => NWE3YzgzMTZfMTdiMjk0MGFfNTQ2MF8xNjBjZTI=
        )
)
```
### 파일 간편 업로드

#### 방식 프로토타입

```php
public Guzzle\Service\Resource\Model putObject(array $args = array())
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| -------------- | -------------- |---------- | ----------- |
 |  Bucket  |  버킷 이름이며, 숫자 및 소문자와 대시 "-"로 구성됩니다 | string |   예 |
 |  Body  | 업로드 파일의 내용이며, 파일 스트림 또는 바이트 스트림이 가능합니다 |  file/string |  예 |
 |  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예 |
 |  ACL  | 파일의 ACL 설정, 예: 'private', 'public-read', 'public-read-write' | string | 아니요 |
 |  GrantFullControl  | 지정 계정에 파일에 대한 읽기/쓰기 권한을 부여합니다 |  string |  아니요 |
 |  GrantRead  |  지정 계정에 파일에 대한 읽기 권한을 부여합니다 | string |  아니요 |
 |  GrantWrite  |  지정 계정에 파일에 대한 쓰기 권한을 부여합니다 | string |  아니요 |
 | StorageClass  | 파일의 스토리지 클래스, STANDARD, STANDARD_IA를 설정합니다. 기본값: STANDARD | String      | 아니요   |
 |  Expires  | Content-Expires를 설정합니다 | string |  아니요 |
 |  CacheControl  |  캐시 정책, Cache-Control을 설정합니다 | string |   아니요 |
 |  ContentType  | 콘텐츠 유형, Content-Type을 설정합니다 |string |   아니요 |  
 |  ContentDisposition  |  파일 이름, Content-Disposition을 설정합니다 | string |   아니요 |
 |  ContentEncoding  |  인코딩 형식, Content-Encoding을 설정합니다 | string |   아니요 |
 |  ContentLanguage  |  언어 유형이며, Content-Language를 설정합니다 | string |   아니요 |
 |  ContentLength  | 전송 길이를 설정합니다 | string |   아니요 |
 |  ContentMD5  | 업로드 파일의 MD5 값을 인증에 사용하도록 설정합니다 | string |   아니요 |
 | Metadata | 사용자의 사용자 지정 파일 메타 정보 | array | 아니요   |
 | ServerSideEncryption | 서버 암호화 방법 | string |   아니요 |

#### 요청 예시
```php
# 파일 업로드
## putObject(파일 업로드 API, 최대 5G 파일 업로드 지원).
## 현재 접근 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 버킷 권한은 승계됩니다.
### 업로드 메모리의 문자열.
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => 'Hello World!'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### 업로드 파일 스트림
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => fopen($local_path, 'rb')));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### header 및 meta 설정
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => fopen($local_path, 'rb'),
        'CacheControl' => 'string',
        'ContentDisposition' => 'string',
        'ContentEncoding' => 'string',
        'ContentLanguage' => 'string',
        'ContentLength' => integer,
        'ContentType' => 'string',
        'Expires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
        'GrantFullControl' => 'string',
        'GrantRead' => 'string',
        'GrantWrite' => 'string',
        'Metadata' => array(
            'string' => 'string',
        ),
        'StorageClass' => 'string'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [Expiration] =>
            [ETag] => "ed076287532e86365e841e92bfc50d8c"
            [ServerSideEncryption] => AES256
            [VersionId] =>
            [SSECustomerAlgorithm] =>
            [SSECustomerKeyMD5] =>
            [SSEKMSKeyId] =>
            [RequestCharged] =>
            [RequestId] => NWE3Yzg0M2NfOTcyMjViNjRfYTE1YV8xNTQzYTY=
            [ObjectURL] => http://testbucket-1252448703.cos.cn-south.myqcloud.com/11%2F%2F32%2F%2F43
        )
)
```

### 멀티파트 업로드

멀티파트 업로드는 파일을 여러 개의 작은 파트로 나누어 업로드를 진행합니다. 여러 개의 작은 파트를 동시에 업로드할 수 있이며, 최대 40TB까지 지원합니다.

멀티파트 파일 업로드의 절차:

1. 멀티파트 업로드를 초기화하고, uploadid를 획득합니다(createMultipartUpload).
2. 파트로 데이터를 업로드합니다(동시 업로드 가능)(uploadPart).
3. 멀티파트 업로드를 완료합니다(completeMultipartUpload).

또한 이미 업로드한 파트를 획득(listParts) alc 멀티파트 업로드를 정지(abortMultipartUpload)가 포함됩니다.

#### 방식 프로토타입

```php
// 멀티파트 업로드 초기화
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());

// 데이터 파트 업로드
public Guzzle\Service\Resource\Model uploadPart(array $args = array());

// 멀티파트 업로드 완료
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());

// 업로드된 파트 나열
public Guzzle\Service\Resource\Model listParts(array $args = array());

// 멀티파트 업로드 정지
public Guzzle\Service\Resource\Model abortMultipartUpload(array $args = array());
```
### 파일 업로드
#### 요청 예시
```php
## Upload(고급 업로드 API, 기본 설정은 멀티파트 업로드이며 최대 50TB 지원).
## 현재 접근 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 버킷 권한은 승계됩니다.
### 업로드 메모리의 문자열
try {
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = 'Hello World!');
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### 업로드 파일 스트림
try {
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = fopen($local_path, 'rb'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### header 및 meta 설정
try {
    $result = $cosClient->Upload(
        $bucket= $bucket,
        $key = $key,
        $body = fopen($local_path, 'rb'),
        $options = array(
            'CacheControl' => 'string',
            'ContentDisposition' => 'string',
            'ContentEncoding' => 'string',
            'ContentLanguage' => 'string',
            'ContentLength' => integer,
            'ContentType' => 'string',
            'Expires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
            'GrantFullControl' => 'string',
            'GrantRead' => 'string',
            'GrantWrite' => 'string',
            'Metadata' => array(
                'string' => 'string',
            ),
            'StorageClass' => 'string'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

```

>?단일 파일이 5M보다 작을 경우, 단일 파일 업로드를 사용하고 그렇지 않으면 멀티파트 로 업로드를 사용합니다.

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [Location] => testbucket-1252448703.cos.cn-south.myqcloud.com/111.txt
            [Bucket] => testbucket
            [Key] => 111.txt
            [ETag] => "715691804ee474f2eb94adb2c5c01155-1"
            [Expiration] =>
            [ServerSideEncryption] => AES256
            [VersionId] =>
            [SSEKMSKeyId] =>
            [RequestCharged] =>
            [RequestId] => NWE3Yzg0YTRfOTUyMjViNjRfNWYyZF8xNTI5ZDQ=
        )
)
```
### 파일 다운로드

파일을 로컬에 다운로드하거나 메모리에 다운로드합니다.

#### 방식 프로토타입

```php
// 파일을 다운로드합니다.
public Guzzle\Service\Resource\Model getObject(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: |    :------------:   | :--------:   | :----------------------------------: |
| Bucket   |      버킷 이름    |    string     |  예         |       
| Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |       
| SaveAs   |   로컬에 저장한 로컬 파일 경로                 |   string      | 예           |
| VersionId     |   객체 버전 번호        |   string      | 예           |       

#### 요청 예시

```php
# 파일 다운로드
## getObject(파일 다운로드)
### 메모리에 다운로드
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key));
    echo($result['Body']);
} catch (\Exception $e) {
    echo "$e\n";
}

### 로컬에 다운로드
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}

### 다운로드 범위 지정
/*
 * Range 필드 형식은 'bytes=a-b'입니다
 */
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Range' => 'bytes=0-10',
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}

### 반환 header 설정
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'ResponseCacheControl' => 'string',
        'ResponseContentDisposition' => 'string',
        'ResponseContentEncoding' => 'string',
        'ResponseContentLanguage' => 'string',
        'ResponseContentType' => 'string',
        'ResponseExpires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}
```
#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [Body] =>
            [DeleteMarker] =>
            [AcceptRanges] => bytes
            [Expiration] =>
            [Restore] =>
            [LastModified] => Fri, 09 Feb 2018 01:10:56 GMT
            [ContentLength] => 5242880
            [ETag] => "715691804ee474f2eb94adb2c5c01155-1"
            [MissingMeta] =>
            [VersionId] =>
            [CacheControl] => private
            [ContentDisposition] => attachment; filename*="UTF-8''111.txt"
            [ContentEncoding] =>
            [ContentLanguage] =>
            [ContentRange] =>
            [ContentType] => text/plain; charset=utf-8
            [Expires] =>
            [WebsiteRedirectLocation] =>
            [ServerSideEncryption] => AES256
            [SSECustomerAlgorithm] =>
            [SSECustomerKeyMD5] =>
            [SSEKMSKeyId] =>
            [StorageClass] =>
            [RequestCharged] =>
            [ReplicationStatus] =>
            [RequestId] => NWE3Yzg4ODlfMThiMjk0MGFfMmI3OV8xNWQxNDg=
        )
)
```

### 파일 삭제

COS의 객체를 삭제합니다.

#### 방식 프로토타입

```php
// 파일 삭제
public Guzzle\Service\Resource\Model deleteObject(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |                버킷 이름               |   string     |  예           |
| Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 액세스 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |   
| VersionId     |   객체 버전 번호        |   string      | 아니요           |  

#### 요청 예시

```php
// COS 객체 삭제
$result = $cosClient->deleteObject(array(
    //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
    'Bucket' => 'testbucket-125000000',
    'Key' => 'hello.txt'));
```
#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [DeleteMarker] =>
            [VersionId] =>
            [RequestCharged] =>
            [RequestId] => NWE3Yzg5MzJfY2FhMzNiMGFfNDVjOV8yY2QyMzg=
        )
)
```


### 객체 속성 획득

COS의 객체 속성을 조회합니다.

#### 방식 프로토타입

```php
// 파일 속성 획득
public Guzzle\Service\Resource\Model headObject(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |   
| Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 액세스 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |    
| VersionId     |   객체 버전 번호        |   string      | 아니요           |

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [DeleteMarker] =>
            [AcceptRanges] =>
            [Expiration] =>
            [Restore] =>
            [LastModified] => Thu, 08 Feb 2018 17:34:53 GMT
            [ContentLength] => 12
            [ETag] => "ed076287532e86365e841e92bfc50d8c"
            [MissingMeta] =>
            [VersionId] =>
            [CacheControl] =>
            [ContentDisposition] =>
            [ContentEncoding] =>
            [ContentLanguage] =>
            [ContentType] => application/octet-stream
            [Expires] =>
            [WebsiteRedirectLocation] =>
            [ServerSideEncryption] => AES256
            [SSECustomerAlgorithm] =>
            [SSECustomerKeyMD5] =>
            [SSEKMSKeyId] =>
            [StorageClass] =>
            [RequestCharged] =>
            [ReplicationStatus] =>
            [RequestId] => NWE3YzhhM2RfMWViZTk0MGFfNWMzMF8xNTFiZDg=
        )
)
```

#### 요청 예시

```php
// COS 파일 속성 획득
 //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
$result $cosClient->headObject(array('Bucket' => 'testbucket-125000000', 'Key' => 'hello.txt'));
```

### 버킷 존재 여부 조회

COS에서의 버킷이 있는지롤 조회합니다.

#### 방식 프로토타입

```php
// 파일 속성 획득
public Guzzle\Service\Resource\Model headBucket(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |     객체 버전 번호      |   string   | 예           |      



#### 요청 예시

```php
// COS 파일 속성 획득
 //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
$result $cosClient->headBucket(array('Bucket' => 'testbucket-125000000'));
```
#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestId] => NWE3YzhhN2VfY2VhMzNiMGFfMmNmXzJjNzc3Zg==
        )
)
```

### 파일 리스트 획득

COS의 파일 리스트를 조회합니다.

#### 방식 프로토타입


```php
// 파일 리스트 획득
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |     
| Delimiter      |      구분 기호         |    string     |  아니요          |    
| Marker      |          ID        |   string     |  아니요          |
| MaxKeys      |           최대 객체 개수         |  int     |   아니요          |
| Prefix      |            접두사         |string     |  아니요           |  

#### 요청 예시

```php
// 버킷 하의 멤버를 획득합니다.
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다.
$result = $cosClient->listObjects(array('Bucket' => 'testbucket-125000000'));
```
#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [Name] => testbucket-1252448703
            [Prefix] =>
            [Marker] =>
            [MaxKeys] => 1000
            [IsTruncated] =>
            [Contents] => Array
                (
                    [0] => Array
                        (
                            [Key] => 11/32/43
                            [LastModified] => 2018-02-08T17:09:16.000Z
                            [ETag] => "ed076287532e86365e841e92bfc50d8c"
                            [Size] => 12
                            [Owner] => Array
                                (
                                    [ID] => 1252448703
                                    [DisplayName] => 1252448703
                                )

                            [StorageClass] => STANDARD
                        )

                    [1] => Array
                        (
                            [Key] => 111
                            [LastModified] => 2018-02-08T17:41:11.000Z
                            [ETag] => "ed076287532e86365e841e92bfc50d8c"
                            [Size] => 12
                            [Owner] => Array
                                (
                                    [ID] => 1252448703
                                    [DisplayName] => 1252448703
                                )

                            [StorageClass] => STANDARD
                        )

                    [2] => Array
                        (
                            [Key] => 111.txt
                            [LastModified] => 2018-02-08T17:11:00.000Z
                            [ETag] => "715691804ee474f2eb94adb2c5c01155-1"
                            [Size] => 5242880
                            [Owner] => Array
                                (
                                    [ID] => 1252448703
                                    [DisplayName] => 1252448703
                                )

                            [StorageClass] => STANDARD
                        )

                )

            [RequestId] => NWE3YzhiYjdfMWJiMjk0MGFfMzA4M18xNjdiNDM=
        )
)
```

### putBucketACL

#### 방식 프로토타입

```php
// 버킷의 권한 리스트 설정
public Guzzle\Service\Resource\Model putBucketAcl(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     | 예         |
| ACL      |         ACL 권한 제어        |    string     | 아니요           |   
| GrantRead |       권한 부여받은 자에게 읽기 권한을 부여합니다. 형식: `id=" ",id=" ", 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>", 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>", 예: 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'         |  string       | 아니요           |     
| GrantWrite |     권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: `id=" ",id=" ", 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>", 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>", 예: 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'         |  string       | 아니요           |      
| GrantFullControl |     권한 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식: `id=" ",id=" ", 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>", 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>”", 예: 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'         |  string       | 아니요           |          


#### 요청 예시

```php
#putBucketACL
try {
    $result = $cosClient->putBucketAcl(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' => 'testbucket-125000000',
        'Grants' => array(
            array(
                'Grantee' => array(
                    'DisplayName' => 'qcs::cam::uin/327874225:uin/327874225',
                    'ID' => 'qcs::cam::uin/327874225:uin/327874225',
                    'Type' => 'CanonicalUser',
                ),
                'Permission' => 'FULL_CONTROL',
            ),
            // ... repeated
        ),
        'Owner' => array(
            'DisplayName' => 'qcs::cam::uin/3210232098:uin/3210232098',
            'ID' => 'qcs::cam::uin/3210232098:uin/3210232098',
        ),));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestId] => NWE3YzhiZTZfZDRiMjk0MGFfODMwXzJjODllYw==
        )
)
```


### getBucketACL
#### 방식 프로토타입

```php
// 버킷의 권한 리스트 획득
public Guzzle\Service\Resource\Model getBucketAcl(array $args = array());
```

#### 요청 매개변수

| 필드 이름   |       유형     | 기본값 | 필수 입력 필드 여부 |                  설명                  |
| :------: |    :------------: | :--:   | :--------:   | :----------------------------------: |
| Bucket   |     string     |  없음    | 예           |               버킷 이름               |



#### 요청 예시
```php
#getBucketACL
try {
    $result = $cosClient->getBucketAcl(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' => 'testbucket-125000000',));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [Owner] => Array
                (
                    [ID] => qcs::cam::uin/3210232098:uin/3210232098
                    [DisplayName] => qcs::cam::uin/3210232098:uin/3210232098
                )

            [Grants] => Array
                (
                    [0] => Array
                        (
                            [Grantee] => Array
                                (
                                    [ID] => qcs::cam::uin/327874225:uin/327874225
                                    [DisplayName] => qcs::cam::uin/327874225:uin/327874225
                                )

                            [Permission] => FULL_CONTROL
                        )

                )

            [RequestId] => NWE3YzhjMTRfYzdhMzNiMGFfYjdiOF8yYzZmMzU=
        )
)
```

### putObjectACL

현재 접근 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 Bucket 권한은 계승됩니다.

#### 방식 프로토타입

```php
// 객체의 권한 리스트 설정
public Guzzle\Service\Resource\Model putObjectAcl(array $args = array());
```

#### 요청 매개변수
| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     | 예         |
 |  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예 |
| ACL      |         ACL 권한 제어        |    string     | 아니요           |   
| GrantRead |       권한 부여받은 자에게 읽기 권한을 부여합니다. 형식: `id=" ",id=" ", 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>", 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>", 예: 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'         |  string       | 아니요           |     
| GrantWrite |     권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: `id=" ",id=" ", 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>", 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>", 예: 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'         |  string       | 아니요           |      
| GrantFullControl |     권한 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식: `id=" ",id=" ", 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>", 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>”", 예: 'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'         |  string       | 아니요           |          


#### 요청 예시
```php
#putObjectACL
try {
    $result = $cosClient->putObjectAcl(array(
        'Bucket' => 'testbucket-1252448703',
        'Key' => '111.txt',
        'Grants' => array(
            array(
                'Grantee' => array(
                    'DisplayName' => 'qcs::cam::uin/327874225:uin/327874225',
                    'ID' => 'qcs::cam::uin/327874225:uin/327874225',
                    'Type' => 'CanonicalUser',
                ),
                'Permission' => 'FULL_CONTROL',
            ),
            // ... repeated
        ),
        'Owner' => array(
            'DisplayName' => 'qcs::cam::uin/3210232098:uin/3210232098',
            'ID' => 'qcs::cam::uin/3210232098:uin/3210232098',
        ),));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] =>
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### getObjectACL
#### 방식 프로토타입

```php
// 객체의 권한 리스트 획득
public Guzzle\Service\Resource\Model getObjectAcl(array $args = array());
```

#### 요청 매개변수

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |        
| Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 액세스 도메인 이름  bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg  중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |        

#### 요청 예시
```php
#getObjectACL
try {
    $result = $cosClient->getObjectAcl(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' => 'testbucket-125000000',
        'Key' => '11'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [Owner] => Array
                (
                    [ID] => qcs::cam::uin/3210232098:uin/3210232098
                    [DisplayName] => qcs::cam::uin/3210232098:uin/3210232098
                )

            [Grants] => Array
                (
                    [0] => Array
                        (
                            [Grantee] => Array
                                (
                                    [ID] => qcs::cam::uin/327874225:uin/327874225
                                    [DisplayName] => qcs::cam::uin/327874225:uin/327874225
                                )

                            [Permission] => FULL_CONTROL
                        )

                )

            [RequestCharged] =>
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjU5OF8yYzlkMmE=
        )
)
```

### putBucketCors
#### 방식 프로토타입

```php
// 버킷의 CORS 구성 설정
public Guzzle\Service\Resource\Model putBucketCors(array $args = array());
```
#### 요청 매개변수

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |         
| CORSRules |        CORS 규칙        |    array     | 예            |
| AllowedMethods |      허용된 HTTP 조작, 열거형 값: GET, PUT, HEAD, POST, DELETE       | array  | 아니요   |  
| AllowedOrigins |     허용된 액세스 리소스, 와일드카드 *를 지원합니다. 형식은 프로토콜: //도메인 이름[:포트] 예: http://www.qq.com        | array  | 아니요   |
| AllowedHeaders | OPTIONS 요청 발송 시 다음 요청에 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있는지 서버에 알리며, [ * ] 와일드카드를 지원합니다 | array  | 아니요   |    
| ExposeHeaders  | 브라우저가 수신할 수 있는 서버의 사용자 지정 헤더 정보 설정           | array  | 아니요   |   
| MaxAgeSeconds  | OPTIONS 요청이 얻은 결과의 유효기간 설정                            | string | 아니요   |       
| ID | 규칙 ID 구성       | string   | 아니요           |    

#### 요청 예시
```php
###putBucketCors
try {
    $result = $cosClient->putBucketCors(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' => 'testbucket-125000000',
        // CORSRules is required
        'CORSRules' => array(
            array(
                'AllowedHeaders' => array('*',),
            // AllowedMethods is required
            'AllowedMethods' => array('Put', ),
            // AllowedOrigins is required
            'AllowedOrigins' => array('*', ),
            'ExposeHeaders' => array('*', ),
            'MaxAgeSeconds' => 1,
        ),
        // ... repeated
    ),
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] =>
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### getBucketCors
#### 방식 프로토타입

```php
// 버킷의 CORS 구성 획득
public Guzzle\Service\Resource\Model getBucketCors(array $args = array());
```
#### 요청 매개변수



| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |


#### 요청 예시
```php
#getBucketCors
try {
    $result = $cosClient->getBucketCors(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' => 'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [CORSRules] => Array
                (
                    [0] => Array
                        (
                            [ID] => 1234
                            [AllowedHeaders] => Array
                                (
                                    [0] => *
                                )

                            [AllowedMethods] => Array
                                (
                                    [0] => PUT
                                )

                            [AllowedOrigins] => Array
                                (
                                    [0] => http://www.qq.com
                                )

                        )

                )

            [RequestId] => NWE3YzhkMmRfMTdiMjk0MGFfNTQzZl8xNWUwMGU=
        )
)
```

### deleteBucketCors
#### 방식 프로토타입

```php
// 버킷의 CORS 구성 삭제
public Guzzle\Service\Resource\Model deleteBucketCors(array $args = array());
```
#### 요청 매개변수

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |


#### 요청 예시
```php
#deleteBucketCors
try {
    $result = $cosClient->deleteBucketCors(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' => 'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] =>
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### putBucketReplication
#### 방식 프로토타입

```php
// 버킷의 크로스 도메인 복사 구성 설정
public Guzzle\Service\Resource\Model putBucketReplication(array $args = array());
```
#### 요청 매개변수

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |         
| Role  | 개시자 ID, 형식: qcs::cam::uin/<OwnerUin>:uin/<SubUin> | string     |  예             |
| Rules | 구체적인 구성 정보, 최대 1000개 지원      |    array   |  예           |  
| ID | 구체적인 Rule의 이름 표시에 사용       |   string   | 예           |
| Status | Rule 유효 여부 표시, 열거형 값: Enabled, Disabled      |   String    |   예        |    
| Prefix      |     접두사 매칭 정책, 중첩할 수 없으며 중첩 시 오류가 반환됩니다. 접두사 매칭 루트 디렉터리는 비어있습니다       |    string    | 예           |   
| Destination |   대상 버킷 정보    |   array       |  예          |       
| Bucket  | 리소스 식별자: qcs::cos:[region]::[bucketname-AppId]    |   array       |  예          |       
| StorageClass | 스토리지 클래스, 열거형 값: STANDARD, STANDARD_IA, NEARLINE, 기본값: 원래 버킷 클래스    |   array       |  아니요          |      

#### 요청 예시
```php
###putBucketCors
try {
    $result = $cosClient->PutBucketReplication(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' => 'testbucket-125000000',
        'Role' => 'qcs::cam::uin/320000000:uin/320000000',
        'Rules'=>array(
            array(
                'Status' => 'Enabled',
                'ID' => 'string',
                'Prefix' => 'string',
                'Destination' => array(
                    'Bucket' => 'qcs::cos:ap-guangzhou::testbucket01-125000000',
                    'StorageClass' => 'standard',
                ),
                // ...repeated
            ),
        ),
    ));
    print_r($result);
} catch (\Exception $e) {
    echo($e);
}
```
#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### getBucketReplication
#### 방식 프로토타입

```php
// 버킷의 크로스 도메인 복사 구성 획득
public Guzzle\Service\Resource\Model getBucketReplication(array $args = array());
```
#### 요청 매개변수



| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |


#### 요청 예시
```php
#getBucketReplication
try {
    $result = $cosClient->GetBucketReplication(array(
        'Bucket' => 'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo($e);
}
```

#### 결과 반환 예제
```php
Array
(
	[data:protected] => Array
	(
	    [Role] => qcs::cam::uin/320000000:uin/320000000
	    [Rules] => Array
	        (
	            [0] => Array
	                (
	                    [ID] => string
	                    [Status] => Enabled
	                    [Prefix] => string
	                    [Destination] => Array
	                        (
	                            [Bucket] => qcs::cos:ap-guangzhou::testbucket01-125000000
	                            [StorageClass] => Standard
	                        )

	                )

	        )

	    [RequestId] => NWI2YWFlN2NfMjNiMjM1MGFfNTQ0OF80NzMzNWY=
	)
)
```

### deleteBucketReplication
#### 방식 프로토타입

```php
// 버킷의 크로스 도메인 복사 구성 삭제
public Guzzle\Service\Resource\Model deleteBucketReplication(array $args = array());
```
#### 요청 매개변수

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |  


#### 요청 예시
```php
#deleteBucketReplication
try {
    $result = $cosClient->deleteBucketReplication(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' => 'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### 객체 복사
#### 방식 프로토타입

```php
//객체 복사
public Guzzle\Service\Resource\Model copyObject(array $args = array());
```

#### 요청 매개변수
| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  |  버킷 이름이며, 숫자 및 소문자와 대시 "-"로 구성됩니다 | string |   예 |
|  CopySource  | 소스 복사     |  string |  예 |
|  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예 |
|  ACL  | 파일의 ACL 설정, 예: 'private', 'public-read', 'public-read-write' | string | 아니요 |
|  GrantFullControl  | 지정 계정에 파일에 대한 읽기/쓰기 권한을 부여합니다 |  string |  아니요 |
|  GrantRead  |  지정 계정에 파일에 대한 읽기 권한을 부여합니다 | string |  아니요 |
|  GrantWrite  |  지정 계정에 파일에 대한 쓰기 권한을 부여합니다 | string |  아니요 |
| StorageClass  | 파일의 스토리지 클래스, STANDARD, STANDARD_IA를 설정합니다. 기본값: STANDARD | String      | 아니요   |
|  Expires  | Content-Expires를 설정합니다 | string |  아니요 |
|  CacheControl  |  캐시 정책, Cache-Control을 설정합니다 | string |   아니요 |
|  ContentType  | 콘텐츠 유형, Content-Type을 설정합니다 |string |   아니요 |  
|  ContentDisposition  |  파일 이름, Content-Disposition을 설정합니다 | string |   아니요 |
|  ContentEncoding  |  인코딩 형식, Content-Encoding을 설정합니다 | string |   아니요 |
|  ContentLanguage  |  언어 유형이며, Content-Language를 설정합니다 | string |   아니요 |
|  ContentLength  | 전송 길이를 설정합니다 | string |   아니요 |
|  ContentMD5  | 업로드 파일의 MD5 값을 인증에 사용하도록 설정합니다 | string |   아니요 |
| Metadata | 사용자의 사용자 지정 파일 메타 정보 | array | 아니요   |
| ServerSideEncryption | 서버 암호화 방법 | string |   아니요 |
| MetadataDirective | 소스 파일의 헤더 사용 여부, 선택 가능값은 Copy, Replaced, 기본값은 Copy, Copy는 소스 파일의 헤더 사용, Replaced는 해당 API의 헤더 사용을 의미합니다 |string | 아니요 |

#### 요청 예시

```php
#copyobject
# 간편 copy API
try {
    $result = $cosClient->copyObject(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' => 'testbucket-125000000',
        // CopySource is required
        'CopySource' => 'lewzylu03-1252448703.cos.ap-guangzhou.myqcloud.com/tox.ini',
        // Key is required
        'Key' => 'string',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

#copy
#5G보다 크면 자동으로 멀티파트 copy API를 사용합니다.
try {
    $result = $cosClient->Copy($bucket = 'lewzylu01-1252448703',
        $key = 'string',
        $copysource = 'lewzylu02-1252448703.cos.ap-guangzhou.myqcloud.com/test1G',
        $options = array('VersionId'=>'MTg0NDY3NDI1NTk0MzUwNDQ1OTg'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### putBucketLifecycle
#### 방식 프로토타입

```php
// 버킷의 수명 주기 설정
public Guzzle\Service\Resource\Model putBucketLifecycle(array $args = array());
```
#### 요청 매개변수
| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  |  버킷 이름이며, 숫자 및 소문자와 대시 "-"로 구성됩니다 | string |   예 |
| Rule  | 해당 규칙을 설정하며, ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, AbortIncompleteMultipartUpload 등이 포함됩니다 | array | 예   |
| ID | 규칙의 ID       | string   | 아니요           |
| Filter  | 규칙이 영향을 주는 Object 집합을 설명하는 데 사용됩니다 | array |   예 |
| Status  | Rule을 시작할지를 설정하며, 선택 가능 값은 Enabled 또는 Disabled입니다 | string |  예 |
| Expiration  | Object 만료 규칙을 설정하며, 일수 Days 또는 날짜 Date를 지정할 수 있습니다 | array |  아니요 |
| Transition  | Object 스토리지 클래스 전환 규칙을 설정하며, 일수 Days 또는 날짜 Date를 지정할 수 있습니다. StorageClass는 Standard_IA를 선택할 수 있습니다 | array |  아니요 |


#### 요청 예시

```php
#putBucketLifecycle
try {
    $result = $cosClient->putBucketLifecycle(array(
    //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
    'Bucket' => 'testbucket-125000000',
    // Rules is required
    'Rules' => array(
        array(
            'Expiration' => array(
                'Days' => 1,
            ),
            'ID' => 'id1',
            'Filter' => array(
                'Prefix' => 'documents/'
            ),
            // Status is required
            'Status' => 'Enabled',
            'Transitions' => array(
                array(
                    'Days' => 200,
                    'StorageClass' => 'Standard_IA')),
            // ... repeated
        ),
    )));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] =>
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### getBucketLifecycle
#### 방식 프로토타입

```php
// 버킷의 수명 주기 구성 획득
public Guzzle\Service\Resource\Model getBucketLifecycle(array $args = array());
```
#### 요청 매개변수

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |    


#### 요청 예시
```php
#getBucketLifecycle
try {
    $result = $cosClient->getBucketLifecycle(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' =>'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [Rules] => Array
                (
                    [0] => Array
                        (
                            [ID] => id1
                            [Filter] => Array
                                (
                                    [Prefix] => documents/
                                )

                            [Status] => Enabled
                            [Transition] => Array
                                (
                                    [Days] => 200
                                    [StorageClass] => Standard_IA
                                )

                            [Expiration] => Array
                                (
                                    [Days] => 1000
                                )

                        )

                )

            [RequestId] => NWE3YzhlZjNfY2FhMzNiMGFfNDVkNF8yZDIxODE=
        )
)
```

### deleteBucketLifecycle
#### 방식 프로토타입

```php
// 버킷의 수명 주기 구성 삭제
public Guzzle\Service\Resource\Model deleteBucketLifecycle(array $args = array());
```
#### 요청 매개변수

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |   

#### 요청 예시

```php
#deleteBucketLifecycle
try {
    $result = $cosClient->deleteBucketLifecycle(array(
        //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
        'Bucket' =>'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] =>
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### object 다운로드 url 획득

object이 서명이 있는 다운로드 url을 획득합니다.

#### 요청 예시

```php
//object의 다운로드 url 획득
//bucket의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다
$bucket =  'testbucket-125000000';
$key = 'hello.txt';
$signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
```
#### 임시 키 사용

```php
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => 'cn-south',
        'timeout' => ,
        'credentials'=> array(
            'appId' => '',
            'secretId'    => '',
            'secretKey' => '',
            'token' => '')));
```


### 보관 파일 복원

#### 방식 프로토타입

```php
// 보관 파일 복원
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.


| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  아니요         |  
| Key      |     객체 키(Key)이며, 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 액세스 도메인 이름  bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg  중, 객체 키는 doc1/pic1.jpg입니다       | string | 예       |      
| Days      |        저장 시간        |   integer |  예          |   
| Tier   |         복구 유형        | string |   아니요          |    

#### 요청 예시

```php
  try {
    $result = $cosClient->restoreObject(array(
        // Bucket is required
        'Bucket' => 'lewzylu02',
        // Objects is required
        'Key' => '11',
        'Days' => 7,
        'CASJobParameters' => array(
            'Tier' =>'Bulk'
        )
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```


### 버전 관리 활성화

#### 방식 프로토타입

```php
// 버전 관리 활성화
public Guzzle\Service\Resource\Model putBucketVersioning(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |     
| Status   |          버전 관리 상태              |   string       | 예           |       

#### 요청 예시
```php
#putBucketVersioning
try {
    $result = $cosClient->putBucketVersioning(
    array('Bucket' => 'lewzylu02',
    'Status' => 'Enabled')
    );
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] =>
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### 버킷 버전 획득

#### 방식 프로토타입

```php
// 버킷 버전 획득
public Guzzle\Service\Resource\Model getBucketVersioning(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |        

#### 요청 예시

```php
try {
    $result = $cosClient->getBucketVersioning(
        array('Bucket' => 'lewzylu02',)
    );
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

```

#### 결과 반환 예제
```php
Array
(
    [data:protected] => Array
        (
            [Status] => Enabled
            [RequestId] => NWE3YzhmZTVfNjIyNWI2NF80YzQ3XzJkNjU4NQ==
        )
)
```

### 각 버전의 파일 리스트를 인쇄합니다

#### 방식 프로토타입

```php
// 각 버전의 파일 리스트를 인쇄합니다
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```

#### 요청 매개변수

$args는 다음 필드의 연결 배열을 포함합니다.

| 매개변수 이름   | 설명   | 유형   | 필수 입력 필드 여부 |
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |      버킷 이름    |    string     |  예         |          
| Delimiter      |      구분 기호         |    string     |  아니요          |      
| Marker      |          식별자        |   string     |  No          |      
| MaxKeys      |           최대 객체 개수         |  int     |   아니요          |       
| Prefix      |            접두사         |string     |  아니요           |

#### 요청 예시

```php
try {
    $result = $cosClient->listObjectVersions(
        array('Bucket' => 'lewzylu02',
            'Prefix'=>'test1G')
    );
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

```
#### 결과 반환 예제
```php
Array
(
   [data:protected] => Array
        (
            [Name] => lewzylu02-1252448703
            [Prefix] => test1G
            [KeyMarker] =>
            [VersionIdMarker] =>
            [MaxKeys] => 1000
            [IsTruncated] =>
            [Versions] => Array
                (
                    [0] => Array
                        (
                            [Key] => test1G
                            [VersionId] => MTg0NDY3NDI1NTg1ODc4Nzk3NjI
                            [IsLatest] => 1
                            [LastModified] => 2018-01-05T03:07:51.000Z
                            [ETag] => "202cb962ac59075b964b07152d234b70"
                            [Size] => 3
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1252448703
                                )

                        )

                    [1] => Array
                        (
                            [Key] => test1G
                            [VersionId] => MTg0NDY3NDI1NTk0MzI3NDU3NTk
                            [IsLatest] =>
                            [LastModified] => 2017-12-26T08:26:50.000Z
                            [ETag] => "13ddf6552868644926ba606cd287106b-1"
                            [Size] => 5242880
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1252448703
                                )

                        )

                    [2] => Array
                        (
                            [Key] => test1G
                            [VersionId] => MTg0NDY3NDI1NTk0MzI3ODAzODc
                            [IsLatest] =>
                            [LastModified] => 2017-12-26T08:26:16.000Z
                            [ETag] => "3c86b7371340b2174b875fa7bcc0bd9a-1"
                            [Size] => 5242880
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1252448703
                                )

                        )
                )

            [RequestId] => NWE3YzkwMGFfMTliYjk0MGFfMWUwOWRfMmJlZWIx
        )
)
```
### 사전 서명 링크
#### 요청 예시
```
try {
    #여기를 다른 어떠한 API로도 바꿀 수 있습니다
    $command = $cosClient->getCommand('putObject', array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => '', //Body는 무엇이든 될 수 있습니다
    ));
    $signedUrl = $command->createPresignedUrl('+10 minutes');
    echo ($signedUrl);
} catch (\Exception $e) {
    echo($e);
}
```
