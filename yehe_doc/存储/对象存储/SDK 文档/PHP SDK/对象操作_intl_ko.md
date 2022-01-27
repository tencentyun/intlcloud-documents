## 소개

본 문서는 객체의 고급 인터페이스, 간단한 작업, 멀티파트 작업 관련 API 개요 및 SDK 예시 코드를 제공합니다.

**간단한 작업**

| API                                                          | 작업명                   | 작업 설명                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회             | 버킷의 일부 또는 모든 객체 조회                 |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | 객체 및 이전 버전 리스트 조회 | 버킷의 일부 또는 모든 객체와 이전 버전 정보 조회 |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 간편한 객체 업로드             | 버킷에 객체 1개 업로드                           |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | 객체 추가 업로드             | 객체를 파트 추가 방식으로 버킷에 업로드                       |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회           | 객체 메타데이터 정보 조회                           |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드                 |로컬에 객체 1개 다운로드                             |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정             | 파일을 타깃 경로에 복사                             |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제             | 버킷에서 지정 객체 삭제                         |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제             | 버킷에서 다수의 객체 일괄 삭제                         |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 아카이브된 객체 복구             | 아카이브 유형의 객체 검색 및 액세스                       |


**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 멀티파트 업로드 작업 초기화                   |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 멀티파트 업로드       | 객체 멀티파트 업로드                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 다른 객체를 한 파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 객체의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 하나의 멀티파트 업로드 작업 중지 및 이미 업로드한 파트 삭제 |

## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

지정 버킷의 모든 객체를 조회합니다(List Objects).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### 요청 예시

#### 예시1: 지정 접두사와 시작 객체의 객체 리스트 조회

[//]: # ".cssg-snippet-get-bucket-comp"

```php
try {
    $result = $cosClient->listObjects(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Delimiter' => '',
        'EncodingType' => 'url',
        'Marker' => 'doc/picture.jpg',
        'Prefix' => 'doc',
        'MaxKeys' => 1000,
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름     | 유형   | 설명                                                         | 필수 입력 여부 |
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Bucket       | String | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Delimiter    | String | 기본값 null. 세퍼레이터 설정(예시: `/`을 설정해 가상 폴더화)                | No       |
| EncodingType | String | 기본 인코딩 없음. 반환값의 인코딩 방식 규정. url 선택 가능                | No       |
| Marker       | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 시작 위치 표시 | No       |
| Prefix       | String | 기본값 null. 객체 키를 필터링해 지정 접두사(prefix)로 시작하는 객체와 매칭 | No       |
| MaxKeys      | Int    | 반환되는 최대 객체 수량. 기본값은 최대 1,000개                    | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Name] => examplebucket-1250000000
            [Prefix] => doc
            [Marker] => doc/picture.jpg
            [MaxKeys] => 10
            [IsTruncated] => 1
            [NextMarker] => doc/exampleobject
            [Contents] => Array
                (
                    [0] => Array
                        (
                            [Key] => doc/exampleobject
                            [LastModified] => 2019-02-14T12:20:40.000Z
                            [ETag] => "e37b429559d82e852af0b2f5b4d078ab72b90208"
                            [Size] => 6532594
                            [Owner] => Array
                                (
                                    [ID] => 100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                        )

                    [1] => Array
                        (
                            [Key] => doc/exampleobject2
                            [LastModified] => 2019-03-04T06:34:43.000Z
                            [ETag] => "988f9f28e68eba9b8c1f5f98ccce0a3c"
                            [Size] => 28
                            [Owner] => Array
                                (
                                    [ID] => 100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                        )
                )
            [RequestId] => NWNhMzM0MmZfOWUxYzBiMDlfOTk2YV83ZWE3ODE=
        )

)
```

#### 반환 결과 설명

| 매개변수 이름     | 유형   | 설명                                                         | 부모 노드   |
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Name         | String | 버킷 이름. 형식: BucketName-APPID                           | 없음       |
| Delimiter    | String | 세퍼레이터 설정(예시: `/`을 설정해 가상 폴더화)                          | 없음       |
| EncodingType | String | 반환값의 인코딩 방식 규정                                         | 없음       |
| Marker       | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 시작 위치 표시 | 없음       |
| Prefix       | String | 객체 키를 필터링해 지정 접두사(prefix)로 시작하는 객체와 매칭  | 없음       |
| MaxKeys      | Int    | 반환되는 최대 객체 수량. 기본값은 최대 1,000개                 | 없음       |
| IsTruncated  | Int    | 반환된 객체의 자르기 여부 표시                                  | 없음       |
| Contents     | Array  | 반환된 객체 리스트                                               | 없음       |
| Content      | Array  | 반환된 객체 속성. 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', 'Size' 등의 정보를 담은 모든 객체의 메타정보를 포함한 리스트 | Contents |

### 객체 및 이전 버전 리스트 조회 

#### 기능 설명

버킷의 일부 또는 모든 객체 및 이전 버전 정보를 조회합니다.

#### 메소드 프로토타입

```
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```

#### 요청 예시

#### 예시1: 이전 객체 리스트 조회

[//]: # ".cssg-snippet-list-object-versioning"

```php
try {
    $result = $cosClient->listObjectVersions(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Delimiter' => '',
        'EncodingType' => 'url',
        'KeyMarker' => 'doc/picture.jpg',
        'VersionIdMarker' => 'MTg0NDUxODMyMTE2ODY0OTExOTk3W',
        'Prefix' => 'doc',
        'MaxKeys' => 1000,
    )); 
    print_r($result);
} catch (\Exception $e) {
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름        | 유형   | 설명                                                         | 필수 입력 여부 |
| --------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket          | String | 버킷 이름. BucketName-APPID로 구성                         | Yes       |
| Prefix          | String | 기본값 null. 객체 키를 필터링해 prefix로 시작하는 객체와 매칭   | No       |
| Delimiter       | String | 기본값 null. 세퍼레이터 설정(예시: `/`을 설정해 가상 폴더화)                | No       |
| KeyMarker       | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 키 시작 위치 표시 | No       |
| VersionIdMarker | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 VersionId 시작 위치 표시 | No       |
| MaxKeys         | Int    | 반환되는 최대 객체 수량. 기본값은 최대 1,000개                         | No       |
| EncodingType    | String | 기본 인코딩 없음. 반환값의 인코딩 방식 규정. url 선택 가능                | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Name] => examplebucket-1250000000
            [Prefix] => doc
            [KeyMarker] => string
            [VersionIdMarker] => string
            [MaxKeys] => 10
            [IsTruncated] => 1
            [NextKeyMarker] => string
            [NextVersionIdMarker] => string
            [Versions] => Array
                (
                    [0] => Array
                        (
                            [Key] => doc/exampleobject1
                            [VersionId] => null
                            [IsLatest] => 1
                            [LastModified] => 2019-06-13T09:24:52.000Z
                            [ETag] => "96e79218965eb72c92a549dd5a330112"
                            [Size] => 6
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1250000000
                                )
                        )

                    [1] => Array
                        (
                            [Key] => doc/exampleobject2
                            [VersionId] => MTg0NDUxODMyMTE2ODY0OTExOTk
                            [IsLatest] => 1
                            [LastModified] => 2019-06-18T12:47:03.000Z
                            [ETag] => "698d51a19d8a121ce581499d7b701668"
                            [Size] => 3
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1250000000
                                )
                        )
                    )
            [RequestId] => NWQwOGVkZGRfMjViMjU4NjRfODNjN18xMTE5YWI4
        )

)
```

#### 반환 결과 설명

| 매개변수 이름            | 유형   | 설명                                                         | 부모 노드   |
| ------------------- | ------ | ------------------------------------------------------------ | -------- |
| Name                | String | 버킷 이름. 형식: BucketName-APPID                           | 없음       |
| Delimiter           | String | 세퍼레이터 설정(예시: `/`을 설정해 가상 폴더화)                          | 없음       |
| EncodingType        | String | 반환값의 인코딩 방식 규정                                         | 없음       |
| KeyMarker           | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 키 시작 위치 표시 | 없음       |
| VersionIdMarker     | String | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 VersionId 시작 위치 표시 | 없음       |
| NextKeyMarker       | String | IsTruncated가 true이면 그 다음 객체를 반환하는 리스트 키의 시작 위치 표시 | 없음       |
| NextVersionIdMarker | String | IsTruncated가 true이면 그 다음 객체를 반환하는 리스트의 VersionId 시작 위치 표시 | 없음       |
| Prefix              | String | 객체 키를 필터링해 지정 접두사(prefix)로 시작하는 객체와 매칭  | 없음       |
| MaxKeys             | Int    | 반환되는 최대 객체 수량. 기본값은 최대 1,000개                    | 없음       |
| IsTruncated         | Int    | 반환된 객체의 자르기 여부 표시                                  | 없음       |
| Versions            | Array  | 여러 버전의 객체 메타데이터를 포함한 리스트                            | 없음       |
| Version             | Array  | 'ETag', 'StorageClass', 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified', 'Size' 등의 정보를 담은 여러 버전의 객체 메타데이터를 포함한 리스트 | Versions |
| CommonPrefixes      | Array  | Prefix로 시작하고 Delimiter로 끝나는 모든 객체를 동일한 종류로 분류      | 없음       |



### 객체 간편 업로드

#### 기능 설명

객체를 지정 버킷에 업로드합니다(PUT Object). 최대 5GB 미만인 객체의 업로드를 지원합니다. 5GB를 초과하는 경우 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) 또는 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)를 사용하여 업로드하십시오.

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model putObject(array $args = array())
```

#### 요청 예시

#### 예시1: 로컬 파일 업로드

[//]: # ".cssg-snippet-put-object"

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
    )); 
    // 요청 완료 
    print_r($result);
} catch (\Exception $e) { 
    // 요청 실패 
    echo($e); 
}
```

#### 예시2: 아카이브된 파일 업로드

[//]: # ".cssg-snippet-put-object-archive"

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
        'StorageClass' => 'Archive'
    )); 
    // 요청 완료 
    print_r($result); 
} catch (\Exception $e) { 
    // 요청 실패 
    echo($e); 
}
```

#### 예시3: 지정 Content-type 파일 업로드

[//]: # ".cssg-snippet-put-object-with-content-type"

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
        'ContentType' => 'text/xml'
    )); 
    // 요청 완료 
    print_r($result); 
} catch (\Exception $e) { 
    // 요청 실패 
    echo($e); 
}
```

#### 예시4: 빈 가상 디렉터리 생성

[//]: # ".cssg-snippet-put-object-with-new-foler"

```php
try {
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'folder/',
        'Body' => "",
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}

```

#### 예시5: ContentMD5 검사 생성 로컬 파일 업로드

```php
try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID 
        'Key' => 'exampleobject', 
        'Body' => fopen('path/to/localFile', 'rb'), 
        'ContentMD5' => true, 
    )); 
    // 요청 완료 
    print_r($result);
} catch (\Exception $e) { 
    // 요청 실패 
    echo($e); 
}
```

#### 예시6: 객체 업로드(단일 링크 속도 제한)
>?객체 업로드 속도 제한에 대한 설명은 [단일 링크 속도 제한](https://intl.cloud.tencent.com/document/product/436/34072)을 참고하십시오.

```php
try {
$result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-125000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'Body' => fopen($local_path, 'rb'),
        'TrafficLimit' => 8 * 1024 * 1024 // 1MB/s로 제한
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```
#### 매개변수 설명

| 매개변수 이름             | 유형        | 설명                                                         | 필수 입력 여부 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket               | String      | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Key                  | String      | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | No       |
| ACL                  | String      | 객체 ACL 설정. 예시: private, public-read                    | No       |
| Body                 | Stream/String | 업로드한 콘텐츠                                                  | Yes       |
| CacheControl         | String      | 캐시 정책. Cache-Control 설정                                 | No       |
| ContentDisposition   | String      | 파일 이름. Content-Disposition 설정                           | No       |
| ContentEncoding      | String      | 인코딩 형식. Content-Encoding 설정                              | No       |
| ContentLanguage      | String      | 언어 유형. Content-Language 설정                              | No       |
| ContentLength        | Int         | 전송 길이 설정                                                 | No       |
| ContentType          | String      | 콘텐츠 유형. Content-Type 설정                                  | No       |
| Expires              | String      | Content-Expires 설정                                              | No       |
| Metadata             | Array       | 사용자 정의 파일 메타정보                                       | No     |
| StorageClass         | String      | 파일의 스토리지 유형이며(예시: STANDARD, STANDARD_IA, ARCHIVE), 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참고   | No       |
| ContentMD5           | Boolean      | 업로드된 파일의 MD5 값을 검사용으로 자동 생성 여부                                | No       |
| ServerSideEncryption | String      | 서버 암호화 방법                                               | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "698d51a19d8a121ce581499d7b701668"
            [VersionId] => MTg0NDUxODMyMTE2ODY0OTExOTk
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ObjectURL] => http://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/123
            [CRC] => 16749565679157681890
        )

)

```

#### 반환 결과 설명

| 매개변수 이름  | 유형   | 설명                       | 부모 노드 |
| --------- | ------ | -------------------------- | ------ |
| ETag      | String | 업로드된 파일의 MD5 값          | 없음     |
| VersionId | String | 버전 제어 활성화 후 파일의 버전 번호 | 없음     |
| CRC     | String | CRC64로 [데이터 검사](https://intl.cloud.tencent.com/document/product/436/34078) | 없음     |

### 객체 추가 업로드

#### 기능 설명

객체를 멀티파트에 추가하는 방식으로 버킷(APPEND object)에 업로드합니다.

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model appendObject(array $args = array());
```

#### 요청 예시

#### 예시1: 업로드할 입력 스트림 추가
```php
try {
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'Position' => 0,
        'Body' => "hello,world",
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시2: 로컬 파일 스트림 추가 업로드
```php
try {
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'Position' => 0,
        'Body' => fopen('path/to/localFile', 'rb'),
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시3: 멀티 데이터 추가 업로드

```php
try {
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'Position' => 0, //객체 위치 추가
        'Body' => fopen('path/to/localFile', 'rb'),//파일 내용 읽기
    ));
    
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'Position' => (integer)$result['Position'], //마지막으로 추가된 파일의 객체 위치에 추가
        'Body' => "hello, world", 
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름  | 유형   | 설명                                                         | 필수 입력 여부 |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket    | String | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Key       | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인<br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | Yes       |
| Position | Integer | 추가 작업의 시작점. 최초 추가는 Position=0으로 설정하고 후속 추가는 Position을 현재 Object의 content-length로 설정                             | Yes      |
| Body | File/String | 로컬 파일 스트림 또는 입력 스트림 등 멀티파트 업로드의 콘텐츠                             | Yes       |

#### 반환 결과 예시

```php
GuzzleHttp\Command\Result Object
(
    [ETag] => "9a74ded332531da4c295934ba5a9cf8b"
    [Position] => 4
    [RequestId] => NjExNWU4NTlfZDIyZjJjMGJfM2Q2ZV8xMzJjZThhZg==
    [Key] => exampleobject
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject
)
```

#### 반환 결과 설명

| 매개변수 이름             | 유형   | 설명                                               | 부모 노드 |
| -------------------- | ------ | -------------------------------------------------- | ------ |
| ETag                 | String | 파일의 MD5 값                                      | 없음     |
| Position              | Integer | 추가 작업의 시작점                                 | 없음     |

### 객체 메타데이터 조회

#### 기능 설명

Object의 Meta 정보를 조회합니다(HEAD Object).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model headObject(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-head-object"

```php
try {
    $result = $cosClient->headObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름  | 유형   | 설명                                                         | 필수 입력 여부 |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket    | String | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Key       | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인<br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | Yes       |
| VersionId | String | 버전 제어 활성화 후 지정 파일 상세 버전 지정                             | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [DeleteMarker] => 
            [AcceptRanges] => 
            [Expiration] => 
            [Restore] => 
            [LastModified] => Tue, 02 Apr 2019 12:38:09 GMT
            [ContentLength] => 238186
            [ETag] => "af9f3b8eaf64473278909183abba1e31"
            [MissingMeta] => 
            [VersionId] => 
            [CacheControl] => 
            [ContentDisposition] => 
            [ContentEncoding] => 
            [ContentLanguage] => 
            [ContentType] => text/plain; charset=utf-8
            [Expires] => 
            [ServerSideEncryption] => 
            [Metadata] => Array
                (
                    [md5] => af9f3b8eaf64473278909183abba1e31
                )
            [SSECustomerAlgorithm] => 
            [SSECustomerKeyMD5] => 
            [SSEKMSKeyId] => 
            [StorageClass] => 
            [RequestCharged] => 
            [ReplicationStatus] => 
            [RequestId] => NWNhMzU3Y2ZfMzFhYzM1MGFfODdhMF8xOTExM2U=
            [CRC] => 16749565679157681890
        )

)
```

#### 반환 결과 설명

| 매개변수 이름             | 유형   | 설명                                               | 부모 노드 |
| -------------------- | ------ | -------------------------------------------------- | ------ |
| CacheControl         | String | 캐시 정책. Cache-Control 설정                       | 없음     |
| ContentDisposition   | String | 파일 이름. Content-Disposition 설정                 | 없음     |
| ContentEncoding      | String | 인코딩 형식. Content-Encoding 설정                    | 없음     |
| ContentLanguage      | String | 언어 유형. Content-Language 설정                    | 없음     |
| ContentLength        | Int    | 전송 길이 설정                                       | 없음     |
| ContentType          | String | 콘텐츠 유형. Content-Type 설정                        | 없음     |
| Metadata             | Array  | 사용자 정의 파일 메타정보                             | 없음     |
| StorageClass         | String | 파일의 스토리지 유형(예시: STANDARD, STANDARD_IA, ARCHIVE). 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참고 | 없음     |
| ServerSideEncryption | String | 서버 암호화 방법                                     | 없음     |
| ETag                 | String | 파일의 MD5 값                                      | 없음     |
| Restore              | String | 아카이브된 파일 복구 정보                                 | 없음     |
| CRC                  | String | CRC64로 [데이터 검사](https://intl.cloud.tencent.com/document/product/436/34078) | 없음     |

### 객체 다운로드

#### 기능 설명

객체를 로컬에 다운로드합니다(GET Object).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model getObject(array $args = array());
```

#### 요청 예시

#### 예시1: 로컬에 파일 다운로드

[//]: #	".cssg-snippet-get-object"

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'SaveAs' => 'path/to/localFile',
    )); 
    // 요청 완료
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시2: range에 따라 파일 콘텐츠 획득

[//]: # ".cssg-snippet-get-object-range"

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'Range' => 'bytes=0-10'
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시3: 지정 버전 파일 다운로드

[//]: # ".cssg-snippet-get-object-with-versionId"

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'VersionId' => 'exampleVersionId'
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시4: 파일 다운로드(단일 링크 속도 제한)
>?객체 다운로드 속도 제한에 대한 설명은 [단일 링크 속도 제한](https://intl.cloud.tencent.com/document/product/436/34072)을 참고하십시오.

```php
try {
   $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-125000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'SaveAs' => '/data/exampleobject',
        'TrafficLimit' => 8 * 1024 * 1024 // 1MB/s로 제한
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름                   | 유형   | 설명                                                         | 필수 입력 여부 |
| -------------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket                     | String | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Key                        | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인<br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | Yes       |
| SaveAs                     | String | 로컬에 저장한 로컬 파일 경로                                     | No       |
| VersionId                  | String | 버전 제어 활성화 후 지정 파일 상세 버전 지정                             | No       |
| Range                      | String | 다운로드 파일의 범위 설정(형식: bytes=first-last)                  | No       |
| ResponseCacheControl       | String | 응답 헤더의 Cache-Control 설정                                   | No       |
| ResponseContentDisposition | String | 응답 헤더의 Content-Disposition 설정                             | No       |
| ResponseContentEncoding    | String | 응답 헤더의 Content-Encoding 설정                                | No       |
| ResponseContentLanguage    | String | 응답 헤더의 Content-Language 설정                                | No       |
| ResponseContentType        | String | 응답 헤더의 Content-Type 설정                                    | No       |
| ResponseExpires            | String | 응답 헤더의 Content-Expires 설정                                 | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [DeleteMarker] => 
            [AcceptRanges] => bytes
            [Expiration] => 
            [Restore] => 
            [LastModified] => Tue, 02 Apr 2019 20:38:09 GMT
            [ContentLength] => 238186
            [ETag] => "af9f3b8eaf64473278909183abba1e31"
            [MissingMeta] => 
            [VersionId] => 
            [CacheControl] => 
            [ContentDisposition] => 
            [ContentEncoding] => 
            [ContentLanguage] => 
            [ContentRange] => 
            [ContentType] => text/plain; charset=utf-8
            [Expires] => 
            [WebsiteRedirectLocation] => 
            [ServerSideEncryption] => 
            [Metadata] => Array
                (
                    [md5] => af9f3b8eaf64473278909183abba1e31
                )

            [SSECustomerAlgorithm] => 
            [SSECustomerKeyMD5] => 
            [SSEKMSKeyId] => 
            [StorageClass] => 
            [RequestCharged] => 
            [ReplicationStatus] => 
            [RequestId] => NWNhNDBmYzBfNmNhYjM1MGFfMmUzYzFfMWIzMDYz
            [CRC] => 16749565679157681890
        )

)
```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------------------ | ------ |
| Body                 | File/String | 콘텐츠 다운로드                                                     | 없음     |
| ETag                 | String      | 파일의 MD5 값                                                | 없음     |
| Expires              | String      | Content-Expires                                              | 없음     |
| Metadata             | Array       | 사용자 정의 파일 메타정보                                       | 없음     |
| StorageClass         | String      | 파일의 스토리지 유형이며(예시: STANDARD, STANDARD_IA, ARCHIVE), 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참고 | 없음     |
| ContentMD5           | String      | 업로드된 파일의 MD5 값을 검사용으로 설정                                | 없음     |
| ServerSideEncryption | String      | 서버 암호화 방법                                               | 없음     |
| CacheControl         | String      | 캐시 정책. Cache-Control 설정                                 | 없음     |
| ContentDisposition   | String      | 파일 이름. Content-Disposition 설정                           | 없음     |
| ContentEncoding      | String      | 인코딩 형식. Content-Encoding 설정                              | 없음     |
| ContentLanguage      | String      | 언어 유형. Content-Language 설정                              | 없음     |
| ContentLength        | Int         | 전송 길이 설정                                                 | 없음     |
| ContentType          | String      | 콘텐츠 유형. Content-Type 설정                                  | 없음     |
| Metadata             | Array       | 사용자 정의 파일 메타정보                                       | 없음     |
| Restore              | String      | 아카이브된 파일 복구 정보                                            | 없음     |
| CRC                  | String | CRC64로 [데이터 검사](https://intl.cloud.tencent.com/document/product/436/34078) | 없음     |

### 객체 복사 설정

객체를 타깃 경로에 복사합니다(PUT Object - Copy).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model copyObject(array $args = array());
```

#### 요청 예시

#### 예시1: 객체 복사

[//]: # ".cssg-snippet-copy-object"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시2: 지정 버전 객체 복사

[//]: # ".cssg-snippet-copy-object-with-versionId"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject?versionId=MTg0NDUxNjI3NTM0ODE2Njc0MzU',
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시3: 스토리지 유형을 아카이브 유형으로 수정

[//]: # ".cssg-snippet-copy-object-update-storage-class"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'StorageClass' => 'Archive'
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시4: meta 속성 수정

[//]: # ".cssg-snippet-copy-object-update-metadata"

```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'MetadataDirective' => 'Replaced',
        'Metadata' => array(
            'key1' => 'value1',
            'key2' => 'value2',
        )
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름          | 유형   | 설명                                                         | 필수 입력 여부 |
| ----------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket            | String | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Key               | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인<br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | Yes       |
| CopySource        | String | Appid, Bucket, Key, Region을 포함한 원본 파일의 복사 경로 설명, <br>예시: `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes       |
| MetadataDirective | String | 옵션 값은 Copy와 Replaced. Copy로 설정하는 경우 설정된 사용자 메타데이터 정보를 무시하고 바로 파일 복사. Replaced로 설정하는 경우 설정된 메타정보에 따라 메타데이터 수정. 타깃 경로와 소스 경로가 같은 경우 반드시 Replaced로 설정 | No       |

### 단일 객체 삭제

#### 기능 설명

버킷에서 지정 Object(파일/객체)를 삭제합니다.

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model deleteObject(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-delete-object"

#### 예시1: 단일 단순 객체 삭제
```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject'
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```
#### 예시2: 버전 번호가 있는 단일 객체 삭제
```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'VersionId' => 'exampleVersionId' //버킷의 버전 제어가 비활성화된 경우 해당 매개변수 사용 불가
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```


#### 매개변수 설명

| 매개변수 이름  | 유형   | 설명                                                         | 필수 입력 여부 |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket    | String | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Key       | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인<br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | Yes       |
| VersionId | String | 파일의 버전 번호 삭제                                             | No       |

### 다수의 객체 삭제

#### 기능 설명

버킷에서 다수의 객체(파일/객체)를 일괄 삭제합니다.

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model deleteObjects(array $args = array());
```

#### 요청 예시

#### 예시1: 여러 개의 단순 객체 삭제
```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Objects' => array(
            array(
                'Key' => 'exampleobject',
            ),  
            // ... repeated
        ),  
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시2: 버전 번호가 있는 여러 객체 삭제


[//]: # ".cssg-snippet-delete-multi-object"

```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Objects' => array(
            array(
                'Key' => 'exampleobject',
                'VersionId' => 'string' //버킷의 버전 제어가 비활성화된 경우 해당 매개변수 사용 불가
            ),  
            // ... repeated
        ),  
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```


#### 예시3: 지정 접두사 삭제

[//]: # ".cssg-snippet-delete-prefix"

```php
$cos_prefix = "cos/folder";
$nextMarker = '';
$isTruncated = true;
while ( $isTruncated ) {
    try {
        $result = $cosClient->listObjects(
            ['Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
            'Delimiter' => '',
            'EncodingType' => 'url',
            'Marker' => $nextMarker,
            'Prefix' => $cos_prefix,
            'MaxKeys' => 1000]
        );    
        $isTruncated = $result['IsTruncated'];
        $nextMarker = $result['NextMarker'];
        foreach ( $result['Contents'] as $content ) {
            $cos_file_path = $content['Key'];
            $local_file_path = $content['Key'];
            // 필요에 따라 다운로드 경로 사용자 정의 스티칭
            try {
                $cosClient->deleteObject(array(
                    'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
                    'Key' => $cos_file_path,
                ));
                echo ( $cos_file_path . "\n" );
            } catch ( \Exception $e ) {
                echo( $e );
            }
        }
    } catch ( \Exception $e ) {
        echo( $e );
    }
}
```


#### 매개변수 설명

| 매개변수 이름  | 유형   | 설명                                                         | 필수 입력 여부 |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket    | String | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Objects   | Array  | 객체 리스트 삭제                                                 | Yes       |
| Object   | Array  | 삭제한 객체                                                 | Yes       |
| Key       | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인<br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | Yes       |
| VersionId | String | 파일의 버전 번호 삭제                                             | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Deleted] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject1
                        )
                )
            [Errors] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject2
                            [Code] => 
                            [Message] => 
                        )
                )
            [RequestId] => NWNhZWYzYWNfMTlhYTk0MGFfNGRjX2MzZTVhOQ==
        )
）
```

#### 반환 결과 설명

| 매개변수 이름 | 유형   | 설명                 | 부모 노드         |
| -------- | ------ | -------------------- | -------------- |
| Deleted  | Array  | 삭제 완료한 객체 리스트 | 없음             |
| Errors   | Array  | 삭제 실패한 객체 리스트 | 없음             |
| Key      | String | 객체 키               | Deleted/Errors |
| Code     | String | 실패 에러 코드           | Errors         |
| Message  | String | 실패 에러 정보         | Errors         |



### 아카이브된 객체 복구 

#### 기능 설명

아카이브 유형의 객체를 검색하여 액세스합니다(POST Object restore).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-restore-object"

```php
try {
    $result = $cosClient->restoreObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'Days' => 10,
        'CASJobParameters' => array(
            'Tier' =>'Expedited'
        )    
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름         | 유형   | 설명                                                         | 필수 입력 여부 |
| ---------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket           | String | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Key              | String | 객체 키                                                       | Yes       |
| Days             | String | 임시 사본 만료 기간 설정(단위: 일)                             | Yes       |
| CASJobParameters | Array  | 정보 복구                                                     | Yes       |
| Tier             | String | 아카이브 유형의 데이터를 복구하는 경우 Tier는 COS가 지원하는 3가지 복구 모드(Expedited, Standard, Bulk) 지정 가능. 딥 아카이브 유형의 데이터를 복구하는 경우 Tier는 COS가 지원하는 2가지 복구 모드(Standard, Bulk) 지정 가능. | Yes       |

## 멀티파트 작업

다음은 객체의 멀티파트 업로드 작업 내용입니다.

- 객체 멀티파트 업로드: 멀티파트 업로드를 초기화하고 파트를 업로드한 후 멀티파트 업로드를 완료합니다.
- 멀티파트 업로드 재개: 업로드된 파트를 조회하고 파트를 업로드한 후 멀티파트 업로드를 완료합니다.
- 업로드된 파트를 삭제합니다.

### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드를 조회합니다(List Multipart Uploads).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model listMultipartUploads(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-list-multi-upload"

```php
try {
    $result = $cosClient->listMultipartUploads(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Delimiter' => '/',
        'EncodingType' => 'url',
        'KeyMarker' => 'prfixKeyMarker',
        'UploadIdMarker' => 'string',
        'Prefix' => 'prfix',
        'MaxUploads' => 1000,
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름       | 유형   | 설명                                                         | 필수 입력 여부 |
| -------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket         | String | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Delimiter      | String | 기본값 null. 세퍼레이터 설정(예시: `/`을 설정해 가상 폴더화)                | No       |
| EncodingType   | String | 기본 인코딩이 없음. 반환값의 인코딩 방식 규정. url 선택 가능                | No       |
| KeyMarker      | String | 반환 parts의 list 시작 위치 표시                            | No       |
| UploadIdMarker | String | 반환 parts의 list 시작 위치 표시                            | No       |
| Prefix         | String | 기본값 null. parts 키를 필터링해 지정 접두사(prefix)로 시작하는 객체와 매칭 | No       |
| MaxUploads     | Int    | 반환 parts의 최대 수량. 기본값은 최대 1,000개                      | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [EncodingType] => 
            [KeyMarker] => 
            [UploadIdMarker] => 
            [MaxUploads] => 1000
            [Prefix] => 
            [IsTruncated] => 
            [Uploads] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject
                            [UploadId] => 1551693693b1e6d0e00eec30c534059865ec89c9393028b60bfaf167e9420524b25eeb2940
                            [Initiator] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [Owner] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                            [Initiated] => 2019-03-04T10:01:33.000Z
                        )

                    [1] => Array
                        (
                            [Key] => exampleobject
                            [UploadId] => 155374001100563fe0e9d37964d53077e54e9d392bce78f630359cd3288e62acee2b719534
                            [Initiator] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [Owner] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                            [Initiated] => 2019-03-28T02:26:51.000Z
                        )

                )

            [RequestId] => NWNhNDJmNzBfZWFhZDM1MGFfMjYyM2FfMWIyNzhh
        )

)
```

#### 반환 결과 설명

| 매개변수 이름     | 유형   | 설명                               | 부모 노드  |
| ------------ | ------ | ---------------------------------- | ------- |
| Bucket       | String | 버킷 이름. 형식: BucketName-APPID | 없음      |
| IsTruncated  | Int    | 반환된 객체의 자르기 여부 표시        | 없음      |
| Uploads      | Array  | 반환된 멀티파트 리스트                     | 없음      |
| Upload       | Array  | 반환된 멀티파트 속성                     | Uploads |
| Key          | String | 객체 키                           | Upload  |
| UploadId     | String | 객체 멀티파트 업로드 ID                  | Upload  |
| Initiator    | String | 해당 멀티파트 작업자 초기화               | Upload  |
| Owner        | String | 멀티파트 소유자                         | Upload  |
| StorageClass | String | 멀티파트 스토리지 유형                       | Upload  |
| Initiated    | String | 멀티파트 초기화 시간                     | Upload  |



### 멀티파트 업로드 초기화

#### 기능 설명

Multipart Upload 업로드 작업 초기화합니다(Initiate Multipart Upload).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-init-multi-upload"

```php
try {
    $result = $cosClient->createMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름             | 유형   | 설명                                                         | 필수 입력 여부 |
| -------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket               | String      | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Key                  | String | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인<br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | Yes       |
| CacheControl         | String | 캐시 정책. Cache-Control 설정                                 | No       |
| ContentDisposition   | String | 파일 이름. Content-Disposition 설정                           | No       |
| ContentEncoding      | String | 인코딩 형식. Content-Encoding 설정                              | No       |
| ContentLanguage      | String | 언어 유형. Content-Language 설정                              | No       |
| ContentLength        | Int    | 전송 길이 설정                                                 | No       |
| ContentType          | String | 콘텐츠 유형. Content-Type 설정                                  | No       |
| Expires              | String | Content-Expires 설정                                              | No       |
| Metadata             | Array  | 사용자 정의 파일 메타정보                                       | No       |
| StorageClass         | String | 파일의 스토리지 유형이며(예시: STANDARD, STANDARD_IA, ARCHIVE), 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참고       |    No       |
| ContentMD5           | Boolean | 업로드된 파일의 MD5 값을 검사용으로 자동 생성 여부                           | No       |
| ServerSideEncryption | String | 서버 암호화 방법                                               | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [Key] => exampleobject
            [UploadId] => 1554277569b3e83df05c730104c325eb7b56000449fb7d51300b0728aacde02a6ea7f6c033
            [RequestId] => NWNhNDY0YzFfMmZiNTM1MGFfNTM2YV8xYjliMTg=
        )

)
```

#### 반환 결과 설명

| 매개변수 이름 | 유형   | 설명                               | 부모 노드 |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket   | String | 버킷 이름. 형식: BucketName-APPID | 없음     |
| Key      | String | 객체 키                             | 없음     |
| UploadId | String | 객체 멀티파트 업로드 ID                   | 없음     |




### 멀티파트 업로드

파일을 멀티파트 업로드합니다(Upload Part).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model uploadPart(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-upload-part"

```php
try {
    $result = $cosClient->uploadPart(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject', 
        'Body' => 'string',
        'UploadId' => 'exampleUploadId', //UploadId는 객체 멀티파트 업로드 ID. 멀티파트 업로드를 초기화한 반환 매개변수에서 획득 
        'PartNumber' => 1, //PartNumber는 멀티파트의 일련 번호, COS는 일련 번호에 따라 멀티파트를 병합
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름      | 유형        | 설명                                                         | 필수 입력 여부 |
| ------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket        | String      | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Key           | String      | 객체 키                                                       | Yes       |
| UploadId      | String      | UploadId는 객체 멀티파트 업로드 ID, 멀티파트 업로드를 초기화한 반환 매개변수에서 획득 | Yes       |
| Body          | File/String | 업로드한 콘텐츠                                                   | Yes       |
| PartNumber    | Int         | PartNumber는 멀티파트의 일련 번호, COS는 일련 번호에 따라 멀티파트를 병합      | Yes       |
| ContentLength | Int         | 전송 길이 설정                                                 | No       |
| ContentMD5    | Boolean      | 업로드된 파일의 MD5 값을 검사용으로 자동 생성 여부                         | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
            [CRC] => 16749565679157681890
        )

)
```

#### 반환 결과 설명

| 매개변수 이름 | 유형   | 설명          | 부모 노드 |
| -------- | ------ | ------------- | ------ |
| ETag     | String | 멀티파트 MD5 값 | 없음     |
| CRC     | String | CRC64로 [데이터 검사](https://intl.cloud.tencent.com/document/product/436/34078) | 없음     |




### 멀티파트 복사

#### 기능 설명

다른 객체를 한 파트로 복사합니다(Upload Part - Copy).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model uploadPartCopy(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-upload-part-copy"

```php
try {
    $result = $cosClient->uploadPartCopy(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject', 
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'CopySourceRange' => 'bytes=0-1', //예시에서는 처음의 2바이트만 복사
        'UploadId' => 'exampleUploadId', //UploadId는 객체 멀티파트 업로드 ID. 멀티파트 업로드를 초기화한 반환 매개변수에서 획득 
        'PartNumber' => 1, //PartNumber는 멀티파트의 일련 번호, COS는 일련 번호에 따라 멀티파트를 병합
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름      | 유형   | 설명                                                         | 필수 입력 여부 |
| ------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket        | String | 버킷 이름. 형식: BucketName-APPID                           | Yes       |
| Key           | String | 객체 키                                                       | Yes       |
| UploadId      | String | UploadId는 객체 멀티파트 업로드 ID, 멀티파트 업로드를 초기화한 반환 매개변수에서 획득 | Yes       |
| CopySource    | String | Appid, Bucket, Key, Region을 포함한 원본 파일의 복사 경로 설명, <br>예시: `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes       |
| CopySourceRange    | String | 소스 객체 복사의 범위 설명(형식: bytes=first-last). 범위를 지정하지 않으면 전체 소스 객체 복사 | No       |
| PartNumber    | Int    | PartNumber는 멀티파트의 일련 번호. COS는 일련 번호에 따라 멀티파트 병합      | Yes       |
| ContentLength | Int    | 전송 길이 설정                                                 | No       |
| ContentMD5    | Boolean | 업로드된 파일의 MD5 값을 검사용으로 자동 생성 여부                             | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [LastModified] => "2017-09-04T04:45:45"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
            [CRC] => 16749565679157681890
        )

)
```

#### 반환 결과 설명

| 매개변수 이름     | 유형   | 설명                           | 부모 노드 |
| ------------ | ------ | ------------------------------ | ------ |
| ETag         | String | 멀티파트 MD5 값                  | 없음     |
| LastModified | String | 반환된 객체의 최종 수정 시간(GMT 형식) | 없음     |
| CRC     | String | CRC64로 [데이터 검사](https://intl.cloud.tencent.com/document/product/436/34078) | 없음     |


### 업로드된 파트 조회

#### 기능 설명

특정 멀티파트 업로드 작업에서 업로드된 파트를 조회합니다(List Parts).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model listParts(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-list-parts"

```php
try {
    $result = $cosClient->listParts(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'UploadId' => 'exampleUploadId',
        'PartNumberMarker' => 1,
        'MaxParts' => 1000,
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름         | 유형   | 설명                                    | 필수 입력 여부 |
| ---------------- | ------ | --------------------------------------- | -------- |
| Bucket           | String | 버킷 이름. 형식: BucketName-APPID      | Yes       |
| Key              | String | 객체 키                                  | Yes       |
| UploadId         | String | 객체 멀티파트 업로드 ID                       | Yes       |
| PartNumberMarker | Int    | 반환 parts의 list 시작 위치 표시       | No       |
| MaxParts         | Int    | 반환 parts의 최대 수량. 기본값은 최대 1,000개 | No       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [Key] => exampleobject
            [UploadId] => 1554279643cf19d71bb5fb0d29613e5541131f3a96387d9e168cd939c23a3d608c9eb94707
            [Owner] => Array
                (
                    [ID] => 1250000000
                    [DisplayName] => 1250000000
                )
            [PartNumberMarker] => 1
            [Initiator] => Array
                (
                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                    [DisplayName] => 100000000001
                )
            [StorageClass] => Standard
            [MaxParts] => 1000
            [IsTruncated] => 
            [Parts] => Array
                (
                    [0] => Array
                        (
                            [PartNumber] => 2
                            [LastModified] => 2019-04-03T08:21:28.000Z
                            [ETag] => "b948e77469189ac94b98e09755a6dba9"
                            [Size] => 1048576
                        )
                    [1] => Array
                        (
                            [PartNumber] => 3
                            [LastModified] => 2019-04-03T08:21:22.000Z
                            [ETag] => "9e5060e2994ec8463bfbebd442fdff16"
                            [Size] => 1048576
                        )                       
                )
            [RequestId] => NWNhNDZkNTJfOGNiMjM1MGFfMTRlYl8xYmJiOTU=
        )

)
```

#### 반환 결과 설명

| 매개변수 이름         | 유형   | 설명                                    | 부모 노드 |
| ---------------- | ------ | --------------------------------------- | ------ |
| Bucket           | String | 버킷 이름. 형식: BucketName-APPID      | 없음     |
| Key              | String | 객체 키                                  | 없음     |
| UploadId         | String | 객체 멀티파트 업로드 ID                       | 없음     |
| IsTruncated      | Int    | 반환된 객체의 자르기 여부 표시             | 없음     |
| PartNumberMarker | Int    | 반환 parts의 list 시작 위치 표시       | 없음     |
| MaxParts         | Int    | 반환 parts의 최대 수량. 기본값은 최대 1,000개 | 없음     |
| Initiator        | String | 해당 멀티파트 작업자 초기화                    | 없음     |
| Parts            | Array  | 반환된 멀티파트 리스트                          | 없음     |
| Part             | Array  | 반환된 멀티파트 속성                          | Parts  |
| PartNumber       | Int    | 멀티파트 일련 번호                                | Part   |
| LastModified     | String | 멀티파트 마지막 업로드 시간                      | Part   |
| ETag             | String | 멀티파트의 MD5 값                           | Part   |
| Size             | String | 멀티파트 크기                              | Part   |



### 멀티파트 업로드 완료

#### 기능 설명

전체 파일의 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());

```

#### 요청 예시

[//]: # ".cssg-snippet-complete-multi-upload"

```php
try {
    $result = $cosClient->completeMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject', 
        'UploadId' => 'exampleUploadId',
        'Parts' => array(
            array(
                'ETag' => 'exampleETag',
                'PartNumber' => 1,
            )), 
            // ... repeated
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름   | 유형   | 설명                               | 필수 입력 여부 |
| ---------- | ------ | ---------------------------------- | -------- |
| Bucket     | String | 버킷 이름. 형식: BucketName-APPID | Yes       |
| Key        | String | 객체 키                             | Yes       |
| UploadId   | String | 객체 멀티파트 업로드 ID                  | Yes       |
| Parts      | Array  | 멀티파트 정보 리스트                       | Yes       |
| Part       | Array  | 멀티파트 업로드한 콘텐츠 정보                 | Yes       |
| ETag       | String | 멀티파트 MD5 값                     | Yes       |
| PartNumber | Int    | 멀티파트 일련 번호                           | Yes       |

### 멀티파트 업로드 중지

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다(Abort Multipart Upload).

#### 메소드 프로토타입

```php
public Guzzle\Service\Resource\Model abortMultipartUpload(array $args = array());
```

#### 요청 예시

[//]: # ".cssg-snippet-abort-multi-upload"

```php
try {
    $result = $cosClient->abortMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject', 
        'UploadId' => 'exampleUploadId',
    )); 
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름 | 유형   | 설명                               | 필수 입력 여부 |
| -------- | ------ | ---------------------------------- | -------- |
| Bucket   | String | 버킷 이름. 형식: BucketName-APPID | Yes       |
| Key      | String | 객체 키                             | Yes       |
| UploadId | String | 객체 멀티파트 업로드 ID                  | Yes       |



## 고급 인터페이스(권장)

이 챕터에서는 업로드 및 복사 작업을 먹싱한 COS의 고급 인터페이스를 소개합니다. 사용자는 상응하는 매개변수만 설정하면 됩니다. 해당 인터페이스는 파일 크기에 따라 간편 업로드(복사)와 멀티파트 업로드(복사)를 결정합니다. 인터페이스 사용 전 [시작하기](https://intl.cloud.tencent.com/document/product/436/12266)에서 안내한 초기화 작업이 완료되었는지 확인하십시오.

### 객체 업로드

#### 메소드 프로토타입

```php
public Qcloud\Cos\Client upload(string $bucket, string $key, $body, array $options = array());
```
#### 기능 설명

해당 인터페이스는 용량이 작은 파일에는 간편 업로드 인터페이스를, 용량이 큰 파일에는 멀티파트 업로드 인터페이스를 호출합니다. 인터페이스 매개변수는 `PUT Object`와 `Upload Part` 인터페이스를 참고하십시오.

#### 매개변수 설명

| 매개변수 이름 | 유형   | 설명                               | 필수 입력 여부 |
| -------- | ------ | ---------------------------------- | -------- |
| bucket   | String | 버킷 이름. 형식: BucketName-APPID | Yes       |
| key      | String | 객체 키                             | Yes       |
| body     | Stream/String | 업로드한 콘텐츠 | Yes       |
| options     | Array | 추가된 설정 항목            | No       |



| options 매개변수 | 유형   | 설명                               | 필수 입력 여부 |
| -------- | ------ | ---------------------------------- | -------- |
| Progress         | Function      | 프로그레스 바 콜백. 매개변수는 총 크기($totalSize), 업로드된 크기($uploadedSize) | No       |
| PartSize         | Int      | 최소 멀티파트 파일 크기. 기본적으로 5M |No       |
| Concurrency         | Int      | 동시 실행 정도. 기본 설정값: 10 | No       |
| ACL                  | String      | 객체 ACL 설정. 예시: private, public-read                    | No       |
| CacheControl         | String      | 캐시 정책. Cache-Control 설정                                 | No       |
| ContentDisposition   | String      | 파일 이름. Content-Disposition 설정                           | No       |
| ContentEncoding      | String      | 인코딩 형식. Content-Encoding 설정                              | No       |
| ContentLanguage      | String      | 언어 유형. Content-Language 설정                              | No       |
| ContentLength        | Int         | 전송 길이 설정                                                 | No       |
| ContentType          | String      | 콘텐츠 유형. Content-Type 설정                                  | No       |
| Expires              | String      | Content-Expires 설정                                              | No       |
| Metadata             | Array       | 사용자 정의 파일 메타정보                                       | No     |
| StorageClass         | String      | 파일의 스토리지 유형이며(예시: STANDARD, STANDARD_IA, ARCHIVE), 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참고   | No       |
| ContentMD5           | Boolean      | 업로드된 파일의 MD5 값을 검사용으로 자동 생성 여부                                | No       |
| ServerSideEncryption | String      | 서버 암호화 방법                                               | No       |

#### 요청 예시

#### 예시1: 로컬에 객체 업로드

[//]: # ".cssg-snippet-transfer-upload-file"

```php
try {
    $result = $cosClient->upload(
        $bucket = 'examplebucket-1250000000', //형식: BucketName-APPID
        $key = 'exampleobject', //해당 key는 객체 키
        $body = fopen('path/to/localFile', 'rb')
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시2: 아카이브된 객체 업로드

[//]: # ".cssg-snippet-transfer-upload-file-archive"

```php
try {
    $result = $cosClient->upload(
        $bucket = 'examplebucket-1250000000', //형식: BucketName-APPID
        $key = 'exampleobject', //해당 key는 객체 키
        $body = fopen('path/to/localFile', 'rb'),
        $options = array(
            'StorageClass' => 'Archive'
        )
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 예시3: 멀티파트 크기별로 meta 업로드할 객체 지정

[//]: # ".cssg-snippet-transfer-upload-file-with-meta"

```php
try {
    $result = $cosClient->upload(
        $bucket = 'examplebucket-1250000000', //형식: BucketName-APPID
        $key = 'exampleobject', //해당 key는 객체 키
        $body = fopen('path/to/localFile', 'rb'),
        $options = array(
            'Metadata' => array(
                'string' => 'string',
            ),
            'PartSize' => 10 * 1024 * 1024
        )
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

### 일괄 업로드(로컬 폴더 업로드)

#### 기능 설명

로컬 폴더의 모든 파일을 COS에 업로드합니다.

#### 요청 예시

[//]: # ".cssg-snippet-transfer-upload-folder"

```php
<?php

require dirname( __FILE__ ) . '/../vendor/autoload.php';

$secretId = 'SECRETID';
//'Tencent Cloud API 키 SecretId';
$secretKey = 'SECRETKEY';
//'Tencent Cloud API 키 SecretKey';
$region = 'ap-beijing';
//기본 버킷 리전 설정
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //프로토콜 헤더, 기본값: http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey
        )
    )
);

function uploadfiles( $path, $cosClient ) {
    foreach ( scandir( $path ) as $afile ) {
        if ( $afile == '.' || $afile == '..' ) continue;
        if ( is_dir( $path.'/'.$afile ) ) {
            uploadfiles( $path.'/'.$afile, $cosClient );
        } else {
            $local_file_path = $path.'/'.$afile;
            $cos_file_path = $local_file_path;
            // 필요에 따라 업로드 경로 사용자 정의 스티칭
            try {
                $cosClient->upload(
                    $bucket = 'examplebucket-1250000000', //형식: BucketName-APPID
                    $key = $cos_file_path,
                    $body = fopen( $cos_file_path, 'rb' )
                );
            } catch ( \Exception $e ) {
                echo( $e );
            }
        }
    }
}

$local_path = '/data/home/folder';
uploadfiles( $local_path, $cosClient );
```

### 객체 다운로드(Range 다운로드)

#### 기능 설명

해당 인터페이스는 파일의 크기에 따라, 용량이 작은 파일은 객체 복사 인터페이스를, 용량이 큰 파일은 동시 실행 range 다운로드를 호출합니다. 인터페이스 매개변수는 `GET Object` 인터페이스를 참고하십시오.

#### 메소드 프로토타입

```php
public Qcloud\Cos\Client download(string $bucket, string $key, string $saveAs, array $options = array());
```

| 매개변수 이름 | 유형   | 설명                               | 필수 입력 여부 |
| -------- | ------ | ---------------------------------- | -------- |
| bucket   | String | 버킷 이름. 형식: BucketName-APPID | Yes       |
| key      | String | 객체 키                             | Yes       |
| saveAs     | String | 저장한 로컬 경로   | Yes       |
| options     | Array | 추가된 설정 항목            | No       |



| options 매개변수 | 유형   | 설명                               | 필수 입력 여부 |
| -------- | ------ | ---------------------------------- | -------- |
| Progress         | Function      | 프로그레스 바 콜백. 매개변수는 총 크기($totalSize), 업로드된 크기($downloadedSize) | No       |
| PartSize         | Int      | 최소 멀티파트 파일 크기. 기본적으로 5M |No       |
| Concurrency         | Int      | 동시 실행 정도. 기본 설정값: 10 | No       |
| ResumableDownload         | Bool      | 체크포인트부터 전송 재개 활성화 여부, 기본값: false | No      |
| ResumableTaskFile         | Int      | 체크포인트 파일 경로. 기본값: &lt;saveAs.cosresumabletask> | No       |


#### 요청 예시

[//]: # ".cssg-snippet-download-object"

```php
$printbar = function($totalSize, $downloadedSize) {
    printf("downloaded [%d/%d]\n", $downloadedSize, $totalSize);
};

try {
    $result = $cosClient->download(
        $bucket = 'examplebucket-1250000000', //형식: BucketName-APPID
        $key = 'exampleobject',
        $saveAs = $local_path,
        $options=['Progress' => $printbar, //프로그레스 바 지정
                  'PartSize' => 10 * 1024 * 1024, //멀티파트 크기
                  'Concurrency' => 5, //동시 실행 수
                  'ResumableDownload' => true, //체크포인트부터 이어서 전송 활성화 여부. 기본값: false
                  'ResumableTaskFile' => 'tmp.cosresumabletask' //체크포인트 파일 정보 경로. 기본 설정값: <localpath>.cosresumabletask
                ]
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

### 일괄 다운로드(COS에서 디렉터리 다운로드)

#### 기능 설명

COS 디렉터리와 해당 파일을 로컬 디스크에 다운로드합니다.

#### 요청 예시

[//]: # ".cssg-snippet-download-folder"

```php
$cos_path = 'cos/folder';
$nextMarker = '';
$isTruncated = true;

while ( $isTruncated ) {
    try {
        $result = $cosClient->listObjects(
            ['Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
            'Delimiter' => '',
            'EncodingType' => 'url',
            'Marker' => $nextMarker,
            'Prefix' => $cos_path,
            'MaxKeys' => 1000]
        );
    } catch ( \Exception $e ) {
        echo( $e );
    }
    $isTruncated = $result['IsTruncated'];
    $nextMarker = $result['NextMarker'];
    foreach ( $result['Contents'] as $content ) {
        $cos_file_path = $content['Key'];
        $local_file_path = $content['Key'];
        // 필요에 따라 다운로드 경로 사용자 정의 스티칭
        try {
            $result = $cosClient->download(
                $bucket = 'examplebucket-1250000000', //형식: BucketName-APPID
                $key = $cos_file_path,
                $saveAs = $local_file_path
            );
            echo ( $cos_file_path . "\n" );
        } catch ( \Exception $e ) {
            echo( $e );
        }
    }
}
```

### 객체 복사

#### 기능 설명

해당 인터페이스는 용량이 작은 파일에는 객체 복사 인터페이스를, 용량이 큰 파일에는 멀티파트 복사 인터페이스를 호출합니다. 이 기능은 종종 객체 속성을 수정하는 데 사용됩니다. 인터페이스 매개변수는 `PUT Object - Copy`와 `Upload Part - Copy` 인터페이스를 참고하십시오.

#### 요청 예시

#### 예시1: 객체 복사

[//]: # ".cssg-snippet-transfer-copy-object"

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //형식: BucketName-APPID
        $key = 'exampleobject', //해당 key는 객체 키
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceobject', 
        )
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

[//]: # ".cssg-snippet-transfer-copy-object-update-storage-class"

#### 예시2: COS 유형 변환

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //형식: BucketName-APPID
        $key = 'exampleobject', //해당 key는 객체 키
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'examplebucket-1250000000', 
            'Key' => 'exampleobject', 
        ),
        $options = array(
            'StorageClass' => 'Archive'
        )
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

[//]: # ".cssg-snippet-transfer-copy-object-update-metadata"

#### 예시3: COS 속성 수정

```php
try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //형식: BucketName-APPID
        $key = 'exampleobject', //해당 key는 객체 키
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceObject', 
        ),
        $options = array(
            'MetadataDirective' => 'Replaced',
            'Metadata' => array(
                'string' => 'string',
            ),
        )
    );
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```
