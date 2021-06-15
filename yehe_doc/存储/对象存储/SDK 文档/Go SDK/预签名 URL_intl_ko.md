## 소개
Go SDK는 사전 서명된 URL 요청을 가져오는 인터페이스를 제공합니다. 자세한 내용은 본 문서의 예시를 참조하십시오.



## 사전 서명된 URL 요청 가져오기 

```go
func (s *ObjectService) GetPresignedURL(ctx context.Context, httpMethod, name, ak, sk string, expired time.Duration, opt interface{}) (*url.URL, error)
```

#### 매개변수 설명
| 매개변수 이름           | 유형                         | 설명                            |
| ------------------ | ---------------------------- | ------------------------------- |
| httpMethod            | string                   | HTTP 요청 방법                        |
| name | string           | HTTP 요청 경로. 즉, 객체 키                 |
| ak             | string                       | SecretId                    |
| sk               | string                       | SecretKey         |
| expired            | time.Duration | 서명 유효 기간             |
| opt    | interface{} | 확장 항목, nil 입력 가능 |

## 영구 키로 사전 서명된 요청 예시

#### 요청 예시 업로드

[//]: # (.cssg-snippet-get-presign-upload-url)
```go
ak := "COS_SECRETID"
sk := "COS_SECRETKEY"

name := "exampleobject"
ctx := context.Background()
f := strings.NewReader("test")

// 1. 일반적인 방식을 통한 객체 업로드
_, err := client.Object.Put(ctx, name, f, nil)
if err != nil {
    panic(err)
}
// 사전 서명된 URL 가져오기
presignedURL, err := client.Object.GetPresignedURL(ctx, http.MethodPut, name, ak, sk, time.Hour, nil)
if err != nil {
    panic(err)
}
// 2. 사전 서명 방식을 통한 객체 업로드
data := "test upload with presignedURL"
f = strings.NewReader(data)
req, err := http.NewRequest(http.MethodPut, presignedURL.String(), f)
if err != nil {
    panic(err)
}
// 사용자가 요청 헤더를 직접 설정할 수 있습니다.
req.Header.Set("Content-Type", "text/html")
_, err = http.DefaultClient.Do(req)
if err != nil {
    panic(err)
}
```

#### 요청 예시 다운로드

[//]: # (.cssg-snippet-get-presign-download-url)
```go
ak := "COS_SECRETID"
sk := "COS_SECRETKEY"
name := "exampleobject"
ctx := context.Background()
// 1. 일반적인 방식을 통한 객체 다운로드
resp, err := client.Object.Get(ctx, name, nil)
if err != nil {
    panic(err)
}
bs, _ := ioutil.ReadAll(resp.Body)
resp.Body.Close()
// 사전 서명된 URL 가져오기
presignedURL, err := client.Object.GetPresignedURL(ctx, http.MethodGet, name, ak, sk, time.Hour, nil)
if err != nil {
    panic(err)
}
// 2. 사전 서명된 URL을 통한 객체 다운로드
resp2, err := http.Get(presignedURL.String())
if err != nil {
    panic(err)
}
bs2, _ := ioutil.ReadAll(resp2.Body)
resp2.Body.Close()
if bytes.Compare(bs2, bs) != 0 {
    panic(errors.New("content is not consistent"))
}
```

## 임시 키로 사전 서명된 요청 예시

```go
// 사용자는 tag 방식을 통해 요청 매개변수 또는 요청 헤더를 서명에 삽입할 수 있습니다.
type URLToken struct {
	SessionToken string `url:"x-cos-security-token,omitempty" header:"-"`
}

func main() {
	// 보유한 임시 키로 변경
	tak := os.Getenv("COS_SECRETID")
	tsk := os.Getenv("COS_SECRETKEY")
	token := &URLToken{
		SessionToken: "<token>",
	}
	u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{})

	name := "exampleobject"
	ctx := context.Background()

	// 방법1 tag를 통한 x-cos-security-token 설정
	// Get presigned
	presignedURL, err := c.Object.GetPresignedURL(ctx, http.MethodGet, name, tak, tsk, time.Hour, token)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
		return
	}
	// Get object by presinged url
	resp, err := http.Get(presignedURL.String())
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}
	defer resp.Body.Close()
	fmt.Println(presignedURL.String())
	fmt.Printf("resp:%v\n", resp)

	// 방법2 PresignedURLOptions를 통한 x-cos-security-token 설정
    // PresignedURLOptions는 사용자에게 추가 요청 매개변수와 요청 헤더를 제공합니다.
	opt := &cos.PresignedURLOptions{
		Query:  &url.Values{},
		Header: &http.Header{},
	}
	opt.Query.Add("x-cos-security-token", "<token>")
	// Get presigned
	presignedURL, err = c.Object.GetPresignedURL(ctx, http.MethodGet, name, tak, tsk, time.Hour, opt)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
		return
	}
	// Get object by presinged url
	resp, err = http.Get(presignedURL.String())
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}
	defer resp.Body.Close()
	fmt.Println(presignedURL.String())
	fmt.Printf("resp:%v\n", resp)
}
```
