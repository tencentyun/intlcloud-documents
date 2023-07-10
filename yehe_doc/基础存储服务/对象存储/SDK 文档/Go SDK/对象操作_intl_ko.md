## 소개

본 문서는 객체의 고급 인터페이스, 간단한 작업, 멀티파트 작업의 API 개요 및 SDK 예시 코드를 제공합니다.

**간단한 작업**

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회   | 버킷의 일부 또는 모든 객체 조회            |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 간편한 객체 업로드   | Bucket에 Object(파일/객체) 업로드     |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | 객체 추가 업로드   | 멀티파트에 추가하는 방식으로 객체 업로드    |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회 | Object의 Meta 정보 조회                  |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 로컬에 Object(파일/객체) 다운로드        |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정   | 파일을 타깃 경로에 복사                        |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제   | Bucket에서 지정 Object(파일/객체) 삭제 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제   | Bucket에서 Object(파일/객체)를 일괄 삭제 |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 보관된 객체 복구 | 아카이브 유형의 객체 검색 및 액세스                      |


**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | Multipart Upload 작업 초기화     |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 파트 업로드       | 파일 멀티파트 업로드                         |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 하나의 멀티파트 업로드 작업 중지 및 이미 업로드한 파트 삭제 |


## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

버킷의 일부 또는 모든 객체를 조회합니다.

#### 메소드 프로토타입

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

#### 요청 예시1: 객체 리스트 나열

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

#### 요청 예시2: 디렉터리의 객체 나열
COS 자체에는 폴더 및 디렉터리의 개념이 없습니다. 사용자의 습관에 맞춰 세퍼레이터 /로 ‘폴더’를 구현할 수 있습니다.

[//]: # (.cssg-snippet-get-bucket2)
```go
var marker string
opt := &cos.BucketGetOptions{
    Prefix:  "folder/",  // prefix는 조회할 폴더를 의미합니다.
    Delimiter: "/",		 // delimiter는 세퍼레이터를 의미합니다. /로 설정하면 현재 디렉터리의 object를 나열하고, 공백으로 설정하면 전체 object를 나열합니다.
    MaxKeys: 1000,       // 순회할 최대 객체 수를 설정합니다. 한 번에 지원되는 listobject는 최대 1000개입니다.
}
isTruncated := true
for isTruncated {
    opt.Marker = marker
    v, _, err := c.Bucket.Get(context.Background(), opt)
    if err != nil {
        fmt.Println(err)
        break
    }
    for _, content := range v.Contents {
        fmt.Printf("Object: %v\n", content.Key)
    }
    // common prefix는 delimiter로 잘린 경로를 표시합니다. 예를 들어 delimiter를 /로 설정하면 common prefix는 모든 서브 디렉터리의 경로를 표시합니다.
    for _, commonPrefix := range v.CommonPrefixes {
        fmt.Printf("CommonPrefixes: %v\n", commonPrefix)
    }
    isTruncated = v.IsTruncated    // 아직 데이터가 있는지 여부
    marker = v.NextMarker          // 다음 요청의 시작 key 설정
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
| Prefix       | 기본값 null. 객체 키를 필터링해 접두사 prefix 값이 동일한 objects를 매칭 | string | No   |
| Delimiter    | 기본값 null. 유사 폴더가 필요한 경우 세퍼레이터 `/` 설정 가능                    | string | No   |
| EncodingType | 기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url                | string | No   |
| Marker       | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 objects list의 시작 위치 표시 | string | No   |
| MaxKeys      | 반환하는 최대 objects 수. 기본값: 최대 1000                    | int    | No   |

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
| Prefix         |기본값 null. 객체 키를 필터링해 접두사 prefix 값이 동일한 objects를 매칭 | string   |
| Marker         | 기본적으로 UTF-8 이진법 순서로 나열. 반환된 objects list의 시작 위치 표시 | string   |
| NextMarker     | IsTruncated가 true면 그다음 반환된 objects list의 시작 위치 표시 | string   |
| Delimiter      | 기본값 null. 유사 폴더가 필요한 경우 세퍼레이터 `/` 설정 가능                   | string   |
| MaxKeys        | 반환하는 최대 objects 수. 기본값: 최대 1000                    | int      |
| IsTruncated    | 반환하는 objects의 잘림 여부 표시                                | bool     |
| Contents       | 모든 object의 메타 정보를 포함한 list. 각 Object 유형별로 ETag, StorageClass, Key, Owner, LastModified, Size 등의 정보 포함 | []Object |
| CommonPrefixes | Prefix로 시작하고 Delimiter로 끝나는 Key를 동일한 종류로 분류     | []string |
| EncodingType   | 기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url                | string   |

### 객체 간편 업로드

#### 기능 설명

Object(파일/객체)를 버킷에 업로드합니다(PUT Object). 최대 5GB까지 지원하며, 5GB 이상인 객체는 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1) 또는 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)를 사용하여 업로드하십시오. 간편한 객체 업로드, 폴더 생성, 일괄 업로드 작업을 지원합니다.


#### 메소드 프로토타입

```go
func (s *ObjectService) Put(ctx context.Context, key string, r io.Reader, opt *ObjectPutOptions) (*Response, error)
func (s *ObjectService) PutFromFile(ctx context.Context, name string, filePath string, opt *ObjectPutOptions) (*Response, error)
```

#### 요청 예시1: 객체 업로드

[//]: # (.cssg-snippet-put-object)
```go
// Case1: Put을 사용해 객체 업로드
key := "exampleobject"
f, err := os.Open("../test")
opt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        ContentType:           "text/html",
    },
    ACLHeaderOptions: &cos.ACLHeaderOptions{
        // 기본 상속 버킷의 권한을 설정하지 않은 경우, 반드시 필요한 작업이 아니라면 파일 업로드 시 제한되지 않도록 단일 파일에 권한을 설정하지 않는 것을 권장합니다.
        XCosACL: "private",
    },
}
_, err = client.Object.Put(context.Background(), key, f, opt)
if err != nil {
    panic(err)
}

// Case 2: PUtFromFile을 사용해 COS에 로컬 파일 업로드
filepath := "./test"
_, err = client.Object.PutFromFile(context.Background(), key, filepath, opt)
if err != nil {
    panic(err)
}

// Case 3은 0바이트 파일을 업로드하고 입력 스트림 길이를 0으로 설정합니다. 
_, err = client.Object.Put(context.Background(), key, strings.NewReader(""), nil)
if err != nil {
    // ERROR
}
```

#### 요청 예시2: 폴더 생성

COS는 '/'로 구분하는 객체 경로를 가상 폴더로 인식합니다. 이러한 특성에 따라 이름이 '/'로 끝나는 빈 스트림을 업로드하면 COS에 빈 폴더를 생성할 수 있습니다.
```go
// 폴더 이름
name := "folder/"
// 크기가 0인 입력 스트림 전송
_, err := c.Object.Put(context.Background(), name, strings.NewReader(""), nil)
if err != nil {
	// ERROR
}
```

#### 요청 예시3: 가상 디렉터리에 업로드

'/'로 구분되는 객체 이름을 업로드하면 파일이 포함된 폴더를 자동으로 생성합니다. 해당 폴더에 새로운 파일을 추가할 경우 COS에 파일 업로드 시 Key를 해당 디렉터리 접두사로 입력하기만 하면 됩니다.
```go
dir := "exampledir/"
filename := "exampleobject"
key := dir + filename
f := strings.NewReader("test file")
_, err = c.Object.Put(context.Background(), key, f, nil)
if err != nil {
    // ERROR
}
```

#### 요청 예시4: 업로드 진행률 조회

```go
type SelfListener struct {
}
// 진행률 콜백 사용자 정의. ProgressChangedCallback 방법을 구현해야 합니다.
func (l *SelfListener) ProgressChangedCallback(event *cos.ProgressEvent) {
    switch event.EventType {
    case cos.ProgressDataEvent:
        fmt.Printf("\r[ConsumedBytes/TotalBytes: %d/%d, %d%%]",
                    event.ConsumedBytes, event.TotalBytes, event.ConsumedBytes*100/event.TotalBytes)
    case cos.ProgressFailedEvent:
        fmt.Printf("\nTransfer Failed: %v", event.Err)
    }
}
func main() {
    // 초기화
    ...
 
    // Case 1: 기본 콜백을 통한 업로드 진행률 조회
    key := "exampleobject"
    f, err := os.Open("../test")
    opt := &cos.ObjectPutOptions{
        ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
            ContentType:           "text/html",
            // 기본 진행률 콜백 함수 설정
            Listener:    &cos.DefaultProgressListener{},
        },
        ACLHeaderOptions: &cos.ACLHeaderOptions{
            // 기본 상속 버킷의 권한을 설정하지 않은 경우, 반드시 필요한 작업이 아니라면 파일 업로드 시 제한되지 않도록 단일 파일에 권한을 설정하지 않는 것을 권장합니다.
            XCosACL: "private",
        },
    }
    _, err = client.Object.Put(context.Background(), key, f, opt)
    if err != nil {
        panic(err)
    }

    // Case 2: 사용자 정의 방식을 통한 업로드 진행률 조회
    opt.Listener = &SelfListener{}
    filepath := "./test"
    _, err = client.Object.PutFromFile(context.Background(), key, filepath, opt)
    if err != nil {
        panic(err)
    }
}

```

#### 요청 예시5: 멀티 스레드 일괄 업로드

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
                        SecretID:  os.Getenv("SECRETID"),
                        SecretKey: os.Getenv("SECRETKEY"),
                },
        })
	// 파일 멀티 스레드 일괄 업로드
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

#### 매개변수 설명

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
    XCosTrafficLimit   int
    Listener           ProgressListener
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r                    | 파일 콘텐츠 업로드. 파일 스트림 또는 바이트 스트림이 될 수 있으며, r이 `bytes.Buffer/bytes.Reader/strings.Reader`가 아닌 경우 반드시 `opt.ObjectPutHeaderOptions.ContentLength`를 지정해야 함 | io.Reader   | Yes   |
| key                  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string      | Yes   |
| XCosACL              | 파일의 ACL 설정. 예: private, public-read, public-read-write   | string      | No   |
| XCosGrantFullControl | 권한을 부여받은 계정에 모든 권한 부여. 포맷: id="[OwnerUin]"                | string      | No   |
| XCosGrantRead        | 권한을 부여받은 계정에 읽기 권한 부여. 포맷: id="[OwnerUin]"                  | string      | No   |
| XCosStorageClass     | 파일의 스토리지 유형(STANDARD, STANDARD_IA, ARCHIVE) 설정. 기본값: STANDARD | string      | No   |
| Expires              | Content-Expires 설정                                         | string      | No   |
| CacheControl         | 캐시 정책. Cache-Control 설정                                 | string      | No   |
| ContentType          | 콘텐츠 유형. Content-Type 설정                                  | string      | No   |
| ContentDisposition   | 파일 이름. Content-Disposition 설정                           | string      | No   |
| ContentEncoding      | 인코딩 포맷. Content-Encoding 설정                              | string      | No   |
| ContentLength        | 전송 길이 설정                                                 | int64       | No   |
| XCosMetaXXX          | 사용자 정의한 파일 메타 정보. 반드시 x-cos-meta로 시작해야 하며, 그렇지 않을 경우 무시됨 | http.Header | No   |
| XCosTrafficLimit     | 단일 링크의 속도 제한 설정                                               | int    | No   |
| Listener             | 진행률 콜백 인터페이스                                                 | Struct | No   |

#### 반환 결과 설명

```go
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```

반환 결과를 통해 Response를 가져옵니다.

```go
resp, err := client.Object.Put(context.Background(), key, f, nil)
etag := resp.Header.Get("ETag")
exp := resp.Header.Get("x-cos-expiration")
```


| 매개변수 이름         | 매개변수 설명                         | 유형   |
| ---------------- | -------------------------------- | ------ |
| ETag             | 업로드된 파일의 MD5 값                | string |
| x-cos-expiration | 라이프사이클 설정 시 파일 만료 규칙 반환 | string |

### 객체 추가 업로드

#### 기능 설명

멀티파트 추가 방식으로 객체를 업로드합니다(APPEND Object).

#### 메소드 프로토타입

```go
func (s *ObjectService) Append(ctx context.Context, name string, position int, r io.Reader, opt *ObjectPutOptions) (int, *Response, error)
```
#### 요청 예시
```go
name := "exampleobject"
pos, _, err := c.Object.Append(context.Background(), name, 0, strings.NewReader("test1"), opt)
if err != nil {
    // ERROR
}
_, _, err = c.Object.Append(context.Background(), name, pos, strings.NewReader("test2"), opt)
if err != nil {
    // ERROR
}
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| name      |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg에서 객체 키는 doc/pic.jpg임 | string |
|  position  |  추가 작업의 시작점, 단위: 바이트. 최초 추가는 Position=0으로 설정하고 후속 추가는 Position을 현재 Object의 content-length로 설정  | int |
|  r         |  파일 콘텐츠 업로드. 파일 스트림 또는 바이트 스트림이 될 수 있으며, r이 bytes.Buffer/bytes.Reader/strings.Reader가 아닌 경우 반드시 opt.ObjectPutHeaderOptions.ContentLength를 지정해야 함 | io.Reader |
|  opt       |  매개변수 업로드, 자세한 내용은 ObjectPutOptions 참고 | struct |

#### 반환 결과 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
|  x-cos-next-append-position |  다음 추가 작업의 시작점, 단위: 바이트 | int |

### 객체 메타데이터 조회

#### 기능 설명

Object의 Meta 정보를 조회합니다(HEAD Object).

#### 메소드 프로토타입

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
| key             | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | Yes   |
| IfModifiedSince | 지정 시간 이후 수정될 경우에만 반환                                     | string | No   |

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
반환 결과를 통해 Response를 가져옵니다.
```go
resp, err := client.Object.Head(context.Background(), key, nil)
contentType := resp.Header.Get("Content-Type")
contentLength := resp.Header.Get("Content-Length")
etag := resp.Header.Get("ETag")
reqid := resp.Header.Get("X-Cos-Request-Id")

```

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| 파일 메타 정보 | Etag, X-Cos-Request-Id 등의 정보 및 설정한 파일 메타 정보를 포함한 파일의 메타 정보 획득 | string |


### 객체 다운로드

#### 기능 설명

Object(파일/객체)를 로컬에 다운로드합니다(GET Object). 간편 다운로드, 일괄 다운로드 작업을 지원합니다.

#### 메소드 프로토타입

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
// opt를 선택할 수 있으며, 특별히 설정하지 않을 경우 nil로 설정 가능
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
#### 요청 예시2: 객체 멀티 스레드 일괄 다운로드
```go
func download(wg *sync.WaitGroup, c *cos.Client, keysCh <-chan string) {
        defer wg.Done()
        for key := range keysCh {
                // 현재 디렉터리에 파일 다운로드. 파일명에 디렉터리 미포함
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
                        SecretID:  os.Getenv("SECRETID"),
                        SecretKey: os.Getenv("SECRETKEY"),
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

#### 요청 예시3: 단일 링크 속도 제한
```go

key := "exampleobject"
opt := &cos.ObjectGetOptions{
    // 속도 제한값은 819200 - 838860800, 즉 100KB/s - 100MB/s 범위에서 설정할 수 있으며, 이 범위를 넘으면 400 오류가 반환됨
    XCosTrafficLimit: 819200,
}
// opt를 선택할 수 있으며, 특별히 설정하지 않을 경우 nil로 설정 가능
// 1. 응답 본문에서 객체 가져오기
_, err := client.Object.GetToFile(context.Background(), key, "example.txt", opt)
if err != nil {
    panic(err)
}
```

#### 요청 예시4: 다운로드 진행률 가져오기

Go SDK는 콜백 방식을 통해 다운로드 진행률을 가져옵니다. 사용자가 cos.ProgressListener 인터페이스를 직접 구현해야 하며, 인터페이스의 정의는 다음과 같습니다.

```go
const (
    // 데이터 전송 시작
    ProgressStartedEvent ProgressEventType = iota
    // 데이터 전송 중
    ProgressDataEvent
    // 데이터 전송 완료. 단, 해당 API 호출 완료 표시 불가
    ProgressCompletedEvent
    // 데이터 전송 시 오류가 발생해야 반환
    ProgressFailedEvent
)
type ProgressEvent struct {
    EventType     ProgressEventType
    RWBytes       int64  // 읽기/쓰기 1회당 바이트
    ConsumedBytes int64  // 완료된 바이트
    TotalBytes    int64  // 총 바이트
    Err           error  // 오류
}
type ProgressListener interface {
    ProgressChangedCallback(event *ProgressEvent)
}
```
```go
type SelfListener struct {
}
// 진행률 콜백 사용자 정의. ProgressChangedCallback 방법을 구현해야 합니다.
func (l *SelfListener) ProgressChangedCallback(event *cos.ProgressEvent) {
    switch event.EventType {
    case cos.ProgressDataEvent:
        fmt.Printf("\r[ConsumedBytes/TotalBytes: %d/%d, %d%%]",
                    event.ConsumedBytes, event.TotalBytes, event.ConsumedBytes*100/event.TotalBytes)
    case cos.ProgressFailedEvent:
        fmt.Printf("\nTransfer Failed: %v", event.Err)
    }
}
func main() {
    // 초기화
    ... 

    key := "exampleobject"
    opt := &cos.ObjectGetOptions{
        ResponseContentType: "text/html",
        // 기본 방식을 사용해 진행률 조회
	Listener:    &cos.DefaultProgressListener{},
    }
    // opt를 선택할 수 있으며, 특별히 설정하지 않을 경우 nil로 설정 가능
    // 1. 응답 본문에서 객체 가져오기
    resp, err := client.Object.Get(context.Background(), key, opt)
    if err != nil {
        panic(err)
    }
    ioutil.ReadAll(resp.Body)
    resp.Body.Close()

    // 2. 로컬 파일에 객체 다운로드
    // 사용자 정의한 진행률 콜백 방법 사용
    opt.Listener = &SelfListener{}
    _, err = client.Object.GetToFile(context.Background(), key, "example.txt", opt)
    if err != nil {
        panic(err)
    }
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
    XCosTrafficLimit           int
    Listener                   ProgressListener
}
```

| 매개변수 이름                   | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
| key                        | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | Yes   |
| localfile                  | 객체를 로컬의 파일 이름으로 저장                                     | string | Yes   |
| ResponseContentType        | 응답 헤더의 Content-Type 설정                                    | string | No   |
| ResponseContentLanguage    | 응답 헤더의 Content-Language 설정                                | string | No   |
| ResponseExpires            | 응답 헤더의 Content-Expires 설정                                 | string | No   |
| ResponseCacheControl       | 응답 헤더의 Cache-Control 설정                                   | string | No   |
| ResponseContentDisposition | 응답 헤더의 Content-Disposition 설정                             | string | No   |
| ResponseContentEncoding    | 응답 헤더의 Content-Encoding 설정                                | string | No   |
| Range                      | 다운로드 파일의 범위 설정. 포맷: bytes=first-last                  | string | No   |
| IfModifiedSince            | 지정 시간 이후 수정될 경우에만 반환                                     | string | No   |
| XCosTrafficLimit           | 단일 링크의 속도 제한 설정                                               | int    | No   |
| Listener                   | 진행률 콜백 인터페이스                                                 | Struct | No   |

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
반환 결과를 통해 Response를 가져옵니다.
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
| Body       | 다운로드 파일의 콘텐츠                                               | StreamBody |
| 파일 메타 정보 | Etag, X-Cos-Request-Id 정보 등 파일의 메타 정보를 다운로드하고 설정한 파일 메타 정보 반환 | string |

### 객체 복사 설정

타깃 경로에 파일을 복사합니다(PUT Object-Copy).

#### 메소드 프로토타입

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
// 기본 상속 버킷의 권한을 설정하지 않은 경우, 반드시 필요한 작업이 아니라면 파일 업로드 시 제한되지 않도록 단일 파일에 권한을 설정하지 않는 것을 권장합니다.
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

#### 요청 예시3: 스토리지 유형 수정

>!표준 스토리지는 표준IA 스토리지, 인텔리전트 티어링 스토리지, 아카이브 스토리지 및 딥 아카이브 스토리지 등으로 수정할 수 있습니다. 아카이브 스토리지 또는 딥 아카이브 스토리지 객체를 다른 스토리지 유형으로 수정하려면 먼저 PostRestore를 사용하여 아카이브 스토리지 또는 딥 아카이브 스토리지 객체가 워밍업해야만 이 인터페이스를 사용하여 스토리지 유형 수정을 요청할 수 있습니다. 스토리지 유형에 대한 자세한 설명은 [스토리지 유형 개요](https://intl.cloud.tencent.com/ko/document/product/436/30925)를 참고하십시오.

```go
name := "exampleobject"
// 원본 객체 업로드
f := strings.NewReader("test")
_, err := client.Object.Put(context.Background(), name, f, nil)
assert.Nil(s.T(), err, "Test Failed")

sourceURL := fmt.Sprintf("%s/%s", client.BaseURL.BucketURL.Host, name)
opt := &cos.ObjectCopyOptions{
    &cos.ObjectCopyHeaderOptions{
        XCosMetadataDirective: "Replaced",
        XCosStorageClass: "Archive",        // 아카이브 유형으로 수정
    },
    nil,
}
_, _, err = client.Object.Copy(context.Background(), name, sourceURL, opt)
if err != nil {
    panic(err)
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
| key                             | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string      | Yes   |
| sourceURL                       | 복사할 원본 파일의 URL                                         | string      | Yes   |
| XCosACL                         | 파일의 ACL 설정. 예: private, public-read, public-read-write   | string      | No   |
| XCosGrantFullControl            | 권한을 부여받은 계정에 모든 권한 부여. 포맷: id="[OwnerUin]"                | string      | No   |
| XCosGrantRead                   | 권한을 부여받은 계정에 읽기 권한 부여. 포맷: id="[OwnerUin]"                  | string      | No   |
| XCosMetadataDirective           | 옵션값: Copy, Replaced: </br><li>Copy로 설정하는 경우, 설정된 사용자 메타데이터 정보를 무시하고 직접 파일 복사</br><li>Replaced로 설정하는 경우, 설정된 메타정보에 따라 메타데이터 수정</br>타깃 경로와 원본 경로가 같은 경우, 반드시 Replaced로 설정해야 합니다. | string      | Yes   |
| XCosCopySourceIfModifiedSince   | Object가 지정된 시간 이후에 수정될 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. XCosCopySourceIfNoneMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | string      | No   |
| XCosCopySourceIfUnmodifiedSince | Object가 지정된 시간 이후에 수정되지 않을 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. XCosCopySourceIfMatch 와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | string      | No   |
| XCosCopySourceIfMatch           | Object의 Etag와 일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. XCosCopySourceIfUnmodifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | string      | No   |
| XCosCopySourceIfNoneMatch       | Object의 Etag와 일치하지 않을 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. XCosCopySourceIfModifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다. | string      | No   |
| XCosStorageClass                | 파일의 스토리지 유형(STANDARD, STANDARD_IA, ARCHIVE) 설정. 기본값: STANDARD  | string      | No   |
| XCosMetaXXX                     | 사용자 정의한 파일 메타 정보                                       | http.Header | No   |
| XCosCopySource                  | 원본 파일의 URL 경로. versionid 하위 리소스로 이전 버전 지정 가능       | string      | No   |

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

#### 메소드 프로토타입

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

해당 요청은 폴더 안의 객체가 아닌 지정 key만 삭제합니다.

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
| key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | Yes   |

### 다수의 객체 삭제

#### 기능 설명

Bucket에서 다수의 Object(파일/객체)를 삭제합니다. 요청 1회당 최대 1000개의 Object를 일괄 삭제할 수 있습니다.

#### 메소드 프로토타입

```go
func (s *ObjectService) DeleteMulti(ctx context.Context, opt *ObjectDeleteMultiOptions) (*ObjectDeleteMultiResult, *Response, error)
```

#### 요청 예시1: 다수의 지정 객체 삭제

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
    // Boolean 값. 이 값으로 Quiet 모드의 실행 여부 결정
    // true 값이면 Quiet 모드 실행, false 값이면 Verbose 모드를 실행. 기본값: false
    // Quiet: true,
}

_, _, err := client.Object.DeleteMulti(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### 요청 예시2: 폴더 및 해당 파일 삭제

COS의 폴더는 객체 이름이 '/'로 구분되고 파일 시스템과 같은 경로를 생성하여 시뮬레이션됩니다. 따라서 폴더를 삭제하는 작업은 COS에서 동일한 접두사를 가진 객체를 일괄 삭제하는 것과 같습니다. 예를 들어, 'prefix/' 폴더는 접두사가 'prefix/'인 모든 객체를 대표하며 'prefix/' 삭제는 접두사가 'prefix/'인 모든 객체를 삭제한다는 의미입니다.
현재 COS Go SDK는 이러한 작업을 지원하는 인터페이스를 제공하지 않습니다. 그러나 기본 작업을 조합하여 이와 동일한 효과를 볼 수 있습니다.

```go
dir := "exampledir/"
var marker string
opt := &cos.BucketGetOptions{
    Prefix:  dir,
    MaxKeys: 1000,
}
isTruncated := true
for isTruncated {
    opt.Marker = marker
    v, _, err := c.Bucket.Get(context.Background(), opt)
    if err != nil {
        // Error
        break
    }
    for _, content := range v.Contents {
        _, err = c.Object.Delete(context.Background(), content.Key)
        if err != nil {
            // Error
        }
    }
    isTruncated = v.IsTruncated
    marker = v.NextMarker
}
```


#### 매개변수 설명

```go
type ObjectDeleteMultiOptions struct {
	Quiet   bool
	Objects []Object   
}
// Object에 객체의 메타 정보 저장
type Object struct {
	Key          string
    // 기타 매개변수는 해당 API와 관련 없음
}
```

| 매개변수 이름 | 매개변수 설명                                                     | 유형      | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| Quiet    | Boolean 값. 이 값으로 Quiet 모드의 실행 여부를 결정합니다. COS에서는 Verbose와 Quiet의 두 가지 모드의 응답 결과를 제공합니다.</br><li>Verbose 모드: 모든 Object의 삭제 결과 반환<br><li>Quiet 모드: 오류가 발생한 Object 정보만 반환</br>true 값이면 Quiet 모드를 실행하고, false 값이면 Verbose 모드를 실행합니다. 기본값: false | Boolean   | No   |
| Objects  | 삭제 예정인 모든 타깃 Object 정보 설명                           | Container | Yes   |
| Key      | 타깃 Object 파일 이름                                         | String    | Yes   |

#### 반환 결과 설명

업로드 파일의 속성:

```go
// ObjectDeleteMultiResult에 DeleteMulti의 결과 저장
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
| Errors         | 이번에 삭제 실패한 Object 정보 설명     | Container |
| Key            | 삭제 실패한 Object의 이름           | string    |
| Code           | 삭제 실패한 에러 코드                 | string    |
| Message        | 삭제 실패한 오류 정보                 | string    |



### 보관된 객체 복구 

#### 기능 설명

아카이브 유형의 객체를 검색하여 액세스합니다(POST Object restore).

#### 메소드 프로토타입

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
        // 기본 상속 버킷의 권한을 설정하지 않은 경우, 반드시 필요한 작업이 아니라면 파일 업로드 시 제한되지 않도록 단일 파일에 권한을 설정하지 않는 것을 권장합니다.
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
| key                  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | Yes   |
| ObjectRestoreOptions | 검색하는 임시 파일의 규칙                                     | struct | Yes   |
| Days                 | 임시 파일의 만료 시간                                       | int    | Yes   |
| CASJobParameters     | 복구 유형의 설정 정보                                       | struct | No   |
| Tier                 | 임시 파일의 검색 모드. CAS 유형의 데이터를 복구하는 경우 Expedited(고속), Standard(표준), Bulk(일괄) 세 가지 모드 중 선택할 수 있습니다. DEEP ARCHIVE 유형의 데이터를 복구하는 경우 Standard와 Bulk 중 선택할 수 있습니다. | string | No   |



## 멀티파트 작업

### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드 정보를 조회합니다(List Multipart Uploads).

#### 메소드 프로토타입

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
| Delimiter      | 구분 문자는 하나의 부호입니다. Object 이름에 지정 접두사가 포함되어 있고, 처음으로 나타난 delimiter 문자 사이의 Object가 하나의 요소(common prefix)가 됩니다. prefix가 없는 경우 경로의 처음부터 시작합니다. | string | No   |
| EncodingType   | 반환값의 인코딩 포맷 규정. 유효한 값: url                            | string | No   |
| Prefix         | 접두사가 Prefix인 Object key를 반환하도록 한정. prefix를 사용하여 조회할 경우 반환되는 key에는 Prefix가 포함되므로 주의해야 합니다. | string | No   |
| MaxUploads     | 반환하는 최대 multipart 수 설정. 유효한 값 범위: 1~1000, 기본값: 1000   | int | No   |
| KeyMarker      | upload-id-marker와 함께 사용합니다. </li><li>upload-id-marker 미지정 시, ObjectName 알파벳 순서가 key-marker보다 큰 항목 열거됩니다. </li><li>upload-id-marker 지정 시, ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거되고, ObjectName 알파벳 순서가 key-marker와 동일하고 UploadID가 upload-id-marker보다 큰 항목이 열거됩니다. | string | No   |
| UploadIDMarker | key-marker와 함께 사용합니다. </li><li>key-marker가 지정되지 않은 경우 upload-id-marker가 무시됩니다. </li><li>key-marker가 지정된 경우 ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거되고, ObjectName 알파벳 순서가 key-marker와 동일하고 UploadID가 upload-id-marker보다 큰 항목이 열거됩니다.</li> | string | No   |


#### 반환 결과 설명

```go
// ListMultipartUploadsResult에 ListMultipartUploads의 결과 저장
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
// Owner가 Bucket/Object's 소유자 정의
type Owner struct {
    ID          string
    DisplayName string
}
```

| 매개변수 이름           | 매개변수 설명                                                     | 유형      |
| ------------------ | ------------------------------------------------------------ | --------- |
| Bucket             | 멀티파트 업로드의 타깃 Bucket. 포맷: BucketName, 예: examplebucket-1250000000 | string    |
| EncodingType       | 기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url                | string    |
| KeyMarker          | 해당 key 값부터 시작하여 항목 열거                                      | string    |
| UploadIDMarker     | 해당 UploadId 값부터 시작하여 항목 열거                                 | string    |
| NextKeyMarker      | 반환 항목이 잘린 경우 NextKeyMarker를 반환하고 다음 항목의 시작점이 됨 | string    |
| NextUploadIDMarker | 반환 항목이 잘린 경우 UploadId를 반환하고 다음 항목의 시작점이 됨     | string    |
| MaxUploads         | 반환하는 멀티파트의 최대 수. 기본값: 최대 1000                       | string    |
| IsTruncated        | 반환하는 멀티파트의 잘림 여부 표시                                     | bool      |
| Uploads            | 모든 Upload 정보                                           | Container |
| Key                | Object 이름                                                | string    |
| UploadID           | 이번 멀티파트 업로드의 ID                                        | string    |
| Key                | 반환하는 멀티파트의 잘림 여부 표시                                     | bool      |
| StorageClass       | 멀티파트의 스토리지 클래스 표시. 열거 값: STANDARD, STANDARD_IA, ARCHIVE | string    |
| Initiator          | 이번 업로드 담당자의 정보 표시                                 | Container |
| Owner              | 해당 멀티파트 소유자 정보 표시                                 | Container |
| Initiated          | 멀티파트 업로드 시작 시간                                           | string    |
| Prefix             | 접두사가 Prefix인 Object key를 반환하도록 한정. Prefix를 사용하여 조회할 경우 반환되는 key에는 Prefix가 포함되므로 주의해야 합니다. | struct    |
| Delimiter          | 구분 문자는 하나의 부호입니다. object 이름에 지정 접두사가 포함되어 있고, 처음으로 나타난 delimiter 문자 사이의 object가 하나의 요소(common prefix)가 됩니다. prefix가 없는 경우 경로 처음부터 시작합니다. | string    |
| CommonPrefixes     |  prefix에서 delimiter 사이의 동일 경로를 같은 클래스로 분류하여 Common Prefix로 정의합니다. | string    |
| ID                 | 사용자의 고유 CAM 자격 ID                                       | string    |
| DisplayName        | 사용자 자격 ID의 약칭(UIN)                                    | string    |


### 객체 멀티파트 업로드

다음은 객체의 멀티파트 업로드 작업 내용입니다.

- 객체 멀티파트 업로드: 멀티파트 업로드를 초기화하고 멀티파트를 업로드하면 완료됩니다.
- 업로드된 파트를 삭제합니다.

>? 객체 멀티파트 업로드는 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)를 사용해 업로드할 수 있습니다(권장).
>

<span id="INIT_MULIT_UPLOAD"></span>
###  멀티파트 업로드 초기화 

#### 기능 설명

Multipart Upload 업로드 작업을 초기화하고 해당하는 uploadId를 가져옵니다(Initiate Multipart Upload).

#### 메소드 프로토타입

```go
func (s *ObjectService) InitiateMultipartUpload(ctx context.Context, name string, opt *InitiateMultipartUploadOptions) (*InitiateMultipartUploadResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-init-multi-upload)
```go
name := "exampleobject"
// opt를 선택할 수 있습니다. 기본 상속 버킷의 권한을 설정하지 않은 경우, 반드시 필요한 작업이 아니라면 파일 업로드 시 제한되지 않도록 단일 파일에 권한을 설정하지 않는 것을 권장합니다.
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
| key                  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string      | Yes   |
| XCosACL              | 파일의 ACL 설정. 예: private, public-read                       | string      | No   |
| XCosGrantFullControl | 권한을 부여받은 계정에 모든 권한 부여. 포맷: id="[OwnerUin]"                | string      | No   |
| XCosGrantRead        | 권한을 부여받은 계정에 읽기 권한 부여. 포맷: id="[OwnerUin]"                  | string      | No   |
| XCosStorageClass     | 파일의 스토리지 유형(STANDARD, STANDARD_IA, ARCHIVE) 설정. 기본값: STANDARD | string      | No   |
| Expires              | Content-Expires 설정                                         | string      | No   |
| CacheControl         | 캐시 정책. Cache-Control 설정                                 | string      | No   |
| ContentType          | 콘텐츠 유형. Content-Type 설정                                  | string      | No   |
| ContentDisposition   | 파일 이름. Content-Disposition 설정                           | string      | No   |
| ContentEncoding      | 인코딩 포맷. Content-Encoding 설정                              | string      | No   |
| ContentLength        | 전송 길이 설정                                                 | int64       | No   |
| XCosMetaXXX          | 사용자 정의한 파일 메타 정보. 반드시 x-cos-meta로 시작해야 하며, 그렇지 않을 경우 무시됨 | http.Header | No   |

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
| Bucket   | Bucket 이름. bucket-appid로 구성                            | string |
| Key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string |


<span id="MULIT_UPLOAD_PART"></span>
###  멀티파트 업로드 

객체를 멀티파트 업로드합니다(Upload Part).

#### 메소드 프로토타입

```go
func (s *ObjectService) UploadPart(ctx context.Context, key, uploadID string, partNumber int, r io.Reader, opt *ObjectUploadPartOptions) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-upload-part)
```go
// 참고: 멀티파트 업로드 최대 수는 10000개
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
| key           | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string    | Yes   |
| UploadId      | 멀티파트 업로드의 식별 ID. InitiateMultipartUpload에서 생성           | string    | Yes   |
| PartNumber    | 업로드하는 파트의 시리얼 넘버                                           | int       | Yes   |
| r             | 멀티파트 콘텐츠 업로드. 로컬 파일 스트림 또는 입력 스트림이 될 수 있으며, r이 `bytes.Buffer/bytes.Reader/strings.Reader`가 아닌 경우 반드시 opt.ContentLength을 지정해야 함 | io.Reader | Yes   |
| ContentLength | 전송 길이 설정                                                 | int64     | No   |

#### 반환 결과 설명

```go
{
    'ETag': 'string'
}
```
반환 결과를 통해 Response를 가져옵니다.
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

#### 메소드 프로토타입

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

| 매개변수 이름 | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | Yes   |
| UploadId | 멀티파트 업로드의 식별 ID. InitiateMultipartUpload에서 생성           | string | Yes   |
| EncodingType | 반환값의 인코딩 방식 규정           | string | No   |
| MaxParts | 한 번에 반환하는 최대 항목 수. 기본값: 1000           | string | No   |
| PartNumberMarker | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 Marker부터 시작           | string | No   |

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
| EncodingType         | 기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url                | string |
| Key                  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string |
| UploadId             | 멀티파트 업로드의 식별 ID. InitiateMultipartUpload에서 생성           | string |
| Initiator            | DisplayName, UIN, ID를 포함한 멀티파트 업로드 생성자                | struct |
| Owner                | DisplayName, UIN, ID를 포함한 파일 소유자의 정보               | struct |
| StorageClass         | 파일의 스토리지 유형(STANDARD, STANDARD_IA, ARCHIVE). 기본값: STANDARD | string |
| PartNumberMarker     | 기본값: 0. 첫 파트부터 멀티파트로 나열하며, PartNumberMarker의 다음 멀티파트부터 나열 | string    |
| NextPartNumberMarker | 다음에 나열하는 멀티파트의 시작 위치 표시                                 | string    |
| MaxParts             | 반환하는 멀티파트의 최대 수. 기본값: 최대 1000                       | string    |
| IsTruncated          | 반환하는 멀티파트의 잘림 여부 표시                                     | bool   |
| Part                 | ETag, PartNumber, Size, LastModified 등 업로드된 멀티파트 관련 정보 | struct |


<span id = "COMPLETE_MULIT_UPLOAD"></span>
###  멀티파트 업로드 완료 

#### 기능 설명

전체 파일의 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 메소드 프로토타입

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
| key                            | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | Yes   |
| UploadId                       | 멀티파트 업로드의 식별 ID. InitiateMultipartUpload에서 생성           | string | Yes   |
| CompleteMultipartUploadOptions | 모든 멀티파트의 ETag와 PartNumber 정보                           | struct | Yes   |

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
| Key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string |
| ETag     | 병합된 객체 고유의 태그값. 객체 콘텐츠의 MD5 검증값이 아니므로, 객체 고유성 검사에만 사용할 수 있음. 파일 콘텐츠 검증이 필요한 경우 업로드 과정에서 단일 파트의 ETag 값 검증 가능 | string |

<span id = "ABORT_MULIT_UPLOAD"></span>
###  멀티파트 업로드 중지 

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다(Abort Multipart Upload).

#### 메소드 프로토타입

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

| 매개변수 이름 | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | Yes   |
| UploadId | 멀티파트 업로드의 식별 ID                                            | string | Yes   |



## 고급 인터페이스(권장)

### 객체 업로드

#### 기능 설명

업로드 인터페이스는 파일 길이에 따라 자동으로 데이터를 분할하여 사용이 편리합니다. 사용자는 멀티파트 업로드의 모든 절차를 신경 쓸 필요가 없습니다. 파일 크기가 16MB를 초과하는 경우, 멀티파트 업로드를 사용하면 PartSize 매개변수를 통해 조정할 수 있습니다.

#### 메소드 프로토타입

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

```go
type MultiUploadOptions struct {
    OptIni             *InitiateMultipartUploadOptions
    PartSize           int64
    ThreadPoolSize     int
    CheckPoint         bool
}
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| key            | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | Yes   |
| filepath       | 로컬 파일명                                                   | string | Yes   |
| opt            | 객체 속성                                                     | Struct | No   |
| OptIni         | 객체 속성과 ACL 설정. 자세한 내용은 [InitiateMultipartUploadOptions](#.E6.96.B9.E6.B3.95.E5.8E.9F.E5.9E.8B9) 참고          | Struct | No   |
| PartSize       | 파트 크기(단위: MB). 사용자가 지정하지 않거나 partSize <= 0으로 지정하는 경우 Go SDK가 자동 분할. 최신 버전의 기본 크기는 16MB    | int    | No   |
| ThreadPoolSize | 스레드 풀 크기. 기본값: 1                                          | int    | No   |
| CheckPoint     | 중단 지점부터 이어서 전송 활성화 여부. 기본값: false                            | bool   | No   |

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
| Key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string |
| ETag     | 병합된 객체 고유의 태그값. 객체 콘텐츠의 MD5 검증값이 아니므로, 객체 고유성 검사에만 사용할 수 있음. 파일 콘텐츠 검증이 필요한 경우 업로드 과정에서 단일 파트의 ETag 값 검증 가능 | string |

### 객체 다운로드

#### 기능 설명

멀티파트 다운로드 인터페이스는 객체 길이에 따라 자동으로 Range를 사용해 데이터를 다운로드하여 동시 다운로드를 구현합니다. 객체가 16MB를 초과하는 경우, Range 방식으로 파일을 다운로드하면 PartSize 매개변수를 통해 조정할 수 있습니다.

#### 메소드 프로토타입

```go
func (s *ObjectService) Download(ctx context.Context, name string, filepath string, opt *MultiDownloadOptions) (*Response, error)
```

#### 요청 예시

[//]: # ".cssg-snippet-download-file"
```go
key := "exampleobject"
file := "localfile"

opt := &cos.MultiDownloadOptions{
	ThreadPoolSize: 5,
}
_, err := c.Object.Download(
	context.Background(), key, file, opt,
)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

```go
type MultiDownloadOptions struct {
    Opt            *ObjectGetOptions
    PartSize       int64
    ThreadPoolSize int
    CheckPoint     bool
    CheckPointFile string
}
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| name  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | Yes   |
| filepath       | 로컬 파일명                                                   | string | Yes   |
| opt            | 객체 매개변수 다운로드                                                 | Struct | No   |
| Opt            | 요청 매개변수. 자세한 내용은 [ObjectGetOptions](#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1) 참고          | Struct | No   |
| PartSize       | 파트 크기(단위: MB). 사용자가 지정하지 않거나 partSize <= 0으로 지정하는 경우 Go SDK가 자동 분할. 최신 버전 기본값은 16MB   | int64    | No   |
| ThreadPoolSize | 스레드 풀 크기. 기본값: 1                                          | int    | No   |
| CheckPoint     | 중단 지점부터 이어서 전송 활성화 여부. 기본값: false                                | bool   | No   |
| CheckPointFile | 중단 지점부터 이어서 전송 활성화 시, 다운로드 진행률을 저장하는 파일 경로 표시. 기본 경로: &lt;filepath>.cosresumabletask. 다운로드 완료 후 해당 진행률 파일은 삭제됨 | string   | No   |

#### 반환 결과 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| \*Response| http 응답. 해당 반환 결과를 통해 응답 상태 코드 및 응답 헤더 등의 정보 획득      | Struct |
| error    | 오류 정보. 정상 시 nil 반환                                      | Struct |



### 객체 이동

#### 기능 설명

객체 이동 사용 시나리오는 객체 복사+객체 삭제의 두 가지 인터페이스를 통해 실현됩니다.

#### 요청 예시

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


