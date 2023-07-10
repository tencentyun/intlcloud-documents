## Overview

This document provides an overview of APIs and SDK code samples for vehicle recognition.

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
| Vehicle and license plate detection | Recognizes vehicles in images. |


## Vehicle and License Plate Detection

#### Feature description

This feature uses a sync GET request to detect a vehicle in an image and recognize its brand, color, location, and license plate information.

#### Method prototype

```java
DetectCarResponse detectCar(DetectCarRequest request);
```

#### Sample request

```java
//1. Create a job request object
DetectCarRequest request = new DetectCarRequest();
//2. Add request parameters as detailed in the API documentation
//2.1 Set the request bucket
request.setBucketName("demobucket-1234567890");
//2.2 Set the image location in the bucket
request.setObjectKey("car.jpg");
DetectCarResponse response = client.detectCar(request);
```


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| bucketName | Request | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| objectKey | Request | Location of the image in the bucket | String    | Yes   |

#### Response description

- Success: The `DetectCarResponse` job result object is returned upon success.
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
