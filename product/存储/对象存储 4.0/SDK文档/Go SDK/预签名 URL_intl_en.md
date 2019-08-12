## Overview
The SDK for Go provides an API to get pre-signed request URLs. For more information, see the examples in this document.



## Getting a Pre-signed Request URL 

```go
func (s *ObjectService) GetPresignedURL(ctx context.Context, httpMethod, name, ak, sk string, expired time.Duration, opt interface{}) (*url.URL, error)
```

### Parameter Descriptions
| Parameter Name | Type | Description |
| ------------------ | ---------------------------- | ------------------------------- |
| httpMethod            | string                   | HTTP request method                        |
| name | string | HTTP request path, i.e., the object key |
| ak             | string                       | SecretId                    |
| sk               | string                       | SecretKey         |
| expired            | time.Duration | Signature's validity period |
| opt | interface{} | Extension. nil can be entered here |

## Example of Pre-signing a Request Using a Permanent Key

### Sample Request for Upload

```go
name := "test/objectPut.go"
ctx := context.Background()
// NewReader create file content
f := strings.NewReader("test")

// 1.Normal add auth header way to put object
_, err := c.Object.Put(ctx, name, f, nil)
if err != nil {
	panic(err)
}
// Get presigned
presignedURL, err := c.Object.PresignedURL(ctx, http.MethodPut, name, ak, sk, time.Hour, nil)
if err != nil {
	panic(err)
}
// 2.Put object content by presinged url
data := "test upload with presignedURL"
f = strings.NewReader(data)
req, err := http.NewRequest(http.MethodPut, presignedURL.String(), f)
if err != nil {
	panic(err)
}
// Can set request header.
req.Header.Set("Content-Type", "text/html")
_, err = http.DefaultClient.Do(req)
if err != nil {
	panic(err)
}
```

### Sample Download Request

```go
name := "test"
ctx := context.Background()
// 1.Normal add auth header way to get object
resp, err := c.Object.Get(ctx, name, nil)
if err != nil {
	panic(err)
} 
bs, _ := ioutil.ReadAll(resp.Body)
resp.Body.Close()
// Get presigned
presignedURL, err := c.Object.GetPresignedURL(ctx, http.MethodGet, name, ak, sk, time.Hour, nil)
if err != nil {
	panic(err)
} 
// 2.Get object content by presinged url
resp2, err := http.Get(presignedURL.String())
if err != nil {
	panic(err)
}                    
bs2, _ := ioutil.ReadAll(resp2.Body)
resp2.Body.Close()
fmt.Printf("result2 is : %s\n", string(bs2))
fmt.Printf("%v\n\n", bytes.Compare(bs2, bs) == 0)
```
