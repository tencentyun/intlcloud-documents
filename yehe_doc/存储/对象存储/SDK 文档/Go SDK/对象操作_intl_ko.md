## 소개

본 문서는 객체에 대한 간단한 작업, 멀티파트 작업 등 기타 관련 작업의 API 개요 및 SDK 예시 코드를 제공합니다.

**간단한 작업**

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회   | 버킷의 일부 또는 모든 객체 조회            |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 간편한 객체 업로드   | Object(파일/객체)를 Bucket에 업로드     |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회 | Object의 Meta 정보 조회                  |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | Object(파일/객체)를 로컬에 다운로드        |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정   | 파일을 타깃 경로에 복사                        |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제   | Bucket에서 지정 Object(파일/객체) 삭제 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제   | Bucket에서 Object(파일/객체) 일괄 삭제 |

**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | Multipart Upload 작업 초기화     |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 파트 업로드       | 파일 멀티파트 업로드                         |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 멀티파트 업로드 작업 중지 및 업로드된 파트 삭제 |

**기타 작업**

| API                                                          | 작업명       | 작업 설명                                      |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 보관된 객체 복구 | 아카이브 유형의 객체 검색 및 액세스                      |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정 | Bucket에 있는 특정 Object(파일/객체)의 ACL 설정 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 조회 | Object(파일/객체)의 ACL 조회                |

## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

버킷의 일부 또는 모든 객체를 조회합니다.

#### 방법 모델

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-get-bucket)
```go
opt := &cos.BucketGetOptions{
    Prefix:  "test",
    MaxKeys: 100,
}
_, _, err := client.Bucket.Get(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

```go
type BucketGetOptions struct {
	Prefix       string 
	Delimiter    string 
	EncodingType string 
	Marker       string 
	MaxKeys      int    
}
```

| 매개변수 이름     | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Prefix       | 기본값 null. 객체 키를 필터링해 접두사 prefix가 동일한 objects를 매칭 | string | 아니요   |
| Delimiter    | 기본값 null. 시뮬레이션 폴더가 필요한 경우 세퍼레이터 `/` 설정 가능                    | string | 아니요   |
| EncodingType | 기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식 규정. 옵션값: url                | string | 아니요   |
| Marker       | 기본적으로 UTF-8 이진법 순서로 나열하며, 반환하는 objects list의 시작 위치 표시 | string | 아니요   |
| MaxKeys      | 반환하는 최대 objects 수량. 기본값: 최대 1000개                    | int    | 아니요   |

#### 반환 결과 설명

```go
type BucketGetResult struct {
	Name           string
	Prefix         string 
	Marker         string 
	NextMarker     string 
	Delimiter      string 
	MaxKeys        int
	IsTruncated    bool
	Contents       []Object 
	CommonPrefixes []string 
	EncodingType   string   
}
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형     |
| -------------- | ------------------------------------------------------------ | -------- |
| Name           | 버킷 이름. 포맷: BucketName-APPID, 예: examplebucket-1250000000 | string   |
| Prefix         | 기본값 null. 객체 키를 필터링해 접두사 prefix가 동일한 objects를 매칭 | string   |
| Marker         | 기본적으로 UTF-8 이진법 순서로 나열하며, 반환하는 objects list의 시작 위치 표시 | string   |
| NextMarker     | IsTruncated가 true인 경우, 다음 반환하는 objects list의 시작 위치 표시 | string   |
| Delimiter      | 기본값 null. 시뮬레이션 폴더가 필요한 경우 세퍼레이터 `/` 설정 가능                   | string   |
| MaxKeys        | 반환하는 최대 objects 수량. 기본값: 최대 1000개                    | int      |
| IsTruncated    | 반환하는 objects의 잘림 여부 표시                                | bool     |
| Contents       | 모든 object의 메타 정보 list를 포함하며, 각 Object 유형에는 ETag, StorageClass, Key, Owner, LastModified, Size 등이 포함됨 | []Object |
| CommonPrefixes | Prefix로 시작하고 Delimiter로 끝나는 모든 Key를 동일한 클래스로 분류     | []string |
| EncodingType   | 기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식 규정. 옵션값: url                | string   |

### 간편한 객체 업로드

#### 기능 설명

Object(파일/객체)를 버킷에 업로드합니다(PUT Object). 최대 5GB(포함)까지 지원하며, 5GB를 초과하는 객체는 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1) 또는 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)를 사용해 업로드하십시오. 간편한 객체 업로드, 폴더 생성, 일괄 업로드 작업을 지원합니다.


#### 방법 모델

```go
func (s *ObjectService) Put(ctx context.Context, key string, r io.Reader, opt *ObjectPutOptions) (*Response, error)
```

#### 요청 예시1: 객체 업로드

[//]: # (.cssg-snippet-put-object)
```go	
key := "exampleobject"
f, err := os.Open("../test")
opt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        ContentType: "text/html",
    },
    ACLHeaderOptions: &cos.ACLHeaderOptions{
        // 기본 상속 버킷의 권한을 설정하지 않은 경우 반드시 필요한 게 아니라면 파일 업로드 시 제한되지 않도록 단일 파일에 권한을 설정하지 않는 것을 권장합니다.
        XCosACL: "private",
    },
}
_, err = client.Object.Put(context.Background(), key, f, opt)
if err != nil {
    panic(err)
}
```
#### 요청 예시2: 폴더 생성
```go
// 폴더 이름
name := "folder/"
// 크기가 0인 입력 스트림 전송
_, err := c.Object.Put(context.Background(), name, strings.NewReader(""), nil)
if err != nil {
	// ERROR
}
```
#### 요청 예시3: 멀티 스레드 일괄 업로드
```
func upload(wg *sync.WaitGroup, c *cos.Client, files <-chan string) {
    defer wg.Done()
    for file := range files {
        name := "folder/" + file
	fd, err := os.Open(file)
        if err != nil {
            //ERROR
            continue
        }
        _, err = c.Object.Put(context.Background(), name, fd, nil)
        if err != nil {
            //ERROR
        }
    }
}
func main() {
        u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
        b := &cos.BaseURL{BucketURL: u}
        c := cos.NewClient(b, &http.Client{
                Transport: &cos.AuthorizationTransport{
                        SecretID:  os.Getenv("COS_SECRETID"),
                        SecretKey: os.Getenv("COS_SECRETKEY"),
                },
        })
	// 멀티 스레드 파일 일괄 업로드
        filesCh := make(chan string, 2)
        filePaths := []string{"test1", "test2", "test3"}
        var wg sync.WaitGroup
        threadpool := 2
        for i := 0; i < threadpool; i++ {
                wg.Add(1)
                go upload(&wg, c, filesCh)
        }
        for _, filePath := range filePaths {
                filesCh <- filePath
        }
        close(filesCh)
        wg.Wait()
}
```
```go
type ObjectPutOptions struct {
	*ACLHeaderOptions       
	*ObjectPutHeaderOptions 
}
type ACLHeaderOptions struct {
	XCosACL              string                           
    XCosGrantRead        string
    XCosGrantWrite       string 
    XCosGrantFullControl string                                           
} 
type ObjectPutHeaderOptions struct {
	CacheControl       string 
	ContentDisposition string 
	ContentEncoding    string 
	ContentType        string 
	ContentLength      int64  
	Expires            string 
	// 사용자 정의한 x-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r                    | 파일 콘텐츠 업로드. 파일 스트림 또는 바이트 스트림이 될 수 있으며, r이 `bytes.Buffer/bytes.Reader/strings.Reader`가 아닌 경우 반드시 `opt.ObjectPutHeaderOptions.ContentLength`를 지정해야 합니다. | io.Reader   | 예   |
| key                  | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string      | 예   |
| XCosACL              | 파일 ACL 설정. 예: private, public-read, public-read-write   | string      | 아니요   |
| XCosGrantFullControl | 권한이 부여된 사용자에게 모든 권한 부여. 포맷: id="[OwnerUin]"                | string      | 아니요   |
| XCosGrantRead        | 권한이 부여된 사용자에게 읽기 권한 부여. 포맷: id="[OwnerUin]"                  | string      | 아니요   |
| XCosStorageClass     | 파일의 스토리지 유형 설정. STANDARD, STANDARD_IA, ARCHIVE, 기본값: STANDARD | string      | 아니요   |
| Expires              | Content-Expires 설정                                         | string      | 아니요   |
| CacheControl         | 캐시 정책, Cache-Control 설정                                 | string      | 아니요   |
| ContentType          | 콘텐츠 유형, Content-Type 설정                                  | string      | 아니요   |
| ContentDisposition   | 파일 이름, Content-Disposition 설정                           | string      | 아니요   |
| ContentEncoding      | 인코딩 포맷, Content-Encoding 설정                              | string      | 아니요   |
| ContentLength        | 전송 길이 설정                                                 | int64       | 아니요   |
| XCosMetaXXX          | 사용자 정의한 파일 메타 정보는 반드시 x-cos-meta로 시작해야 하며, 그렇지 않을 경우 무시됩니다. | http.Header | 아니요   |

#### 반환 결과 설명

```go
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```
반환 결과 Response로 획득합니다.
```go
resp, err := client.Object.Put(context.Background(), key, f, nil)
etag := resp.Header.Get("ETag")
exp := resp.Header.Get("x-cos-expiration")
```
| 매개변수 이름         | 매개변수 설명                         | 유형   |
| ---------------- | -------------------------------- | ------ |
| ETag             | 업로드한 파일의 MD5 값                | string |
| x-cos-expiration | 라이프사이클 설정 후 파일 만료 규칙 반환 | string |

### 객체 메타데이터 조회

#### 기능 설명

Object의 Meta 정보를 조회합니다(HEAD Object).

#### 방법 모델

```go
func (s *ObjectService) Head(ctx context.Context, key string, opt *ObjectHeadOptions) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-head-object)
```go
key := "exampleobject"
_, err := client.Object.Head(context.Background(), key, nil)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

```go
type ObjectHeadOptions struct {
	IfModifiedSince string 
}
```

| 매개변수 이름        | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| key             | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string | 예   |
| IfModifiedSince | 지정 시간 이후 수정될 경우에만 반환                                     | string | 아니요   |

#### 반환 결과 설명

```go
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```
반환 결과 Response로 획득합니다.
```go
resp, err := client.Object.Head(context.Background(), key, nil)
contentType := resp.Header.Get("Content-Type")
contentLength := resp.Header.Get("Content-Length")
etag := resp.Header.Get("ETag")
reqid := resp.Header.Get("X-Cos-Request-Id")

```

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| 파일 메타 정보 | Etag와 X-Cos-Request-Id 등의 정보 및 설정한 파일 메타 정보를 포함한 파일의 메타 정보 획득 | string |

### 객체 다운로드

#### 기능 설명

Object(파일/객체)를 로컬에 다운로드합니다(GET Object). 간편 다운로드, 일괄 다운로드 작업을 지원합니다.

#### 방법 모델

```go
func (s *ObjectService) Get(ctx context.Context, key string, opt *ObjectGetOptions) (*Response, error)

func (s *ObjectService) GetToFile(ctx context.Context, key, localfile string, opt *ObjectGetOptions) (*Response, error)
```

#### 요청 예시1: 객체 다운로드

[//]: # (.cssg-snippet-get-object)
```go
key := "exampleobject"
opt := &cos.ObjectGetOptions{
    ResponseContentType: "text/html",
    Range:               "bytes=0-3",
}
// opt를 선택할 수 있으며, 특별한 설정이 없는 경우 nil로 설정 가능
// 1. 응답 본문에서 객체 가져오기
resp, err := client.Object.Get(context.Background(), key, opt)
if err != nil {
    panic(err)
}
ioutil.ReadAll(resp.Body)
resp.Body.Close()

// 2. 로컬 파일에 객체 다운로드
_, err = client.Object.GetToFile(context.Background(), key, "example.txt", nil)
if err != nil {
    panic(err)
}
```
#### 요청 예시2: 멀티 스레드로 객체 일괄 다운로드
```go
func download(wg *sync.WaitGroup, c *cos.Client, keysCh <-chan string) {
        defer wg.Done()
        for key := range keysCh {
                // 현재 디렉터리로 파일 다운로드, 파일 이름에 디렉터리 미포함
                _, filename := filepath.Split(key)
                _, err := c.Object.GetToFile(context.Background(), key, filename, nil)
                if err != nil {
                	// ERROR
                }
        }
}
func main() {
        u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
        b := &cos.BaseURL{BucketURL: u}
        c := cos.NewClient(b, &http.Client{
                Transport: &cos.AuthorizationTransport{
                        SecretID:  os.Getenv("COS_SECRETID"),
                        SecretKey: os.Getenv("COS_SECRETKEY"),
                },
        })
        keysCh := make(chan string, 2)
        keys := []string{"folder/exampleobject1", "folder/exampleobject2", "folder/exampleobject3"}
        var wg sync.WaitGroup
        threadpool := 2
        for i := 0; i < threadpool; i++ {
                wg.Add(1)
                go download(&wg, c, keysCh)
        }
        for _, key := range keys {
                keysCh <- key
        }
        close(keysCh)
        wg.Wait()
}
```
#### 매개변수 설명

```go
type ObjectGetOptions struct {
	ResponseContentType        string 
	ResponseContentLanguage    string 
	ResponseExpires            string 
	ResponseCacheControl       string 
	ResponseContentDisposition string 
	ResponseContentEncoding    string 
	Range                      string 
	IfModifiedSince            string 
}
```

| 매개변수 이름                   | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
| key                        | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string | 예   |
| localfile                  | 객체를 로컬에 저장할 파일 이름                                     | string | 예   |
| ResponseContentType        | 응답 헤더의 Content-Type 설정                                    | string | 아니요   |
| ResponseContentLanguage    | 응답 헤더의 Content-Language 설정                                | string | 아니요   |
| ResponseExpires            | 응답 헤더의 Content-Expires 설정                                 | string | 아니요   |
| ResponseCacheControl       | 응답 헤더의 Cache-Control 설정                                   | string | 아니요   |
| ResponseContentDisposition | 응답 헤더의 Content-Disposition 설정                             | string | 아니요   |
| ResponseContentEncoding    | 응답 헤더의 Content-Encoding 설정                                | string | 아니요   |
| Range                      | 파일 다운로드 범위 설정. 포맷: bytes=first-last                  | string | 아니요   |
| IfModifiedSince            | 지정 시간 이후 수정될 경우에만 반환                                     | string | 아니요   |

#### 반환 결과 설명

```go
{
    'Body': '',
    'Accept-Ranges': 'bytes',
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Range': 'bytes 0-16086/16087',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```
반환 결과 Response로 획득합니다.
```go
resp, err := client.Object.Get(context.Background(), key, nil)
body, _ := ioutil.ReadAll(resp.Body)
contentType := resp.Header.Get("Content-Type")
contentLength := resp.Header.Get("Content-Length")
etag := resp.Header.Get("ETag")
reqid := resp.Header.Get("X-Cos-Request-Id")

```
| 매개변수 이름   | 매개변수 설명                                                     | 유형       |
| ---------- | ------------------------------------------------------------ | ---------- |
| Body       | 파일의 콘텐츠 다운로드                                               | StreamBody |
| 파일 메타 정보 | Etag와 X-Cos-Request-Id 등의 정보를 포함한 파일의 메타 정보를 다운로드하고 설정된 파일 메타 정보 반환 | string     |

### 객체 복사 설정

타깃 경로에 파일을 복사합니다(PUT Object-Copy).

#### 방법 모델

```go
func (s *ObjectService) Copy(ctx context.Context, key, sourceURL string, opt *ObjectCopyOptions) (*ObjectCopyResult, *Response, error)
```

#### 요청 예시1: 객체 간편 복사

[//]: # (.cssg-snippet-copy-object)
```go
name := "exampleobject"
// 원본 객체 업로드
f := strings.NewReader("test")
_, err := client.Object.Put(context.Background(), name, f, nil)
assert.Nil(s.T(), err, "Test Failed")

sourceURL := fmt.Sprintf("%s/%s", client.BaseURL.BucketURL.Host, name)
dest := "example_dest"
// 기본 상속 버킷의 권한을 설정하지 않은 경우 반드시 필요한 게 아니라면 파일 업로드 시 제한되지 않도록 단일 파일에 권한을 설정하지 않는 것을 권장합니다.
// opt := &cos.ObjectCopyOptions{}
_, _, err = client.Object.Copy(context.Background(), dest, sourceURL, nil)
if err != nil {
    panic(err)
}
```
#### 요청 예시2: 객체 이동
```go
source := "test/oldfile"
f := strings.NewReader("test")
// 파일 업로드
_, err := c.Object.Put(context.Background(), source, f, nil)
if err != nil {
    // Error
}

// 객체 이동
dest := "test/newfile"
soruceURL := fmt.Sprintf("%s/%s", u.Host, source)
_, _, err := c.Object.Copy(context.Background(), dest, soruceURL, nil)
if err == nil {
	    _, err = c.Object.Delete(context.Background(), source, nil)
 	if err != nil {
 		// Error
 	}
}
```

#### 매개변수 설명

```go
type ObjectCopyOptions struct {
	*ObjectCopyHeaderOptions 
	*ACLHeaderOptions        
}
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
type ObjectCopyHeaderOptions struct {
	XCosMetadataDirective           string 
	XCosCopySourceIfModifiedSince   string 
	XCosCopySourceIfUnmodifiedSince string 
	XCosCopySourceIfMatch           string 
	XCosCopySourceIfNoneMatch       string 
	XCosStorageClass                string 
	// 사용자 정의한 x-cos-meta-* header
	XCosMetaXXX    				    *http.Header 
	XCosCopySource 					string      
}
```

| 매개변수 이름                        | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| ------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| key                             | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string      | 예   |
| sourceURL                       | 복사할 원본 파일의 URL 설명                                         | string      | 예   |
| XCosACL                         | 파일 ACL 설정. 예: private, public-read, public-read-write   | string      | 아니요   |
| XCosGrantFullControl            | 권한이 부여된 사용자에게 모든 권한 부여. 포맷: id="[OwnerUin]"                | string      | 아니요   |
| XCosGrantRead                   | 권한이 부여된 사용자에게 읽기 권한 부여. 포맷: id="[OwnerUin]"                  | string      | 아니요   |
| XCosMetadataDirective           | 옵션값: Copy, Replaced</br><li>Copy로 설정 시, 설정된 사용자 메타데이터 정보를 무시하고 바로 복사합니다.</br><li>Replaced로 설정 시, 설정된 메타 정보에 따라 메타데이터를 수정합니다.</br>타깃 경로와 원본 경로가 동일한 경우 반드시 Replaced로 설정해야 합니다. | string      | 예   |
| XCosCopySourceIfModifiedSince   | Object가 지정된 시간 이후에 수정될 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. XCosCopySourceIfNoneMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | string      | 아니요   |
| XCosCopySourceIfUnmodifiedSince | Object가 지정된 시간 이후에 수정되지 않을 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. XCosCopySourceIfMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | string      | 아니요   |
| XCosCopySourceIfMatch           | Object의 Etag와 일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. XCosCopySourceIfUnmodifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | string      | 아니요   |
| XCosCopySourceIfNoneMatch       | Object의 Etag와 일치하지 않을 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. XCosCopySourceIfModifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | string      | 아니요   |
| XCosStorageClass                | 파일의 스토리지 유형 설정. STANDARD, STANDARD_IA, ARCHIVE, 기본값: STANDARD  | string      | 아니요   |
| XCosMetaXXX                     | 사용자 정의한 파일 메타 정보                                       | http.Header | 아니요   |
| XCosCopySource                  | 원본 파일 URL 경로. versionid 하위 리소스로 이전 버전 지정 가능       | string      | 아니요   |

#### 반환 결과 설명

업로드 파일의 속성:

```go
type ObjectCopyResult struct {
    ETag         string 
    LastModified string
}
```
| 매개변수 이름     | 매개변수 설명                   | 유형   |
| ------------ | -------------------------- | ------ |
| ETag         | 파일의 MD5 값 복사          | string |
| LastModified | 파일의 최종 수정 시간 복사 | string |

### 단일 객체 삭제

#### 기능 설명

Bucket에서 지정 Object(객체/폴더)를 삭제합니다.

#### 방법 모델

```go
func (s *ObjectService) Delete(ctx context.Context, key string) (*Response, error)
```

#### 요청 예시1: 객체 삭제

[//]: # (.cssg-snippet-delete-object)
```go
key := "exampleobject"
_, err := client.Object.Delete(context.Background(), key)
if err != nil {
    panic(err)
}
```

#### 요청 예시2: 폴더 삭제
```go
key := "folder/"
_, err := c.Object.Delete(context.Background(), key)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string | 예   |

### 다수의 객체 삭제

#### 기능 설명

Bucket에서 다수의 Object(파일/객체)를 삭제합니다. 요청 한 번에 최대 1000개의 Object 일괄 삭제를 지원합니다.

#### 방법 모델

```go
func (s *ObjectService) DeleteMulti(ctx context.Context, opt *ObjectDeleteMultiOptions) (*ObjectDeleteMultiResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-delete-multi-object)
```go
var objects []string
objects = append(objects, []string{"a", "b", "c"}...)
obs := []cos.Object{}
for _, v := range objects {
    obs = append(obs, cos.Object{Key: v})
}
opt := &cos.ObjectDeleteMultiOptions{
    Objects: obs,
    // Boolean 값. 이 값으로 Quiet 모드 실행 여부 결정
    // true 값이면 Quiet 모드 실행, false 값이면 Verbose 모드 실행. 기본값: false
    // Quiet: true,
}

_, _, err := client.Object.DeleteMulti(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

```go
type ObjectDeleteMultiOptions struct {
	Quiet   bool
	Objects []Object   
}
// Object에 객체 메타 정보 저장
type Object struct {
	Key          string
    // 기타 매개변수는 이 API와 관련 없음
}
```

| 매개변수 이름 | 매개변수 설명                                                     | 유형      | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| Quiet    | Boolean 값. 이 값으로 Quiet 모드 실행 여부를 결정합니다. 응답 결과로 COS에서 Verbose와 Quiet 두 가지 모드를 제공합니다.</br><li>Verbose 모드는 모든 Object의 삭제 결과를 반환합니다.<br><li>Quiet 모드는 오류가 발생한 Object 정보만 반환합니다.</br>true 값이면 Quiet 모드를 실행하고, false 값이면 Verbose 모드를 실행합니다. 기본값: false | Boolean   | 아니요   |
| Objects  | 삭제 예정인 모든 타깃 Object 정보 설명                           | Container | 예   |
| Key      | 타깃 Object 파일 이름                                         | String    | 예   |

#### 반환 결과 설명

업로드 파일의 속성:

```go
// ObjectDeleteMultiResult에 DeleteMulti 결과 저장
type ObjectDeleteMultiResult struct {	
	DeletedObjects []Object
	Errors         []struct {
		Key     string
		Code    string
		Message string
	}
}
```

| 매개변수 이름       | 매개변수 설명                           | 유형      |
| -------------- | ---------------------------------- | --------- |
| DeletedObjects | 삭제 예정인 모든 타깃 Object 정보 설명 | Container |
| Errors         | 이번 삭제에 실패한 Object 정보 설명     | Container |
| Key            | 삭제 실패한 Object 이름           | string    |
| Code           | 삭제 실패한 에러 코드                 | string    |
| Message        | 삭제 실패한 오류 정보                 | string    |

## 멀티파트 작업

### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드 정보를 조회합니다(List Multipart Uploads).

#### 방법 모델

```go
func (s *BucketService) ListMultipartUploads(ctx context.Context, opt *ListMultipartUploadsOptions) (*ListMultipartUploadsResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-list-multi-upload)
```go
_, _, err := client.Bucket.ListMultipartUploads(context.Background(), nil)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

```go
type ListMultipartUploadsOptions struct {
	Delimiter      string
	EncodingType   string
	Prefix         string
	MaxUploads     int
	KeyMarker      string
	UploadIDMarker string                                         
}
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Delimiter      | 구분 문자는 하나의 부호로, Object 이름에 지정한 접두사가 포함되어 있고 처음으로 나타난 delimiter 부호 사이의 Object가 하나의 요소(common prefix)가 됩니다. prefix가 없는 경우 경로 시작점부터 시작합니다. | string | 아니요   |
| EncodingType   | 반환값의 인코딩 포맷 규정. 유효한 값: url                            | string | 아니요   |
| Prefix         | Prefix를 접두사로 하는 Object key에 한정하여 반환. prefix를 사용하여 조회할 경우 반환되는 key에 Prefix가 포함되므로 주의해야 합니다. | string | 아니요   |
| MaxUploads     | 반환하는 최대 multipart 수량 설정. 유효한 값 범위: 1~1000, 기본값: 1000   | int | 아니요   |
| KeyMarker      | upload-id-marker와 함께 사용합니다.</li><li>upload-id-marker가 지정되지 않은 경우 ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거됩니다.</li><li>upload-id-marker가 지정된 경우 ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거됩니다. ObjectName 알파벳 순서가 key-marker와 동일하고 UploadID가 upload-id-marker보다 큰 항목이 열거됩니다. | string | 아니요   |
| UploadIDMarker | key-marker와 함께 사용합니다.</li><li>key-marker가 지정되지 않은 경우 upload-id-marker를 무시합니다.</li><li>key-marker가 지정된 경우 ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거됩니다. ObjectName 알파벳 순서가 key-marker와 동일하고 UploadID는 upload-id-marker보다 큰 항목이 열거됩니다. | string | 아니요   |


#### 반환 결과 설명

```go
// ListMultipartUploadsResult에 ListMultipartUploads 결과 저장
type ListMultipartUploadsResult struct {
	Bucket             string
	EncodingType       string
	KeyMarker          string
	UploadIDMarker     string
    NextKeyMarker      string
    NextUploadIDMarker string
    MaxUploads         int
    IsTruncated        bool
    Uploads            []struct {
    	Key          string
    	UploadID     string
    	StorageClass string
    	Initiator    *Initiator
    	Owner        *Owner
    	Initiated    string
    }
    Prefix         string
    Delimiter      string
    CommonPrefixes []string 
}
// Owner와 동일한 구조 사용
type Initiator Owner
// Owner에서 Bucket/Object의 소유자 정의
type Owner struct {
	ID          string
	DisplayName string
}
```

| 매개변수 이름           | 매개변수 설명                                                     | 유형      |
| ------------------ | ------------------------------------------------------------ | --------- |
| Bucket             | 멀티파트 업로드의 타깃 Bucket. 포맷: BucketName, 예: examplebucket-1250000000 | string    |
| EncodingType       | 기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식 규정. 옵션값: url                | string    |
| KeyMarker          | 해당 key 값부터 항목 열거                                      | string    |
| UploadIDMarker     | 해당 UploadId 값부터 항목 열거                                 | string    |
| NextKeyMarker      | 반환하는 항목이 잘리는 경우 NextKeyMarker를 다음 항목 시작점으로 반환 | string    |
| NextUploadIDMarker | 반환하는 항목이 잘리는 경우 UploadId를 다음 항목 시작점으로 반환     | string    |
| MaxUploads         | 반환하는 최대 멀티파트 수. 기본값: 최대 1000개                       | string    |
| IsTruncated        | 반환하는 멀티파트의 잘림 여부 표시                                     | bool      |
| Uploads            | 모든 Upload 정보                                           | Container |
| Key                | Object 이름                                                | string    |
| UploadID           | 이번 멀티파트 업로드의 식별 ID                                        | string    |
| Key                | 반환하는 멀티파트의 잘림 여부 표시                                     | bool      |
| StorageClass       | 멀티파트의 스토리지 클래스 표시. 열거 값: STANDARD, STANDARD_IA, ARCHIVE | string    |
| Initiator          | 이번 업로드 요청자 정보 표시                                 | Container |
| Owner              | 해당 멀티파트 소유자 정보 표시                                 | Container |
| Initiated          | 멀티파트 업로드 시작 시간                                           | string    |
| Prefix             | Prefix를 접두사로 하는 Objectkey에 한정하여 반환. prefix를 사용하여 조회할 경우 반환되는 key에 Prefix가 포함되므로 주의해야 합니다. | struct    |
| Delimiter          | 구분 문자는 하나의 부호로, object 이름에 지정한 접두사가 포함되어 있고 처음으로 나타난 delimiter 부호 사이의 object가 하나의 요소(common prefix)가 됩니다. prefix가 없는 경우 경로 시작점부터 시작합니다. | string    |
| CommonPrefixes     | prefix부터 delimiter 사이의 동일 경로를 같은 클래스로 분류하여 Common Prefix로 정의합니다. | string    |
| ID                 | 사용자 고유의 CAM 신분 ID                                       | string    |
| DisplayName        | 사용자 신분 ID의 약칭(UIN)                                    | string    |


### 객체 멀티파트 업로드

객체 멀티파트 업로드에는 다음 작업이 포함됩니다.

- 객체 멀티파트 업로드: 멀티파트 업로드를 초기화하고 파트를 업로드한 후 멀티파트 업로드를 완료합니다.
- 업로드된 멀티파트를 삭제합니다.

>?객체 멀티파트 업로드 시에는 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) 업로드(권장)를 사용할 수도 있습니다.


<span id="INIT_MULIT_UPLOAD"></span>
###  멀티파트 업로드 초기화 

#### 기능 설명

Multipart Upload 작업을 초기화하여 해당하는 uploadId를 획득합니다(Initiate Multipart Upload).

#### 방법 모델

```go
func (s *ObjectService) InitiateMultipartUpload(ctx context.Context, name string, opt *InitiateMultipartUploadOptions) (*InitiateMultipartUploadResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-init-multi-upload)
```go
name := "exampleobject"
// opt를 선택할 수 있습니다. 기본 상속 버킷의 권한을 설정하지 않은 경우 반드시 필요한 게 아니라면 파일 업로드 시 제한되지 않도록 단일 파일에 권한을 설정하지 않는 것을 권장합니다.
v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil)
if err != nil {
    panic(err)
}
UploadID = v.UploadID
```

#### 매개변수 설명

```go
type InitiateMultipartUploadOptions struct {
	*ACLHeaderOptions       
	*ObjectPutHeaderOptions 
}
type ACLHeaderOptions struct {
	XCosACL              string                           
	XCosGrantRead        string
	XCosGrantWrite       string 
	XCosGrantFullControl string                                           
} 
type ObjectPutHeaderOptions struct {
	CacheControl       string 
	ContentDisposition string 
	ContentEncoding    string 
	ContentType        string 
	ContentLength      int64   
	Expires            string 
	// 사용자 정의한 x-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}

```

| 매개변수 이름             | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| key                  | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string      | 예   |
| XCosACL              | 파일 ACL 설정. 예: private, public-read                       | string      | 아니요   |
| XCosGrantFullControl | 권한이 부여된 사용자에게 모든 권한 부여. 포맷: id="[OwnerUin]"                | string      | 아니요   |
| XCosGrantRead        | 권한이 부여된 사용자에게 읽기 권한 부여. 포맷: id="[OwnerUin]"                  | string      | 아니요   |
| XCosStorageClass     | 파일의 스토리지 유형 설정. STANDARD, STANDARD_IA, ARCHIVE, 기본값: STANDARD | string      | 아니요   |
| Expires              | Content-Expires 설정                                         | string      | 아니요   |
| CacheControl         | 캐시 정책, Cache-Control 설정                                 | string      | 아니요   |
| ContentType          | 콘텐츠 유형, Content-Type 설정                                  | string      | 아니요   |
| ContentDisposition   | 파일 이름, Content-Disposition 설정                           | string      | 아니요   |
| ContentEncoding      | 인코딩 포맷, Content-Encoding 설정                              | string      | 아니요   |
| ContentLength        | 전송 길이 설정                                                 | int64       | 아니요   |
| XCosMetaXXX          | 사용자 정의한 파일 메타 정보는 반드시 x-cos-meta로 시작해야 하며, 그렇지 않을 경우 무시됩니다. | http.Header | 아니요   |

#### 반환 결과 설명

```go
type InitiateMultipartUploadResult struct {
	Bucket   string
	Key      string
	UploadID string
} 
```

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| UploadId | 멀티파트 업로드의 식별 ID                                            | string |
| Bucket   | Bucket 이름은 bucket-appid로 구성                            | string |
| Key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string |


<span id="MULIT_UPLOAD_PART"></span>
###  멀티파트 업로드 

객체를 멀티파트 업로드합니다(Upload Part).

#### 방법 모델

```go
func (s *ObjectService) UploadPart(ctx context.Context, key, uploadID string, partNumber int, r io.Reader, opt *ObjectUploadPartOptions) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-upload-part)
```go
// 참고: 최대 멀티파트 업로드 수량 10000개
key := "exampleobject"
f := strings.NewReader("test hello")
// opt 선택 가능
resp, err := client.Object.UploadPart(
    context.Background(), key, UploadID, 1, f, nil,
)
if err != nil {
    panic(err)
}
PartETag = resp.Header.Get("ETag")
```

#### 매개변수 설명

```go
type ObjectUploadPartOptions struct {
    ContentLength   int64
}
```

| 매개변수 이름      | 매개변수 설명                                                     | 유형      | 필수 입력 여부 |
| ------------- | ------------------------------------------------------------ | --------- | ---- |
| key           | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string    | 예   |
| UploadId      | 멀티파트 업로드의 식별 ID는 InitiateMultipartUpload에서 생성           | string    | 예   |
| PartNumber    | 업로드하는 멀티파트의 시리얼 넘버                                           | int       | 예   |
| r             | 멀티파트 콘텐츠 업로드. 로컬 파일 스트림 또는 입력 스트림이 될 수 있으며, r이 `bytes.Buffer/bytes.Reader/strings.Reader`가 아닌 경우 반드시 opt.ContentLength를 지정해야 합니다. | io.Reader | 예   |
| ContentLength | 전송 길이 설정                                                 | int64     | 아니요   |

#### 반환 결과 설명

```go
{
    'ETag': 'string'
}
```
반환 결과 Response로 획득합니다.
```go
resp, err := client.Object.UploadPart(context.Background(), key, UploadID, 1, f, nil)
etag := resp.Header.Get("ETag")
```
| 매개변수 이름 | 매개변수 설명          | 유형   |
| -------- | ----------------- | ------ |
| ETag     | 업로드된 멀티파트의 MD5 값 | string |


<span id = "LIST_MULIT_UPLOAD"></span>
###  업로드된 파트 조회 

#### 기능 설명

특정 멀티파트 업로드 작업에서 업로드된 파트를 조회합니다(List Parts).

#### 방법 모델

```go
func (s *ObjectService) ListParts(ctx context.Context, name, uploadID string, opt *ObjectListPartsOptions) (*ObjectListPartsResult, *Response, error)

```

#### 요청 예시

[//]: # (.cssg-snippet-list-parts)
```go
key := "exampleobject"
_, _, err := client.Object.ListParts(context.Background(), key, UploadID, nil)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

```go
type ObjectListPartsOptions struct {
	EncodingType     string
	MaxParts         string
	PartNumberMarker string                                      
}
```

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string | 예   |
| UploadId | 멀티파트 업로드의 식별 ID는 InitiateMultipartUpload에서 생성           | string | 예   |
| EncodingType | 반환값의 인코딩 방식 규정           | string | 아니요   |
| MaxParts | 한 번에 반환하는 최대 항목 수량. 기본값: 1000           | string | 아니요   |
| PartNumberMarker | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 marker부터 시작됩니다.           | string | 아니요   |

#### 반환 결과 설명

```go
type ObjectListPartsResult struct {
	Bucket               string
	EncodingType         string
	Key                  string
	UploadID             string
	Initiator            *Initiator
	Owner                *Owner
	StorageClass         string
	PartNumberMarker     string
	NextPartNumberMarker string
	MaxParts             string
	IsTruncated          bool
	Parts                []Object
}
type Initiator struct {
	UIN         string
	ID          string
	DisplayName string
}
type Owner struct {
	UIN         string
	ID          string
	DisplayName string
}
type Object struct {
	Key          string
	ETag         string
	Size         int
	PartNumber   int
	LastModified string
	StorageClass string 
	Owner        *Owner
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   |
| -------------------- | ------------------------------------------------------------ | ------ |
| Bucket               | 버킷 이름. 포맷: BucketName-APPID, 예: examplebucket-1250000000 | string |
| EncodingType         | 기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식 규정. 옵션값: url                | string |
| Key                  | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string |
| UploadId             | 멀티파트 업로드의 식별 ID는 InitiateMultipartUpload에서 생성           | string |
| Initiator            | DisplayName, UIN, ID를 포함한 멀티파트 업로드 생성자                | struct |
| Owner                | DisplayName, UIN, ID를 포함한 파일 소유자               | struct |
| StorageClass         | 파일의 스토리지 유형. STANDARD, STANDARD_IA, ARCHIVE, 기본값: STANDARD | string |
| PartNumberMarker     | 기본값: 0. 첫 파트부터 멀티파트로 나열하며, PartNumberMarker의 다음 멀티파트부터 나열 | string    |
| NextPartNumberMarker | 다음에 나열하는 멀티파트의 시작 위치 표시                                 | string    |
| MaxParts             | 반환하는 최대 멀티파트 수. 기본값: 최대 1000개                       | string    |
| IsTruncated          | 반환하는 멀티파트의 잘림 여부 표시                                     | bool   |
| Part                 | ETag, PartNumber, Size, LastModified 등 업로드된 멀티파트 관련 정보 | struct |


<span id = "COMPLETE_MULIT_UPLOAD"></span>
###  멀티파트 업로드 완료 

#### 기능 설명

전체 파일의 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 방법 모델

```go
func (s *ObjectService) CompleteMultipartUpload(ctx context.Context, key, uploadID string, opt *CompleteMultipartUploadOptions) (*CompleteMultipartUploadResult, *Response, error)

```

#### 요청 예시

[//]: # (.cssg-snippet-complete-multi-upload)
```go
// 멀티파트 업로드 완료
key := "exampleobject"
uploadID := UploadID

opt := &cos.CompleteMultipartUploadOptions{}
opt.Parts = append(opt.Parts, cos.Object{
	PartNumber: 1, ETag: PartETag},
)

_, _, err := client.Object.CompleteMultipartUpload(
	context.Background(), key, uploadID, opt,
)
if err != nil {
	panic(err)
}
```

#### 매개변수 설명

```go
type CompleteMultipartUploadOptions struct {
	Parts   []Object 
}
type Object struct { 
	ETag         string 
	PartNumber   int     
}
```

| 매개변수 이름                       | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| key                            | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string | 예   |
| UploadId                       | 멀티파트 업로드의 식별 ID는 InitiateMultipartUpload에서 생성           | string | 예   |
| CompleteMultipartUploadOptions | 모든 멀티파트의 ETag와 PartNumber 정보                           | struct | 예   |

#### 반환 결과 설명

```go
type CompleteMultipartUploadResult struct {
	Location string
	Bucket   string
	Key      string
	ETag     string
}

```

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URL 주소                                                     | string |
| Bucket   | 버킷 이름. 포맷: BucketName-APPID, 예: examplebucket-1250000000 | string |
| Key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string |
| ETag     | 병합된 객체 고유의 태그값. 이 값은 객체 콘텐츠의 MD5 검증 값이 아니며, 객체 고유성 검사에만 사용할 수 있습니다. 파일 콘텐츠 검증이 필요한 경우 업로드 과정에서 단일 멀티파트의 ETag 값을 검증할 수 있습니다. | string |

<span id = "ABORT_MULIT_UPLOAD"></span>
###  멀티파트 업로드 중지 

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다(Abort Multipart Upload).

#### 방법 모델

```go
func (s *ObjectService) AbortMultipartUpload(ctx context.Context, key, uploadID string) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-abort-multi-upload)
```go
key := "exampleobject"
// Abort
_, err := client.Object.AbortMultipartUpload(context.Background(), key, UploadID)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string | 예   |
| UploadId | 멀티파트 업로드의 식별 ID                                            | string | 예   |

## 기타 작업

### 보관된 객체 복구 

#### 기능 설명

아카이브 유형의 객체를 검색하여 액세스합니다(POST Object restore).

#### 방법 모델

```go
func (s *ObjectService) PostRestore(ctx context.Context, key string, opt *ObjectRestoreOptions) (*Response, error) 
```

#### 요청 예시

[//]: # (.cssg-snippet-restore-object)
```go
key := "example_restore"
f, err := os.Open("../test")
if err != nil {
    panic(err)
}
opt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        ContentType:      "text/html",
        XCosStorageClass: "ARCHIVE", //아카이브 유형
    },
    ACLHeaderOptions: &cos.ACLHeaderOptions{
        // 기본 상속 버킷의 권한을 설정하지 않은 경우 반드시 필요한 게 아니라면 파일 업로드 시 제한되지 않도록 단일 파일에 권한을 설정하지 않는 것을 권장합니다.
        XCosACL: "private",
    },
}
// 아카이브 다이렉트 업로드
_, err = client.Object.Put(context.Background(), key, f, opt)
if err != nil {
    panic(err)
}

opts := &cos.ObjectRestoreOptions{
    Days: 2,
    Tier: &cos.CASJobParameters{
        // Standard, Exepdited and Bulk
        Tier: "Expedited",
    },
}
// 아카이브 복구
_, err = client.Object.PostRestore(context.Background(), key, opts)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

```go
type ObjectRestoreOptions struct {        
    Days    int               
    Tier    *CASJobParameters 
}
type CASJobParameters struct {
    Tier    string 
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| key                  | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string | 예   |
| ObjectRestoreOptions | 검색하는 임시 파일 규칙                                     | struct | 예   |
| Days                 | 임시 파일의 만료 시간                                       | int    | 예   |
| CASJobParameters     | 복구 유형의 설정 정보                                       | struct | 아니요   |
| Tier                 | 임시 파일 검색 모드. 옵션값은 'Expedited'(고속 모드), 'Standard'(표준 모드), 'Bulk'(일괄 모드) 세 가지 모드가 있습니다. | string | 아니요   |

### 객체 ACL 설정

#### 기능 설명

객체 액세스 권한 제어 리스트를 설정합니다(PUT Object acl).

#### 방법 모델

```go
func (s *ObjectService) PutACL(ctx context.Context, key string, opt *ObjectPutACLOptions) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-put-object-acl)
```go
// 1. 요청 헤더로 설정
opt := &cos.ObjectPutACLOptions{
    Header: &cos.ACLHeaderOptions{
        XCosACL: "private",
    },
}
key := "exampleobject"
_, err := client.Object.PutACL(context.Background(), key, opt)
if err != nil {
    panic(err)
}
// 2. 요청 본문으로 설정
opt = &cos.ObjectPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            ID: "qcs::cam::uin/100000000001:uin/100000000001",
        },
        AccessControlList: []cos.ACLGrant{
            {
                Grantee: &cos.ACLGrantee{
                    Type: "RootAccount",
                    ID:   "qcs::cam::uin/100000760461:uin/100000760461",
                },

                Permission: "FULL_CONTROL",
            },
        },
    },
}

_, err = client.Object.PutACL(context.Background(), key, opt)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

```go
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| key                  | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string | 예   |
| XCosACL              | Object의 ACL 설정. 예: private, public-read                  | string | 아니요   |
| XCosGrantFullControl | 권한이 부여된 사용자에게 모든 권한 부여. 포맷: id="[OwnerUin]"                | string | 아니요   |
| XCosGrantRead        | 권한이 부여된 사용자에게 읽기 권한 부여. 포맷: id="[OwnerUin]"                  | string | 아니요   |
| ACLXML               | 지정 계정에 Bucket 액세스 권한 부여. 자세한 포맷은 get object acl의 반환 결과를 확인하십시오. | struct | 아니요   |

### 객체 ACL 조회

#### 기능 설명

Object(파일/객체)의 ACL(GET Object acl)을 조회합니다.

#### 방법 모델

```go
func (s *ObjectService) GetACL(ctx context.Context, key string) (*ObjectGetACLResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-get-object-acl)
```go
key := "exampleobject"
_, _, err := client.Object.GetACL(context.Background(), key)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string | 예   |

#### 반환 결과 설명

```go
type ACLXml struct {
	Owner             *Owner
	AccessControlList []ACLGrant 
}
type Owner struct { 
	ID          string 
	DisplayName string
}
type ACLGrant struct {
	Grantee    *ACLGrantee
	Permission string
}
type ACLGrantee struct {
	Type        string 
	ID          string 
	DisplayName string
    UIN         string 
}
```

| 매개변수 이름          | 매개변수 설명                                                     | 유형   |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner             | DisplayName, ID를 포함한 Bucket 소유자 정보                  | struct |
| AccessControlList | Grantee, Permission을 포함한 Bucket 권한 부여자 정보          | struct |
| Grantee           | DisplayName, Type, ID, UIN을 포함한 권한 부여자 정보          | struct |
| Type              | CanonicalUser 또는 Group 유형의 권한 부여자 유형            | string |
| ID                | Type이 CanonicalUser일 때 해당하는 권한 부여자 ID                | string |
| DisplayName       | 권한 부여자 이름                                             | string |
| UIN               | Type이 Group일 때 해당하는 권한 부여자 UIN                       | string |
| Permission        | 권한 부여자가 가지고 있는 Bucket 권한. 옵션값: FULL_CONTROL(읽기 및 쓰기 권한), WRITE(쓰기 권한), READ(읽기 권한) | string |



## 고급 인터페이스(권장)

### 객체 업로드

#### 기능 설명

업로드 인터페이스가 파일 길이에 따라 자동으로 데이터를 분할하여 사용자의 사용 진입 장벽을 낮춰주므로 사용자는 멀티파트 업로드의 모든 절차에 주의하지 않아도 됩니다.

#### 방법 모델

```go
func (s *ObjectService) Upload(ctx context.Context, key string, filepath string, opt *MultiUploadOptions) (*CompleteMultipartUploadResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-transfer-upload-file)
```go
key := "exampleobject"
file := "../test"

_, _, err := client.Object.Upload(
    context.Background(), key, file, nil,
)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| key            | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string | 예   |
| filepath       | 로컬 파일명                                                   | string | 예   |
| opt            | 객체 속성                                                     | Struct | 아니요   |
| OptIni         | 객체 속성과 ACL 설정. 자세한 내용은 [InitiateMultipartUploadOptions](#.E6.96.B9.E6.B3.95.E5.8E.9F.E5.9E.8B9)를 참조하십시오.          | Struct | 아니요   |
| PartSize       | 파트 크기. 단위: MB, 사용자가 지정하지 않거나 partSize <= 0으로 지정하는 경우 Go SDK가 자동으로 분할합니다.    | int    | 아니요   |
| ThreadPoolSize | 스레드 풀 크기. 기본값: 1                                          | int    | 아니요   |

#### 반환 결과 설명

```go
type CompleteMultipartUploadResult struct {
	Location string
	Bucket   string
	Key      string
	ETag     string
}

```

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URL 주소                                                     | string |
| Bucket   | 버킷 이름. 포맷: BucketName-APPID, 예: examplebucket-1250000000 | string |
| Key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자입니다. 예: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg입니다. | string |
| ETag     | 병합된 객체 고유의 태그값. 이 값은 객체 콘텐츠의 MD5 검증 값이 아니며, 객체 고유성 검사에만 사용할 수 있습니다. 파일 콘텐츠 검증이 필요한 경우 업로드 과정에서 단일 멀티파트의 ETag 값을 검증할 수 있습니다. | string |
