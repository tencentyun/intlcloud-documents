

## Overview

This document provides an overview of APIs and SDK code samples for persistent image processing.

| API | Description |
| :----------------------------------------------------------- | :----------------------------------- |
| [Persistent image processing](https://intl.cloud.tencent.com/document/product/436/40592) | Processes images persistently. |


### Processing during upload

#### Feature description

CI allows you to process images during upload and save the input images and processing results to COS. Currently, images within 20 MB can be processed.

#### Method prototype

```cpp
CosResult PutImage(const PutImageByFileReq& request, PutImageByFileResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

PutImageByFileReq req(bucket_name, object_name, local_file);
PutImageByFileResp resp;

PicOperation pic_operation;

PicRules rule;
// Path of the processing result file. If the path starts with `/`, the result file will be stored in the specified folder; otherwise, it will be stored in the same directory as the input image file.
rule.fileid = "/" + object_name + "_sharpen";
// Sharpening parameter
rule.rule = "imageMogr2/sharpen/70";
pic_operation.AddRule(rule);

rule.fileid = "/" + object_name + "_rotate";
// Rotation parameter
rule.rule = "imageMogr2/rotate/90";
pic_operation.AddRule(rule);
 
CosResult result = cos.PutImage(req, &resp);
if (result.IsSucc()) {
   // The call is successful. You can call the `resp` member functions to get the return content.
   std::cout << "ProcessResult: " << resp.GetUploadResult().to_string() << std::endl;
} else {
   // The call failed. You can call the `result` member functions to get the error information.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ------------------ | -------- |
| req  | `PutImage` operation request. | PutImageByFileReq  | Yes       |
| resp | `PutImage` operation response. | PutImageByFileResp | Yes       |

`req` involves the following structures:

```cpp
struct PicRules {
  std::string bucket;  // Name of the destination bucket to store the results in the format of `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket by default.
  std::string fileid;  // Path of the processing result file. If the path starts with `/`, the result file will be stored in the specified folder; otherwise, it will be stored in the same directory as the input image file.
  std::string rule;  // Processing parameters. For more information, see the COS image processing API. To process an image with a specified style, the value must start with `style/` with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`.
};

class PicOperation {
 public:
  PicOperation() : is_pic_info(true) {}
  virtual ~PicOperation() {}
  void AddRule(const PicRules& rule) { rules.push_back(rule); }
  void TurnOffPicInfo() { is_pic_info = false; }
 private:
  boolis_pic_info;  // Whether to return the input image information. Valid values: 0 (no), 1 (yes). Default value: 0.
  std::vector<PicRules> rules;  // Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed.
};
```

`resp` involves the following structures:

```cpp
struct CodeLocation {
  std::vector<std::string> points;  // QR code coordinates
};

struct QRcodeInfo {
  std::string code_url;        // QR code content. Content may not be recognized.
  CodeLocation code_location;  // Location coordinates of the QR code recognized in the image

};

struct Object {
  std::string key;       // Filename
  std::string location;  // Image path
  std::string format;    // Image format
  int width;             // Image width
  int height;            // Image height
  int size;              // Image size
  int quality;           // Image quality
  std::string etag;      // `ETag` of the processing result image
  int code_status;  // Whether QR codes are recognized. 0: no; 1: yes.
  int watermark_status;  // When `type`
                         // is 2, this field will be returned to indicate the confidence of the extracted blind watermark.
                         //  Value range: 0–100. If the value is above 75, there is a confirmed blind watermark. If the value is between 60 and 75, there is a suspected blind watermark. If the value is below 60, no blind watermark is extracted.
  std::vector<QRcodeInfo> qr_code_info;  // Recognized QR code. There may be multiple ones.
};

struct ProcessResults {
  std::vector<Object> objects;  // There may be multiple objects
};

struct ImageInfo {
  std::string format;  // Format
  int width;           // Image width
  int height;          // Image height
  int quality;         // Image quality
  std::string ave;     // Image average hue
  int orientation;     // Image rotation angle
};

struct UploadResult {
  OriginalInfo original_info;  // Input image information
  ProcessResults process_result;  // Image processing result
};
```



### Processing in-cloud image

#### Feature description

This feature can process an image stored in COS and save the processing result to COS.

#### Method prototype

```cpp
CosResult CloudImageProcess(const CloudImageProcessReq& request, CloudImageProcessResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

CloudImageProcessReq req(bucket_name, object_name);
CloudImageProcessResp resp;

PicOperation pic_operation;
PicRules rule;
// Path of the processing result file. If the path starts with `/`, the result file will be stored in the specified folder; otherwise, it will be stored in the same directory as the input image file.
rule.fileid = "/" + object_name + "_thumbnail";
// Scaling parameter
rule.rule = "imageMogr2/thumbnail/!30p";
pic_operation.AddRule(rule);

rule.fileid = "/" + object_name + "_cut";
// Cropping parameter
rule.rule = "imageMogr2/cut/300x300";
pic_operation.AddRule(rule);
req.SetPicOperation(pic_operation);

CosResult result = cos.CloudImageProcess(req, &resp);
if (result.IsSucc()) {
   // The call is successful. You can call the `resp` member functions to get the return content.
} else {
   // The call failed. You can call the `result` member functions to get the error information.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ------------------ | -------- |
| req  | `PutImage` operation request. | PutImageByFileReq  | Yes       |
| resp | `PutImage` operation response. | PutImageByFileResp | Yes       |

