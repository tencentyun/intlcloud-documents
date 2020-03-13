## Introduction
Go SDK provides a pre-signed URL for obtaining requests. For detailed operations, please see the following examples.



## Obtaining pre-signed URL used for request 

```go
func (s *ObjectService) GetPresignedURL(ctx context.Context, httpMethod, name, ak, sk string, expired time.Duration, opt interface{}) (*url.URL, error)
```

#### Parameter Description
| Parameter Name | Type | Description |
| ------------------ | ---------------------------- | ------------------------------- |
| httpMethod | string | HTTP request method |
| name | string | HTTP request path, i.e.: the key |
| ak | string | SecretId |
| sk | string | SecretKey |
| expired | time.Duration | Validity period of the sign |
| opt    | interface{} | Can be nil |

## Example of using permanent key to generate pre-signed URL

### Example for uploading requests

[//]: # (.cssg-snippet-get-presign-upload-url)
```go
ak := "COS_SECRETID"
sk := "COS_SECRETKEY"

name := "exampleobject"
ctx := context.Background()
f := strings.NewReader("test")

// 1. Upload the object via standard method
_, err := client.Object.Put(ctx, name, f, nil)
if err != nil {
    panic(err)
}
// Obtaining pre-signed URL
presignedURL, err := client.Object.GetPresignedURL(ctx, http.MethodPut, name, ak, sk, time.Hour, nil)
if err != nil {
    panic(err)
}
// 2. Upload the object via pre-signed method
data := "test upload with presignedURL"
f := strings.NewReader("test")
req, err := http.NewRequest(http.MethodPut, presignedURL.String(), f)
if err != nil {
    panic(err)
}
// User can customize the request header configuration
"headers": {"Content-Type":"text/html"},
_, err = http.DefaultClient.Do(req)
if err != nil {
    panic(err)
}
```

#### Samples for downloading requests

[//]: # (.cssg-snippet-get-presign-download-url)
```go
ak := "COS_SECRETID"
sk := "COS_SECRETKEY"
name := "exampleobject"
ctx := context.Background()
// 1. Download the object via standard method
resp, err := client.Object.Get(ctx, name, nil)
if err != nil {
    panic(err)
}
bs, _ := ioutil.ReadAll(resp.Body)
resp.Body.Close()
// Obtaining pre-signed URL
presignedURL, err := client.Object.GetPresignedURL(ctx, http.MethodGet, name, ak, sk, time.Hour, nil)
if err != nil {
    panic(err)
}
// 2. Download the object via pre-signed URL
resp2, err := http.Get(presignedURL.String())
if err != nil {
    panic(err)
}
bs, _ := ioutil.ReadAll(resp.Body)
resp2.Body.Close()
if bytes.Compare(bs2, bs) != 0 {
    panic(errors.New("content is not consistent"))
}
```
