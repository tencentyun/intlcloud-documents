## Overview
The Go SDK provides pre-signed request URLs. For detailed operations, please see the following examples.

>?
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 

## Getting a Pre-signed Request URL 

```go
func (s *ObjectService) GetPresignedURL(ctx context.Context, httpMethod, name, ak, sk string, expired time.Duration, opt interface{}) (*url.URL, error)
```

#### Parameter description
| Parameter | Type | Description |
| ------------------ | ---------------------------- | ------------------------------- |
| httpMethod | string | HTTP request method |
| name | string | HTTP request path, i.e.: the key |
| ak             | string                       | SecretId                    |
| sk               | string                       | SecretKey         |
| expired | time.Duration | Validity period of the signature |
| opt    | interface{} | Can be nil |

## Generating Pre-signed URL with Permanent Key

### Upload request sample

[//]: # (.cssg-snippet-get-presign-upload-url)
```go
ak := "SECRETID"
sk := "SECRETKEY"

name := "exampleobject"
ctx := context.Background()
f := strings.NewReader("test")

// 1. Upload the object using the standard method.
_, err := client.Object.Put(ctx, name, f, nil)
if err != nil {
    panic(err)
}
// Obtain the pre-signed URL.
presignedURL, err := client.Object.GetPresignedURL(ctx, http.MethodPut, name, ak, sk, time.Hour, nil)
if err != nil {
    panic(err)
}
// 2. Upload the object using a pre-signed URL.
data := "test upload with presignedURL"
f = strings.NewReader(data)
req, err := http.NewRequest(http.MethodPut, presignedURL.String(), f)
if err != nil {
    panic(err)
}
// You can configure request headers by yourself.
req.Header.Set("Content-Type", "text/html")
_, err = http.DefaultClient.Do(req)
if err != nil {
    panic(err)
}
```

#### Samples for download requests

[//]: # (.cssg-snippet-get-presign-download-url)
```go
ak := "SECRETID"
sk := "SECRETKEY"
name := "exampleobject"
ctx := context.Background()
// 1. Download the object using the standard method.
resp, err := client.Object.Get(ctx, name, nil)
if err != nil {
    panic(err)
}
bs, _ := ioutil.ReadAll(resp.Body)
resp.Body.Close()
// Obtain the pre-signed URL.
presignedURL, err := client.Object.GetPresignedURL(ctx, http.MethodGet, name, ak, sk, time.Hour, nil)
if err != nil {
    panic(err)
}
// 2. Download the object using a pre-signed URL.
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

## Generating Pre-signed URL with Temporary Key

```go
// You can use tags to put the request parameters or request headers in the signature.
type URLToken struct {
	SessionToken string `url:"x-cos-security-token,omitempty" header:"-"`
}

func main() {
	// Replace it with your temporary key.
	tak := os.Getenv("SECRETID")
	tsk := os.Getenv("SECRETKEY")
	token := &URLToken{
		SessionToken: "<token>",
	}
	u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{})

	name := "exampleobject"
	ctx := context.Background()

	// Method 1. Use tags to configure “x-cos-security-token”.
	// Get presigned
	presignedURL, err := c.Object.GetPresignedURL(ctx, http.MethodGet, name, tak, tsk, time.Hour, token)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
		return
	}
	// Get object by pre-signed URL
	resp, err := http.Get(presignedURL.String())
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}
	defer resp.Body.Close()
	fmt.Println(presignedURL.String())
	fmt.Printf("resp:%v\n", resp)

	// Method 2. Use “PresignedURLOptions” to configure “x-cos-security-token”.
    // You can add request parameters and request headers through “PresignedURLOptions”.
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
	// Get object by pre-signed URL
	resp, err = http.Get(presignedURL.String())
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}
	defer resp.Body.Close()
	fmt.Println(presignedURL.String())
	fmt.Printf("resp:%v\n", resp)
}
```
