## Overview

This document provides an overview of APIs and SDK code samples for search by image.

| API | Description |
| ------------- |  ---------------------- |
| [Enabling search by image](https://intl.cloud.tencent.com/document/product/1045/43516) |  Enables the search by image feature for a bucket |
| [Adding an image to the image library](https://intl.cloud.tencent.com/document/product/1045/43517) |  Adds an image to the image library |
| [Searching for an image](https://intl.cloud.tencent.com/document/product/1045/43518) |  Searches for an image in the image library |
| [Removing an image from the image library](https://intl.cloud.tencent.com/document/product/1045/43519) |  Removes an image from the image library |

## Enabling Search by Image

#### Feature description

This API is used to enable the search by image feature for a bucket.

#### Method prototype

```java
boolean openImageSearch(OpenImageSearchRequest imageSearchRequest);
```


#### Sample request

```java
//1. Create a job request object
OpenImageSearchRequest request = new OpenImageSearchRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demobucket-123456789");
request.setMaxCapacity("100");
request.setMaxQps("10");
//3. Call the API to get the job response object
boolean response = client.openImageSearch(request);
```


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| bucketName | Request | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| maxCapacity | Request | Maximum capacity of the image library	 | String    | Yes   |
| MaxQps | Request | Maximum QPS of the image library	 | String    | No   |

#### Response description

- Success: `true` is returned upon success. 
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Adding Image to Image Library

#### Feature description

This API is used to add an image to the image library.

#### Method prototype

```java
boolean addGalleryImages(ImageSearchRequest imageSearchRequest);
```


#### Sample request

```java
//1. Create a job request object
ImageSearchRequest request = new ImageSearchRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demobucket-123456789");
request.setObjectKey("1.png");
request.setEntityId("mark1");
//3. Call the API to get the job response object
boolean response = client.addGalleryImages(request);
```


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| bucketName | Request | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| objectKey | Request | Location of the image in the bucket	 | String    | Yes   |
| entityId | Request | Entity ID, which can contain up to 64 characters. If `EntityId` already exists, this request will add the image to it. | String | Yes |
| customContent | Request | Custom content, which can contain up to 4,096 characters. The content set will be returned when the image is queried.	  | String | No  |
| tags | Request | Custom image tags. The value is a JSON string containing up to 10 key:value pairs.	 | String | No   |

#### Response description

- Success: `true` is returned upon success. 
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Searching for Image

#### Feature description

This API is used to search for an image in the image library.

#### Method prototype

```java
ImageSearchResponse searchGalleryImages(ImageSearchRequest imageSearchRequest);
```

#### Sample request

```java
//1. Create a job request object
ImageSearchRequest request = new ImageSearchRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demobucket-123456789");
request.setObjectKey("1.png");
//3. Call the API to get the job response object
ImageSearchResponse response = client.searchGalleryImages(request);
```


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| bucketName | Request | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| objectKey | Request | Location of the image in the bucket	 | String    | Yes   |
| matchThreshold | Request | Only images scoring higher than the value of `MatchThreshold` will be returned. Default value: `0`.		  | String    | No |
| Offset | Request | Starting number. Default value: `0`.		 | String    | No   |
| limit| Request | Number of results to be returned. Default value: `10`. Maximum value: `100`.		 | String    | No   |
| filter | Request | Uses image tags to filter images. You can use AND and OR to set multiple conditions (>, >=, <, <=, =, !=).		 | String | No |

#### Response description

- Success: The `ImageSearchResponse` response object is returned upon success.
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Removing Image from Image Library

#### Feature description

This API is used to remove an image from the image library.

#### Method prototype

```java
boolean deleteGalleryImages(ImageSearchRequest imageSearchRequest);
```


#### Sample request

```java
//1. Create a job request object
ImageSearchRequest request = new ImageSearchRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demobucket-123456789");
request.setObjectKey("1.png");
request.setEntityId("mark");
//3. Call the API to get the job response object
boolean response = client.deleteGalleryImages(request);
```


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| bucketName | Request | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| objectKey | Request | Location of the image in the bucket | String    | Yes   |
| entityId | Request | Entity ID | String    | Yes   |

#### Response description

- Success: `true` is returned upon success.
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

