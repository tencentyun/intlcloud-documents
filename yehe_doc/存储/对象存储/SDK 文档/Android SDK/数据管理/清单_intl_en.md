

## Overview

This document provides an overview of APIs and SDK code samples related to inventory.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Setting an inventory job | Sets an inventory job in a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries inventory jobs for a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job of a bucket |

## Setting Inventory Job

#### Feature description

This API (PUT Bucket inventory) is used to create an inventory job in a bucket.

#### Method prototype

```
PutBucketInventoryResult putBucketInventory(PutBucketInventoryRequest request)throws CosXmlClientException, CosXmlServiceException;

void putBucketInventoryAsync(PutBucketInventoryRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketInventoryRequest putBucketInventoryRequest = new PutBucketInventoryRequest(bucket);
putBucketInventoryRequest.setInventoryId("inventoryId");
putBucketInventoryRequest.setIncludedObjectVersions(InventoryConfiguration.IncludedObjectVersions.ALL);
putBucketInventoryRequest.setScheduleFrequency(InventoryConfiguration.SCHEDULE_FREQUENCY_DAILY);
putBucketInventoryRequest.setDestination("CSV", "1000000000", "examplebucket-1250000000", "region", "objectPrefix");

// Use the sync method
try {
    PutBucketInventoryResult putBucketInventoryResult = cosXmlService.putBucketInventory(putBucketInventoryRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.putBucketInventoryAsync(putBucketInventoryRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketInventoryResult putBucketInventoryResult = (PutBucketInventoryResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| bucket  | Bucket for which to set an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| InventoryId            | Inventory job settings                                                 | String |
| includedObjectVersions | Whether to include object versions in the inventory.                                     | Enum |
| scheduleFrequency      | Inventory job frequency                                                 | Enum |
| destination              | Describes the information of the inventory result storage                                       | Object |

#### Response description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

#### Error code description

Some frequent special errors that may occur with this request are listed below:

| Error code | Description | Status code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You probably do not have access to the bucket. | HTTP 403 Forbidden |

## Querying Inventory Job

#### Feature description

This API (GET Bucket inventory) is used to query the inventory job information in a bucket.

#### Method prototype

```
GetBucketInventoryResult getBucketInventory(GetBucketInventoryRequest request)throws CosXmlClientException, CosXmlServiceException;

void getBucketInventoryAsync(GetBucketInventoryRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketInventoryRequest getBucketInventoryRequest = new GetBucketInventoryRequest(bucket);
// Set signature verification host. All headers are to be verified by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketInventoryRequest.setSignParamsAndHeaders(null, headerKeys);
getBucketInventoryRequest.setInventoryId("inventoryId");
// Use the sync method
try {
    GetBucketInventoryResult getBucketInventoryResult = cosXmlService.getBucketInventory(getBucketInventoryRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.getBucketInventoryAsync(getBucketInventoryRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketInventoryResult getBucketInventoryResult = (GetBucketInventoryResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| ----------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to query an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| inventoryId | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |

#### Response description

| Member Variable | Description | Type |
| ---------------------- | -------------------------------------------------------- | ---------------------- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
| inventoryConfiguration | Returns bucket object's `InventoryConfiguration` information             | InventoryConfiguration |

## Deleting Inventory Job

#### Feature description

This API (DELETE Bucket inventory) is used to delete a specified inventory job of a bucket.

#### Method prototype

```
DeleteBucketInventoryResult deleteBucketInventory(DeleteBucketInventoryRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketInventoryAsync(DeleteBucketInventoryRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketInventoryRequest deleteBucketInventoryRequest = new DeleteBucketInventoryRequest(bucket);
// Set signature verification host. All headers are to be verified by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteBucketInventoryRequest.setSignParamsAndHeaders(null, headerKeys);
getBucketInventoryRequest.setInventoryId("inventoryId");
// Use the sync method
try {
    DeleteBucketInventoryResult deleteBucketInventoryResult = cosXmlService.deleteBucketInventory(deleteBucketInventoryRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.deleteBucketInventoryAsync(deleteBucketInventoryRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketInventoryResult deleteBucketInventoryResult = (DeleteBucketInventoryResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| ----------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to delete an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| inventoryId | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |

#### Response description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
