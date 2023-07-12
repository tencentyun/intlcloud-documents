### Introduction

This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycles, versioning, and cross-region replication.

**Cross-origin access**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting a cross-origin access configuration | Sets the cross-origin access permissions of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying a cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting a cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting a lifecycle configuration | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation Name | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning configuration of a bucket |
| [GET Bucket versioning](https://cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication rules | Sets the cross-region replication rules of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication rules | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication rules| Deletes the cross-region replication rules of a bucket |

## Cross-origin access

### Setting a cross-origin access configuration

## Feature description 

This API is used to set the cross-origin access configuration of a bucket.

#### Method prototype

```java
public void setBucketCrossOriginConfiguration(String bucketName, BucketCrossOriginConfiguration bucketCrossOriginConfiguration);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------ |
| bucketName | Bucket naming format is `BucketName-APPID`. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| bucketCrossOriginConfiguration | The cross-origin access rules set for a bucket | BucketCrossOriginConfiguration |

#### Response description

- Successful: No value is returned.
-Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 

[//]: # (.cssg-snippet-put-bucket-cors)
```java
// Enter the bucket name in the format: BucketName-APPID.
String bucketName = "examplebucket-1250000000";
| bucketCrossOriginConfiguration | The cross-domain access rules set for a bucket | BucketCrossOriginConfiguration |
List<CORSRule> corsRules = new ArrayList<CORSRule>();
CORSRule corsRule = new CORSRule();
// Rule name
corsRule.setId("set-bucket-cors-test");
// Allowed HTTP method
corsRule.setAllowedMethods(CORSRule.AllowedMethods.PUT, CORSRule.AllowedMethods.GET, CORSRule.AllowedMethods.HEAD);
corsRule.setAllowedHeaders("x-cos-grant-full-control");
corsRule.setAllowedOrigins("http://mail.qq.com", "http://www.qq.com", "http://video.qq.com");
corsRule.setExposedHeaders("x-cos-request-id");
corsRule.setMaxAgeSeconds(60);
corsRules.add(corsRule);
bucketCORS.setRules(corsRules);
cosClient.setBucketCrossOriginConfiguration(bucketName, bucketCORS);
```

### Querying a cross-origin access configuration

#### Feature description

This API is used to query the cross-origin access configuration of a bucket.

#### Method prototype

```java
public BucketCrossOriginConfiguration getBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

-Success: Returns the cross-origin rules for the bucket.
-Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 

[//]: # (.cssg-snippet-get-bucket-cors)
```java
// Enter the bucket name in the format: BucketName-APPID.
String bucketName = "examplebucket-1250000000";
BucketCrossOriginConfiguration corsGet = cosClient.getBucketCrossOriginConfiguration(bucketName);
List<CORSRule> corsRules = corsGet.getRules();
for (CORSRule rule : corsRules) {
    List<CORSRule.AllowedMethods> allowedMethods = rule.getAllowedMethods();
    List<String> allowedHeaders = rule.getAllowedHeaders();
    List<String> allowedOrigins = rule.getAllowedOrigins();
    List<String> exposedHeaders = rule.getExposedHeaders();
    int maxAgeSeconds = rule.getMaxAgeSeconds();
}
```

### Deleting a cross-origin configuration

#### Feature description

This API is used to delete the cross-origin access configuration of a bucket.

#### Method prototype

```java
public void deleteBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

- Successful: No value is returned.
-Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 

[//]: # (.cssg-snippet-delete-bucket-cors)
```java
Bucket. Format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucketCrossOriginConfiguration(bucketName);
```

## Lifecycle

### Setting a lifecycle configuration

#### Feature description

This API is used to set the lifecycle configuration of a bucket.

#### Method prototype

```java
public void setBucketLifecycleConfiguration(String bucketName, BucketLifecycleConfiguration bucketLifecycleConfiguration) 
        throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------------------------- | ------------------------------------------------------------ | ---------------------------- |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| bucketLifecycleConfiguration | Lifecycle configuration | BucketLifecycleConfiguration |

#### Response description

- Successful: No value is returned.
-Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```java
List<BucketLifecycleConfiguration.Rule> rules = new ArrayList<BucketLifecycleConfiguration.Rule>();
// Rule 1: Delete files whose paths start with hongkong_movie/ after 30 days
BucketLifecycleConfiguration.Rule deletePrefixRule = new BucketLifecycleConfiguration.Rule();
deletePrefixRule.setId("delete prefix xxxy after 30 days");
deletePrefixRule.setFilter(new LifecycleFilter(new LifecyclePrefixPredicate("hongkong_movie/")));
// Deleting files that have been uploaded or modified for 30 days
deletePrefixRule.setExpirationInDays(30);
// Setting rules to active
deletePrefixRule.setStatus(BucketLifecycleConfiguration.ENABLED);

// Rule 2: Put files into low frequency after 20 days and delete them after one year
BucketLifecycleConfiguration.Rule standardIaRule = new BucketLifecycleConfiguration.Rule();
standardIaRule.setId("standard_ia transition");
standardIaRule.setFilter(new LifecycleFilter(new LifecyclePrefixPredicate("standard_ia/")));
List<BucketLifecycleConfiguration.Transition> standardIaTransitions = new ArrayList<BucketLifecycleConfiguration.Transition>();
BucketLifecycleConfiguration.Transition standardTransition = new BucketLifecycleConfiguration.Transition();
standardTransition.setDays(20);
standardTransition.setStorageClass(StorageClass.Standard_IA.toString());
standardIaTransitions.add(standardTransition);
standardIaRule.setTransitions(standardIaTransitions);
standardIaRule.setStatus(BucketLifecycleConfiguration.ENABLED);
standardIaRule.setExpirationInDays(365);

// Adding two rules to the policy set
rules.add(deletePrefixRule);
rules.add(standardIaRule);

// Generating bucketLifecycleConfiguration
BucketLifecycleConfiguration bucketLifecycleConfiguration =
        new BucketLifecycleConfiguration();
bucketLifecycleConfiguration.setRules(rules);

// Enter the Bucket name in the format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
SetBucketLifecycleConfigurationRequest setBucketLifecycleConfigurationRequest =
        new SetBucketLifecycleConfigurationRequest(bucketName, bucketLifecycleConfiguration);

// Configuring the lifecycle configuration
cosClient.setBucketLifecycleConfiguration(setBucketLifecycleConfigurationRequest);
```

### Querying a lifecycle configuration

## Feature description

This API is used to query the lifecycle configuration of a bucket.

#### Method prototype

```java
public BucketLifecycleConfiguration getBucketLifecycleConfiguration(String bucketName)
throws CosClientException, CosServiceException;

```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

- Successful: The BucketLifecycleConfiguration type, including the lifecycle rules of the bucket, is returned.
-Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```java
// Entering the bucket name in the format: BucketName-APPID.
String bucketName = "examplebucket-1250000000";
BucketLifecycleConfiguration queryLifeCycleRet =
        cosClient.getBucketLifecycleConfiguration(bucketName);
List<BucketLifecycleConfiguration.Rule> ruleLists = queryLifeCycleRet.getRules();
```

### Deleting a lifecycle configuration

#### Feature description

This API is used to delete the lifecycle configuration of a bucket.

#### Method prototype

```java
public void deleteBucketLifecycleConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

- Successful: No value is returned.
-Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```java
Bucket. Format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucketLifecycleConfiguration(bucketName);
```


## Versioning
### Setting versioning

#### Feature description

This API is used to set the versioning configuration of a bucket.

#### Method prototype
```java
public void setBucketVersioningConfiguration(SetBucketVersioningConfigurationRequest setBucketVersioningConfigurationRequest)
    throws CosClientException, CosServiceException;
```

#### Parameter description
| Parameter Name | Description | Type |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| setBucketVersioningConfigurationRequest | Versioning configuration | SetBucketVersioningConfigurationRequest |


#### Response description
  - Successful: No value is returned.
  -Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 

**Enabling versioning**

[//]: # (.cssg-snippet-put-bucket-versioning)
```java
String bucketName = "examplebucket-1250000000";
// Enable Versioning
cosClient.setBucketVersioningConfiguration(
        new SetBucketVersioningConfigurationRequest(bucketName,
                new BucketVersioningConfiguration(BucketVersioningConfiguration.ENABLED)));
```

**Suspending Versioning**

```java
String bucketName = "examplebucket-1250000000";
// Suspend versioning
cosClient.setBucketVersioningConfiguration(
new SetBucketVersioningConfigurationRequest(bucketName,
new BucketVersioningConfiguration(BucketVersioningConfiguration.SUSPENDED)));
```

### Querying versioning

#### Feature description

This API is used to query the versioning configuration of a bucket.

#### Method prototype
```java
// Method 1: Enter the bucket name
public BucketVersioningConfiguration getBucketVersioningConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// Method 2: Obtain the configuration via a GetBucketVersioningConfigurationRequest
public BucketVersioningConfiguration getBucketVersioningConfiguration(
    GetBucketVersioningConfigurationRequest getBucketVersioningConfigurationRequest)
        throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| getBucketVersioningConfigurationRequest | Obtaining versioning configuration request | GetBucketVersioningConfigurationRequest |


#### Response description
-Success: The multi-version configuration of the bucket is returned.
-Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 
[//]: # (.cssg-snippet-get-bucket-versioning)
```java
String bucketName = "examplebucket-1250000000";
// Obtaining the versioning configuration
BucketVersioningConfiguration bvc =
        cosClient.getBucketVersioningConfiguration(bucketName);
// Obtaining the versioning configuration
BucketVersioningConfiguration bvc2 = cosClient.getBucketVersioningConfiguration(
        new GetBucketVersioningConfigurationRequest(bucketName));
```

## Cross-region replication
### Setting cross-region replication rules

#### Feature description

This API is used to set the cross-region replication rules of a bucket

#### Method prototype

```java
public void setBucketReplicationConfiguration(
        SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest)
                throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Parameter Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| setBucketReplicationConfigurationRequest | Cross-region replication configuration | SetBucketReplicationConfigurationRequest |

#### Response description

  - Successful: No value is returned.
  -Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 

[//]: # (.cssg-snippet-put-bucket-replication)
```java
// Source bucket name, including appid
String bucketName = "examplebucket-1250000000";

BucketReplicationConfiguration bucketReplicationConfiguration = new BucketReplicationConfiguration();
// Configure initiator identity in the format: qcs::cam::uin/<OwnerUin>:uin/<SubUin>
bucketReplicationConfiguration.setRoleName("qcs::cam::uin/100000000001:uin/100000000001");

// Configure the destination bucket and storage class in the QCS format: qcs::cos:[region]::[bucketname-AppId]
ReplicationDestinationConfig replicationDestinationConfig = new ReplicationDestinationConfig();
replicationDestinationConfig.setBucketQCS("qcs::cos:ap-beijing::destinationbucket-1250000000");
replicationDestinationConfig.setStorageClass(StorageClass.Standard);

// Configure the rule status and prefix
ReplicationRule replicationRule = new ReplicationRule();
replicationRule.setStatus(ReplicationRuleStatus.Enabled);
replicationRule.setPrefix("");
replicationRule.setDestinationConfig(replicationDestinationConfig);
### Adding a rule
String ruleId = "replication-to-beijing";
bucketReplicationConfiguration.addRule(ruleId, replicationRule);

SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest =
        new SetBucketReplicationConfigurationRequest(bucketName, bucketReplicationConfiguration);
cosClient.setBucketReplicationConfiguration(setBucketReplicationConfigurationRequest);
```

### Querying cross-region replication rules

#### Feature description

This API is used to query the cross-region replication rules of a bucket.

#### Method prototype
```java
// Obtaining the cross-region replication configuration of a bucket method 1
public BucketReplicationConfiguration getBucketReplicationConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// Obtaining the cross-region replication configuration of a bucket method 2		
public BucketReplicationConfiguration getBucketReplicationConfiguration(
            GetBucketReplicationConfigurationRequest getBucketReplicationConfigurationRequest)
            throws CosClientException, CosServiceException;
```
#### Parameter description

| Parameter Name | Parameter Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| getBucketReplicationConfigurationRequest | Obtaining cross-region replication configuration request                                       | GetBucketReplicationConfigurationRequest |

#### Response description
-Success: Returns the cross-region replication rule for the bucket.
-Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 
[//]: # (.cssg-snippet-get-bucket-replication)
```java
String bucketName = "examplebucket-1250000000";

// Obtaining the cross-region replication configuration of a bucket method 1
BucketReplicationConfiguration brcfRet = cosClient.getBucketReplicationConfiguration(bucketName);

// Obtaining the cross-region replication configuration of a bucket method 2
BucketReplicationConfiguration brcfRet2 = cosClient.getBucketReplicationConfiguration(
        new GetBucketReplicationConfigurationRequest(bucketName));
```

## Deleting cross-region replication rules

#### Feature description

This API is used to delete the cross-region replication rules of a bucket.

#### Method prototype
```java
// Deleting the cross-region replication configuration of a bucket method 1
public void deleteBucketReplicationConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// Deleting the cross-region replication configuration of a bucket method 2		
public void deleteBucketReplicationConfiguration(
            DeleteBucketReplicationConfigurationRequest deleteBucketReplicationConfigurationRequest)
            throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Parameter Description | Type |
| ------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| deleteBucketReplicationConfigurationRequest | Deleting cross-region replication configuration request                                       | DeleteBucketReplicationConfigurationRequest |

#### Response description

  - Successful: No value is returned.
  -Failure: An error (such as an authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting] (https://intl.cloud.tencent.com/document/product/436/30599).

#### Sample request 

[//]: # (.cssg-snippet-delete-bucket-replication)
```java
String bucketName = "examplebucket-1250000000";

// Deleting the cross-region replication configuration of a bucket method 1
cosClient.deleteBucketReplicationConfiguration(bucketName);

// Deleting the cross-region replication configuration of a bucket method 2
cosClient.deleteBucketReplicationConfiguration(new DeleteBucketReplicationConfigurationRequest(bucketName));
```
