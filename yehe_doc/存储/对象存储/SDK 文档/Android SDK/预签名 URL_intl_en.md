## Introduction
Android SDK provides the API for getting an object URL and the pre-signed URL for a request. 

## Obtaining Object URL
```java
string getAccessUrl(CosXmlRequest cosXmlRequest);
```

## Obtaining Pre-signed URL Used for Request 

```java
String getPresignedURL(CosXmlRequest cosXmlRequest) throws CosXmlClientException;
```

#### Parameter Description

| Parameter Name | Type | Description |
|-----|-----|----|
|cosXmlRequest|CosXmlRequest| Request object|
|presignedUrlRequest |PresignedUrlRequest |Pre-signed URL instance|
|checkParameterListForSing |`Set<String>`|Request headers in the signature for verification |
|checkHeaderListForSign  |`Set<String>`|Request parameters in the signature for verification|

#### PresignedUrlRequest structure description

Get the corresponding pre-signed request URL through the PresignedUrlRequest object to send requests.

| Parameter Name | Type | Description |
|-----|-----|----|
|bucket|string| Bucket name of the COS XML API in the format `<BucketName-APPID>`<br>For example, examplebucket-1250000000 |
|requestMethod|string|HTTP request method, such as `GET` (Download)|
|cosPath |string|Object key, i.e. the location identifier of the object in the bucket|
|checkParameterListForSing |`Set<String>`|Request headers in the signature for verification |
|checkHeaderListForSign  |`Set<String>`|Request parameters in the signature for verification|

## Pre-signed request examples

### Example for uploading requests

[//]: # (.cssg-snippet-get-presign-upload-url)
```java
try {

    String bucket = "examplebucket-1250000000"; //Bucket name
    String cosPath = "exampleobject"; //The location identifier of the object in the bucket. For example, cosPath = "text.txt";
    String method = "PUT"; // HTTP Request Method
    PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket, cosPath) {
        @Override
        public RequestBodySerializer getRequestBody() throws CosXmlClientException {
            // Used to calculate pre-signed URLs requests like `PUT` that requires a request body
            return RequestBodySerializer.string("text/plain", "this is test");
        }
    };
    presignedUrlRequest.setRequestMethod(method);

    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest); // Upload pre-signed URL (Calculates the signed URL with the permanent key method)) 

    //String urlWithSign = cosXmlService.getPresignedURL(putObjectRequest)； //Directly uses PutObjectRequest

    String srcPath = new File(context.getExternalCacheDir(), "exampleobject").toString();
    PutObjectRequest putObjectRequest = new PutObjectRequest("examplebucket-1250000000", "exampleobject", srcPath);
    // Set the pre-signed URL for upload request
    putObjectRequest.setRequestURL(urlWithSign);
    // Set progress callback
    putObjectRequest.setProgressListener(new CosXmlProgressListener() {
        @Override
        public void onProgress(long progress, long max) {
            // todo Do something to update progress...
        }
    });
    // Upload using sync method
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
```

#### Samples for Download Requests

[//]: # (.cssg-snippet-get-presign-download-url)
```java
try {
    String bucket = "examplebucket-1250000000"; //Bucket name
    String cosPath = "exampleobject"; //The location identifier of the object in the bucket. For example, cosPath = "text.txt";
    String method = "GET"; // HTTP Request Method
    PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket, cosPath);
    presignedUrlRequest.setRequestMethod(method);

    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest); // Upload pre-signed URL (Calculates the signed URL with the permanent key method)) 

    //String urlWithSign = cosXmlService.getPresignedURL(getObjectRequest)； // Directly uses GetObjectRequest

    String savePath = context.getExternalCacheDir().toString(); // Local path
    String saveFileName = "exampleobject"; // Local filename
    GetObjectRequest getObjectRequest = new GetObjectRequest("examplebucket-1250000000", "exampleobject", savePath, saveFileName);

    // Set the pre-signed URL for upload request
    getObjectRequest.setRequestURL(urlWithSign);
    // Set progress callback
    getObjectRequest.setProgressListener(new CosXmlProgressListener() {
        @Override
        public void onProgress(long progress, long max) {
            // todo Do something to update progress...
        }
    });
    // Download using sync method
    GetObjectResult getObjectResult = cosXmlService.getObject(getObjectRequest);

} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
```
