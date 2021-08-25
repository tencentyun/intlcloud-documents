## 소개

본 문서는 객체 태그에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름       | 작업 설명                     |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | 객체 태그 설정 | 업로드한 객체의 태그 설정       |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | 객체 태그 조회 | 지정한 객체의 기존 태그 조회 |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | 객체 태그 삭제 | 지정한 객체의 기존 태그 삭제 |


## 객체 태그 설정

#### 기능 설명

COS는 기존 객체의 태그 설정을 지원합니다. PUT Object tagging 인터페이스에 객체 태그로 키 값 쌍을 추가하면 기존 객체 리소스를 그룹화하고 관리하는 데 도움이 됩니다. 자세한 내용은 [객체 태그 개요](https://intl.cloud.tencent.com/document/product/436/35665)를 참고하십시오.

#### 메소드 프로토타입

```go
func (s *ObjectService) PutTagging(ctx context.Context, name string, opt *ObjectPutTaggingOptions, id ...string) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-put-object-tagging)
```go
// Case1, PutTagging을 통한 클라우드 객체 태그 설정
opt := &cos.ObjectPutTaggingOptions{
    TagSet: []cos.ObjectTaggingTag{
        {
            Key:   "test_k2",
            Value: "test_v2",
        },
        {
            Key:   "test_k3",
            Value: "test_v3",
        },
    },
}
name := "example"
_, err := c.Object.PutTagging(context.Background(), name, opt)
if err != nil {
    //ERROR
}

// Case2 업로드 시 객체 태그 설정
name = "test/example"
f := strings.NewReader("test")
popt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        XOptionHeader: &http.Header{},
    },
}
popt.XOptionHeader.Add("x-cos-tagging", "Key1=Value1&Key2=Value2")
_, err = c.Object.Put(context.Background(), name, f, popt)
```

#### 매개변수 설명

```go
type ObjectPutTaggingOptions struct {
    TagSet  []ObjectTaggingTag
}
type BucketTaggingTag struct {
    Key   string
    Value string
}
```
| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| name     | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String | 예   |
| TagSet   | 태그 집합. 최대 10개의 태그 지원    | Array  | 예   |
| Key      | 태그 키. 길이는 128바이트 이하이며 알파벳, 숫자, 공백, 덧셈 기호, 뺄셈 기호, 언더바, 등호, 마침표, 콜론, 슬래시 지원 | String | 예   |
| Value    | 태그 값. 길이는 256바이트 이하이며 알파벳, 숫자, 공백, 덧셈 기호, 뺄셈 기호, 언더바, 등호, 마침표, 콜론, 슬래시 지원 | String | 예   |

## 객체 태그 조회

#### 기능 설명

GET Object tagging 인터페이스는 지정한 객체의 기존 태그를 조회하는 데 사용합니다.

#### 메소드 프로토타입

```go
func (s *ObjectService) GetTagging(ctx context.Context, name string, id ...string) (*ObjectGetTaggingResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-get-object-tagging)
```go
name := "example"
res, _, err := c.Object.GetTagging(context.Background(), name)
if err != nil {
    //ERROR
}
```

#### 결과 설명
```go
type ObjectGetTaggingResult struct {
    TagSet  []ObjectTaggingTag
}
type BucketTaggingTag struct {
    Key   string
    Value string
}
```

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| TagSet   | 태그 집합. 최대 10개의 태그 지원    | Array  |
| Key      | 태그 키. 길이는 128바이트 이하이며, 알파벳, 숫자, 공백, 덧셈 기호, 뺄셈 기호, 언더바, 등호, 마침표, 콜론, 슬래시 지원 | String |
| Value    | 태그 값. 길이는 256바이트 이하이며, 알파벳, 숫자, 공백, 덧셈 기호, 뺄셈 기호, 언더바, 등호, 마침표, 콜론, 슬래시 지원 | String |

## 객체 태그 삭제

#### 기능 설명

DELETE Object tagging 인터페이스는 지정 객체의 기존 태그를 삭제하는 데 사용합니다.

#### 메소드 프로토타입

```go
func (s *ObjectService) DeleteTagging(ctx context.Context, name string, id ...string) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-delete-object-tagging)
```go
name := "example"
_, err = c.Object.DeleteTagging(context.Background(), name)
if err != nil {
    //ERROR
}
```
