

The following example shows how to automatically process an image when you upload it.

Upon the successful upload, COS will save both the original and processed images, and you can obtain the processing result by a common download request.

[//]: #".cssg-snippet-put-image-and-process"

```go
u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
c := cos.NewClient(b, &http.Client{
	Transport: &cos.AuthorizationTransport{
		SecretID:  os.Getenv("COS_SECRETID"),
		SecretKey: os.Getenv("COS_SECRETKEY"),
		Transport: &debug.DebugRequestTransport{// is used to Debug
			RequestHeader: true,
			RequestBody:    false,
			ResponseHeader: true,
			ResponseBody:   true,
		},
	},
})

opt := &cos.ObjectPutOptions{
	nil,
	&cos.ObjectPutHeaderOptions{
		XOptionHeader: &http.Header{},
	},
}
pic := &cos.PicOperations{
	IsPicInfo: 1,
	Rules: []cos.PicOperationsRules{
		{
             // Name of the destination bucket to store the result. Format: BucketName-APPID. If not specified, the result is saved to the current bucket by default.
            Bucket: "examplebucket-1250000000",
             // File key of the processing result. If it starts with “/”, the result is stored in the specified folder. Otherwise, it is stored in the same directory as the original image file.
			FileId: "example.png",
             // Processing parameters. For the rules, see https://cloud.tencent.com/document/product/460/6924.
             // Use this parameter to convert jpeg to png.
			Rule: "imageView2/format/png",
		},
	},
}
// Convert the processing rules into json strings and set image processing headers.
opt.XOptionHeader.Add("Pic-Operations", cos.EncodePicOperations(pic))
name := "example.jpg"
local_filename := "./example.jpg"
_, err := c.Object.PutFromFile(context.Background(), name, local_filename, opt)
```
