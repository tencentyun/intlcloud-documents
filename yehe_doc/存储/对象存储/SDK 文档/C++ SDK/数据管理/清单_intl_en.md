## Overview

This document provides an overview of APIs and SDK code samples related to COS inventory.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Creating an inventory configuration | Creates an inventory configuration for a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying an inventory configuration | Queries an inventory configuration of a bucket |
| [LIST Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30627) | Listing inventory configurations | Lists the inventory configurations of a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory configuration | Deletes an inventory configuration of a bucket |

## Creating an Inventory Configuration

#### API description

This API (PUT Bucket inventory) is used to create an inventory configuration for a bucket.

#### Method prototype

```cpp
CosResult BucketOp::PutBucketInventory(const PutBucketInventoryReq& req, PutBucketInventoryResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::PutBucketInventoryReq req(bucket_name);
qcloud_cos::PutBucketInventoryResp resp;

// Create an inventory configuration.
req.SetId("list");

COSBucketDestination destination;
destination.SetFormat("CSV");
destination.SetAccountId("100010974959");

destination.SetBucket("qcs::cos:ap-guangzhou::loggtest-1234567890");
destination.SetPrefix("/");
destination.SetEncryption(true);

OptionalFields fields;
fields.SetIsSize(true);
fields.SetIsLastModified(true);
fields.SetIsStorageClass(true);
fields.SetIsMultipartUploaded(true);
fields.SetIsReplicationStatus(true);
fields.SetIsEtag(true);

Inventory inventory;
inventory.SetIsEnable(true);
inventory.SetIncludedObjectVersions("All");
inventory.SetFilter("/");
inventory.SetId(req.GetId());
inventory.SetFrequency("Daily");
inventory.SetCOSBucketDestination(destination);
inventory.SetOptionalFields(fields);

req.SetInventory(inventory);

qcloud_cos::CosResult result = cos.PutBucketInventory(req, &resp);
if (result.IsSucc()) {
    // Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -----------------------------| ----------------------| ------|
| req  | Request of the `PutBucketInventory` operation | PutBucketInventoryReq | Yes |
| resp | Resonse of the `PutBucketInventory` operation | PutBucketInventoryResp | Yes |


`PutBucketInventoryReq` provides the following member function:

```
// Set an inventory policy.
void SetInventory(Inventory& inventory);
```

Classes in the request are defined as follows:

```

// Inventory configuration parameters
class Inventory {
    void SetId(const std::string& id) // Set the ID of the inventory.
    void SetIsEnable(bool is_enabled) // Specify whether to enable the inventory.    
    void SetIncludedObjectVersions(const std::string& included_objectversions) // Specify whether to include object versions in the inventory.
    void SetFilter(const std::string& filter) // Specifies an inventory filter to include certain objects (prefixes).    
    void SetCOSBucketDestination(const COSBucketDestination& destination) // Set the information about the bucket that stores the published inventory results.
    void SetOptionalFields(const OptionalFields& fields) // Specify the fields to include in the inventory results.
    void SetFrequency(const std::string& frequency) // Specifies how frequently (either `Daily` or `Weekly`) the inventory results are produced.
}

// Fields to include in the inventory results
class OptionalFields {
    void SetIsSize(const bool size); // Specify whether to include the object size field.
    void SetIsLastModified(const bool last_modified) // Specify whether to include the last modified time field.
    void SetIsStorageClass(const bool storage_class) // Specify whether to include the storage class field.
    void SetIsMultipartUploaded(const bool ismultipart_uploaded) // Specify whether to include the multipart upload field.    
    void SetIsReplicationStatus(const bool replication_status) // Specify whether to include the cross-bucket replication status field.
}

// Information about where to publish the inventory results
class COSBucketDestination {
public:
    void SetFormat(const std::string& format) // Specify the format of the inventory. Currently, CSV is supported.    
    void SetAccountId(const std::string& accountId) // Specify the ID of the bucket owner.  
    void SetBucket(const std::string& bucket) // Specify the full ID of the bucket.
    void SetPrefix(const std::string& prefix) // Specify the name of the bucket that stores the inventory results.    
    void SetEncryption(const bool encryption) // Specify whether to encrypt the inventory results.    
```


#### Error codes

The following describes some common errors that may occur when you make requests using this API.

| Error Code | Description | Status Code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid argument | HTTP 400 Bad Request |
| TooManyConfigurations | The number of created inventory configurations exceeding the upper threshold (1,000) | HTTP 400 Bad Request |
| AccessDenied | Unauthorized access. You may not have permission to access the bucket | HTTP 403 Forbidden |


## Querying an Inventory Configuration

#### API description

This API (GET Bucket inventory) is used to query an inventory configuration of a bucket.

#### Method prototype

```cpp
CosResult CosAPI::GetBucketInventory(const GetBucketInventoryReq& request, GetBucketInventoryResp* response) {                                      
```

#### Sample request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::GetBucketInventoryReq req(bucket_name);
qcloud_cos::GetBucketInventoryResp resp;

// Set the inventory configuration.
req.SetId("list");

qcloud_cos::CosResult result = cos.GetBucketInventoryResp(req, &resp);
if (result.IsSucc()) {
    // Request successful. You can obtain the inventory information.
    //const Inventory inventory = resp.GetInventory();
    //std::cout << "inventory isenabled:" << inventory.GetIsEnable() << std::endl;
    //std::cout << "inventory IncludedObjectVersions:" << inventory.GetIncludedObjectVersions() << std::endl;
    //std::cout << "inventory filter:" << inventory.GetFilter() << std::endl;
    //std::cout << "inventory id:" << inventory.GetId() << std::endl;
    //std::cout << "inventory Frequency:" << inventory.GetFrequency() << std::endl;

    //std:: cout << "===================================" << std::endl;
    //COSBucketDestination destination = inventory.GetCOSBucketDestination();
    //std::cout << "destination Format:" << destination.GetFormat() << std::endl;
    //std::cout << "destination AccountID:" << destination.GetAccountId() << std::endl;
    //std::cout << "destination Bucket:" << destination.GetBucket() << std::endl;
    //std::cout << "destination Encryption:" << destination.GetEncryption() << std::endl;

    //std:: cout << "===================================" << std::endl;
    //    
    //OptionalFields fields = inventory.GetOptionalFields();

    //std::cout << "fields Size:" << fields.GetIsSize() << std::endl;
    //std::cout << "fields LastModified:" << fields.GetIsLastModified() << std::endl;
    //std::cout << "fields StorageClass:" << fields.GetIsStorageClass() << std::endl;
    //std::cout << "fields Region:" << fields.GetIsMultipartUploaded() << std::endl;
    //std::cout << "fields ReplicationStatus:" << fields.GetIsReplicationStatus() << std::endl;
    //std::cout << "fields Tag:" <<     fields.GetIsETag() << std::endl;
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -----------------------------| ----------------------| ------|
| req | Request of the `GetBucketInventory` operation | GetBucketInventoryReq | Yes |
| resp | Response of the `GetBucketInventory` operation | GetBucketInventoryResp | Yes |


`GetBucketInventoryResp` provides the following member function:

```
// Obtain the inventory policy.
const Inventory& GetInventory() const;
```

## Querying the List of Inventory Configurations

#### API description

This API (List Bucket Inventory Configurations) is used to obtain the list of inventory configurations for a bucket.

#### Method prototype

```cpp
CosResult CosAPI::ListBucketInventoryConfigurations(const ListBucketInventoryConfigurationsReq& request, ListBucketInventoryConfigurationsResp* response) {                                      
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::ListBucketInventoryConfigurationsReq req(bucket_name);
qcloud_cos::ListBucketInventoryConfigurationsResp resp;

qcloud_cos::CosResult result = cos.ListBucketInventoryConfigurations(req, &resp);
if (result.IsSucc()) {
    // Request successful. You can obtain the inventory configurations.
   // std::cout << "===================ListBucketInventoryConfigurations=====================" << std::endl;
   //     
   // std::vector<Inventory> inventory_vec = resp.GetInventory();
   //     
   // std::cout << resp.GetIsTruncated() << std::endl;
   // std::cout << resp.GetContinuationToken() << std::endl;
   // std::cout << resp.GetNextContinuationToken() << std::endl;
   //     
   // std::vector<Inventory>::iterator itr = inventory_vec.begin();
   // for(; itr != inventory_vec.end(); ++itr) {
   //         
   //    std:: cout << "==============Inventory=============================" << std::endl;
   //    std::cout << "inventory id:" << itr->GetId() << std::endl;
   //    std::cout << "inventory isenabled:" <<  itr->GetIsEnable() << std::endl;
   //    std::cout << "inventory IncludedObjectVersions:" << itr->GetIncludedObjectVersions() << std::endl;
   //    std::cout << "inventory filter:" << itr->GetFilter() << std::endl;
   //    std::cout << "inventory Frequency:" <<     itr->GetFrequency() << std::endl;
   //    std:: cout << "==============GetCOSBucketDestination==================" << std::endl;
   //    COSBucketDestination destination = itr->GetCOSBucketDestination();
   //    std::cout << "destination Format:" << destination.GetFormat() << std::endl;
   //    std::cout << "destination AccountID:" << destination.GetAccountId() << std::endl;
   //    std::cout << "destination Bucket:" << destination.GetBucket() << std::endl;
   //    std::cout << "destination Encryption:" << destination.GetEncryption() << std::endl;
   //          
   //    std:: cout << "===================OptionalFields======================" << std::endl;
   //    OptionalFields fields = itr->GetOptionalFields();
   //    std::cout << "fields Size:" << fields.GetIsSize() << std::endl;
   //    std::cout << "fields LastModified:" << fields.GetIsLastModified() << std::endl;
   //    std::cout << "fields StorageClass:" << fields.GetIsStorageClass() << std::endl;
   //    std::cout << "fields Region:" << fields.GetIsMultipartUploaded() << std::endl;
   //    std::cout << "fields ReplicationStatus:" << fields.GetIsReplicationStatus() << std::endl;
   //    std::cout << "fields Tag:" <<     fields.GetIsETag() << std::endl;
   // }    
   // std::cout << "===============ListBucketInventoryConfigurations end================" << std::endl;
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
}

```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | --------------------------------------------| -------------------------------------| ------|
| req  | Request of the `ListBucketInventoryConfigurations` operation | ListBucketInventoryConfigurationsReq | Yes |
| resp | Response of the `ListBucketInventoryConfigurations` operation | ListBucketInventoryConfigurationsResp| Yes |


`ListBucketInventoryConfigurationsReq` provides the following member function:

```
// In the COS response, if the value of `IsTruncated` is `true` and the `NextContinuationToken` node carries a value, you can pass the value of this parameter as the argument of `continuation-token` so that you can obtain the remaining inventory configurations.
void SetContinuationToken(const std::string continuation_token); 
```


## Deleting an Inventory Configuration

#### API description

This API (DELETE Bucket inventory) is used to delete an inventory configuration of a bucket.

#### Method prototype

```cpp
CosResult CosAPI::DeleteBucketInventory(const DeleteBucketInventoryReq& request, DeleteBucketInventoryResp* response);                          
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::DeleteBucketInventoryReq req(bucket_name);
qcloud_cos::DeleteBucketInventoryResp resp;

qcloud_cos::CosResult result = cos.DeleteBucketInventory(req, &resp);
if (result.IsSucc()) {
    // Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -------------------------------| ------------------------| ------|
| req  | Request of the `DeletBucketInventory` operation | DeletBucketInventoryReq | Yes |
| resp | Response of the `DeletBucketInventory` operation | DeletBucketInventoryResp | Yes |


`DeleteBucketInventoryReq` provides the following member function:

```
void SetId(const std::string id)  // Set the ID of the inventory to delete.
```
