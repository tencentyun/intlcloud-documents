## Overview

This document provides an overview of APIs related to cross-origin access, lifecycle, versioning, and cross-region replication and corresponding SDK sample code.

**Cross-origin access**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning feature of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rule of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rule of a bucket |

## Cross-origin Access

### Setting Cross-origin Access Configuration

#### Feature Description

This API (PUT Bucket cors) is used to set the cross-origin access configuration information of the specified bucket.

#### Method Prototype

```java
public void setBucketCrossOriginConfiguration(String bucketName, BucketCrossOriginConfiguration bucketCrossOriginConfiguration);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| bucketCrossOriginConfiguration | The cross-origin access policy set for the bucket | BucketCrossOriginConfiguration |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
BucketCrossOriginConfiguration bucketCORS = new BucketCrossOriginConfiguration();
List<CORSRule> corsRules = new ArrayList<>();
CORSRule corsRule = new CORSRule();
// Rule name
corsRule.setId("set-bucket-cors-test");  
// Allowed HTTP method
corsRule.setAllowedMethods(AllowedMethods.PUT, AllowedMethods.GET, AllowedMethods.HEAD);
corsRule.setAllowedHeaders("x-cos-grant-full-control");
corsRule.setAllowedOrigins("http://mail.qq.com",         "http://www.qq.com", "http://video.qq.com");
corsRule.setExposedHeaders("x-cos-request-id");
corsRule.setMaxAgeSeconds(60);
corsRules.add(corsRule);
bucketCORS.setRules(corsRules);
cosClient.setBucketCrossOriginConfiguration(bucketName, bucketCORS);
```

### Querying Cross-origin Access Configuration

#### Feature Description

This API (GET Bucket cors) is used to query the cross-origin access configuration information of the specified bucket.

#### Method Prototype

```java
public BucketCrossOriginConfiguration getBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |

#### Return Result Descriptions

- Success: The cross-origin access rule of the bucket is returned.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
BucketCrossOriginConfiguration corsGet = cosClient.getBucketCrossOriginConfiguration(bucketName);
List<CORSRule> corsRules = corsGet.getRules();
for (CORSRule rule : corsRules) {
List<AllowedMethods> allowedMethods = rule.getAllowedMethods();
List<String> allowedHeaders = rule.getAllowedHeaders();
List<String> allowedOrigins = rule.getAllowedOrigins();
List<String> exposedHeaders = rule.getExposedHeaders();
int maxAgeSeconds = rule.getMaxAgeSeconds();
}
```

### Deleting Cross-origin Access Configuration

#### Feature Description

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of the specified bucket.

#### Method Prototype

```java
public void deleteBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucketCrossOriginConfiguration(bucketName);
```

## Lifecycle

### Setting Lifecycle

#### Feature Description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration information of the specified bucket.

#### Method Prototype

```java
public void setBucketLifecycleConfiguration(String bucketName, BucketLifecycleConfiguration bucketLifecycleConfiguration) 
        throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------------------------- | ------------------------------------------------------------ | ---------------------------- |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| bucketLifecycleConfiguration | Lifecycle configuration | BucketLifecycleConfiguration |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
List<Rule> rules = new ArrayList<>();
// Rule 1. Delete files starting with hongkong_movie/ in path in 30 days
Rule deletePrefixRule = new Rule();
deletePrefixRule.setId("delete prefix xxxy after 30 days");
deletePrefixRule
.setFilter(new LifecycleFilter(newLifecyclePrefixPredicate("hongkong_movie/")));
// Files will be deleted 30 days after they are uploaded or modified
deletePrefixRule.setExpirationInDays(30);
// Set the rule to effective
deletePrefixRule.setStatus(BucketLifecycleConfiguration.ENABLED);

// Rule 2. Files will be transitioned to Standard_IA storage class in 20 days and deleted in one year
Rule standardIaRule = new Rule();
standardIaRule.setId("standard_ia transition");
standardIaRule.setFilter(new LifecycleFilter(new LifecyclePrefixPredicate("standard_ia/")));
List<Transition> standardIaTransitions = new ArrayList<>();
Transition standardTransition = new Transition();
standardTransition.setDays(20);
standardTransition.setStorageClass(StorageClass.Standard_IA.toString());
standardIaTransitions.add(standardTransition);
standardIaRule.setTransitions(standardIaTransitions);
standardIaRule.setStatus(BucketLifecycleConfiguration.ENABLED);
standardIaRule.setExpirationInDays(365);
		
// Add the two rules to the policy collection
rules.add(deletePrefixRule);
rules.add(standardIaRule);

// Generate bucketLifecycleConfiguration
BucketLifecycleConfiguration bucketLifecycleConfiguration =
new BucketLifecycleConfiguration();
bucketLifecycleConfiguration.setRules(rules);

// Bucket name is in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
SetBucketLifecycleConfigurationRequest setBucketLifecycleConfigurationRequest =
new SetBucketLifecycleConfigurationRequest(bucketName, bucketLifecycleConfiguration);

// Set the lifecycle
cosClient.setBucketLifecycleConfiguration(setBucketLifecycleConfigurationRequest);
```

### Querying Lifecycle

#### Feature Description

This API (GET Bucket lifecycle) is used to query the lifecycle of the specified bucket.

#### Method Prototype

```java
public BucketLifecycleConfiguration getBucketLifecycleConfiguration(String bucketName)
throws CosClientException, CosServiceException;

```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |

#### Return Result Descriptions

- Success: The BucketLifecycleConfiguration class is returned, which contains the lifecycle rule of the bucket.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
BucketLifecycleConfiguration queryLifeCycleRet =
        cosClient.getBucketLifecycleConfiguration(bucketName);
List<Rule> ruleLists = queryLifeCycleRet.getRules();
```

### Deleting Lifecycle

#### Feature Description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle of the specified bucket.

#### Method Prototype

```java
public void deleteBucketLifecycleConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucketLifecycleConfiguration(bucketName);
```


## Versioning
### Setting Versioning

#### Feature Description

This API (PUT Bucket versioning) is used to set the versioning feature of the specified bucket.

#### Method Prototype
```java
public void setBucketVersioningConfiguration(SetBucketVersioningConfigurationRequest setBucketVersioningConfigurationRequest)
    throws CosClientException, CosServiceException;
```

#### Parameter Descriptions
| Parameter Name | Description | Type |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| setBucketVersioningConfigurationRequest | Versioning configuration | SetBucketVersioningConfigurationRequest |


#### Return Result Descriptions
  - Success: No return value.
  - Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

**Enable versioning**

```java
String bucketName = "examplebucket-1250000000";
// Enable versioning
cosClient.setBucketVersioningConfiguration(
new SetBucketVersioningConfigurationRequest(bucketName,
new BucketVersioningConfiguration(BucketVersioningConfiguration.ENABLED)));
```

**Suspend versioning**

```java
String bucketName = "examplebucket-1250000000";
// Suspend versioning
cosClient.setBucketVersioningConfiguration(
new SetBucketVersioningConfigurationRequest(bucketName,
new BucketVersioningConfiguration(BucketVersioningConfiguration.SUSPENDED)));
```

### Querying Versioning

#### Feature Description

This API (GET Bucket versioning) is used to query the versioning information of the specified bucket.

#### Method Prototype
```java
// Method 1. Pass in the bucket name
public BucketVersioningConfiguration getBucketVersioningConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// Method 2. Get through GetBucketVersioningConfigurationRequest
public BucketVersioningConfiguration getBucketVersioningConfiguration(
    GetBucketVersioningConfigurationRequest getBucketVersioningConfigurationRequest)
        throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| getBucketVersioningConfigurationRequest | Request to get the versioning configuration | GetBucketVersioningConfigurationRequest |


#### Return Result Descriptions
- Success: The versioning configuration of the bucket is returned.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request
```java
String bucketName = "examplebucket-1250000000";
// Get versioning information
BucketVersioningConfiguration bvc =
     cosClient.getBucketVersioningConfiguration(bucketName);
// Get versioning information
BucketVersioningConfiguration bvc2 = cosClient.getBucketVersioningConfiguration(
   new GetBucketVersioningConfigurationRequest(bucketName));
```

## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API (PUT Bucket replication) is used to set the cross-region replication rule for the specified bucket.

#### Method Prototype

```java
public void setBucketReplicationConfiguration(
        SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest)
                throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| setBucketReplicationConfigurationRequest | Cross-region replication configuration | SetBucketReplicationConfigurationRequest |

#### Return Result Descriptions

  - Success: No return value.
  - Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Source bucket name which should include the appid
String bucketName = "examplebucket-1250000000";

BucketReplicationConfiguration bucketReplicationConfiguration = new BucketReplicationConfiguration();
// Set the initiator's identity in the format of qcs::cam::uin/<OwnerUin>:uin/<SubUin>
bucketReplicationConfiguration.setRoleName("qcs::cam::uin/123456789:uin/987654543");

// Set the destination bucket and storage class. The format of QCS is: qcs::cos:[region]::[bucketname-AppId]
ReplicationDestinationConfig replicationDestinationConfig = new ReplicationDestinationConfig();
replicationDestinationConfig.setBucketQCS("qcs::cos:ap-chongqing::examplebucket-target-1250000000");
replicationDestinationConfig.setStorageClass(StorageClass.Standard);

// Set the rule status and prefix
ReplicationRule replicationRule = new ReplicationRule();
replicationRule.setStatus(ReplicationRuleStatus.Enabled);
replicationRule.setPrefix("");
replicationRule.setDestinationConfig(replicationDestinationConfig);
// Add a rule
String ruleId = "replication-to-chongqing";
bucketReplicationConfiguration.addRule("replication-to-chongqing", replicationRule);

try {
    SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest =
        new SetBucketReplicationConfigurationRequest(bucketName, bucketReplicationConfiguration);
  cosclient.setBucketReplicationConfiguration(setBucketReplicationConfigurationRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} finally {
    cosclient.shutdown();
}
```

### Querying Cross-region Replication

#### Feature Description

This API (GET Bucket replication) is used to query the cross-region replication rule of the specified bucket.

#### Method Prototype
```java
// Method 1 to get the cross-region replication configuration of the bucket
public BucketReplicationConfiguration getBucketReplicationConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// Method 2 to get the cross-region replication of the bucket		
public BucketReplicationConfiguration getBucketReplicationConfiguration(
            GetBucketReplicationConfigurationRequest getBucketReplicationConfigurationRequest)
            throws CosClientException, CosServiceException;
```
#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| getBucketReplicationConfigurationRequest | Request to get the cross-region replication configuration | GetBucketReplicationConfigurationRequest |

#### Return Result Descriptions
- Success: The cross-region replication rule of the bucket is returned.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request
```java
String bucketName = "examplebucket-1250000000";

// Method 1 to get the cross-region replication configuration of the bucket
BucketReplicationConfiguration brcfRet = cosClient.getBucketReplicationConfiguration(bucketName);

// Method 2 to get the cross-region replication configuration of the bucket
BucketReplicationConfiguration brcfRet2 = cosClient.getBucketReplicationConfiguration(
 new GetBucketCrossOriginConfigurationRequest(bucketName));
```

### Deleting Cross-region Replication

#### Feature Description

This API (DELETE Bucket replication) is used to delete the cross-region replication rule of the specified bucket.

#### Method Prototype
```java
// Method 1 to delete the cross-region replication configuration of the bucket
public void deleteBucketReplicationConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// Method 2 to delete the cross-region replication of the bucket		
public void deleteBucketReplicationConfiguration(
            DeleteBucketReplicationConfigurationRequest deleteBucketReplicationConfigurationRequest)
            throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| deleteBucketReplicationConfigurationRequest | Request to delete the cross-region replication configuration | DeleteBucketReplicationConfigurationRequest |

#### Return Result Descriptions

  - Success: No return value.
  - Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
String bucketName = "examplebucket-1250000000";

// Method 1 to delete the cross-region replication configuration of the bucket
cosClient.deleteBucketReplicationConfiguration(bucketName);

// Method 2 to delete the cross-region replication configuration of the bucket
cosClient.deleteBucketReplicationConfiguration(new DeleteBucketCrossOriginConfigurationRequest(bucketName));
```
