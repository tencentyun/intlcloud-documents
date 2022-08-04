## Overview

This document provides an overview of APIs and SDK code samples for blind watermarking.

## SDK API References

For the parameters and method description of all the APIs in the SDK, see the [API documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Adding Blind Watermark

### Feature description

You can add a blind watermark when uploading or downloading an object.

### Sample 1: Adding a blind watermark during upload

[//]: #	".cssg-snippet-put-object-with-watermark"

```cs
PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);

JObject o = new JObject();
// Do not return the input image
o["is_pic_info"] = 0;
JArray rules = new JArray();
JObject rule = new JObject();
rule["bucket"] = bucket;
rule["fileid"] = key;
// Processing parameters. For rules, visit https://cloud.tencent.com/document/product/436/46782.
rule["rule"] = "watermark/3/type/<type>/image/<imageUrl>/text/<text>/level/<level>";
rules.Add(rule);
o["rules"] = rules;

string ruleString = o.ToString(Formatting.None);
request.SetRequestHeader("Pic-Operations", ruleString);
// Execute the request
PutObjectResult result = cosXml.PutObject(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs).
>

### Sample 2: Adding a blind watermark during download

[//]: #	".cssg-snippet-download-object-with-watermark"

```cs
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, key, localDir, localFileName);
// Processing parameters. For rules, visit https://cloud.tencent.com/document/product/436/46782.
getObjectRequest.SetQueryParameter("watermark/3/type/<type>/image/<imageUrl>/text/<text>", null);

GetObjectResult result = cosXml.GetObject(getObjectRequest);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs).
>
