This document provides an overview of APIs and SDK code samples related to lifecycle.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle configuration | Sets lifecycle management configuration for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of bucket |

## Setting Lifecycle Configuration

#### Feature description

This API is used to set the lifecycle configuration for a bucket.

#### Method prototype

```java
public void setBucketLifecycleConfiguration(String bucketName, BucketLifecycleConfiguration bucketLifecycleConfiguration) 
        throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```java
List<BucketLifecycleConfiguration.Rule> rules = new ArrayList<BucketLifecycleConfiguration.Rule>();
// Rule 1: delete files whose paths start with hongkong_movie/ after 30 days
BucketLifecycleConfiguration.Rule deletePrefixRule = new BucketLifecycleConfiguration.Rule();
deletePrefixRule.setId("delete prefix xxxy after 30 days");
deletePrefixRule.setFilter(new LifecycleFilter(new LifecyclePrefixPredicate("hongkong_movie/")));
// Deleting files that have been uploaded or modified for 30 days
deletePrefixRule.setExpirationInDays(30);
// Setting rules to active
deletePrefixRule.setStatus(BucketLifecycleConfiguration.ENABLED);

// Rule 2: put files into low frequency after 20 days and delete them after one year
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

// Bucket name in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
SetBucketLifecycleConfigurationRequest setBucketLifecycleConfigurationRequest =
        new SetBucketLifecycleConfigurationRequest(bucketName, bucketLifecycleConfiguration);

// Configuring the lifecycle configuration
cosClient.setBucketLifecycleConfiguration(setBucketLifecycleConfigurationRequest);
```



#### Parameter description

| Parameter | Description | Type |
| ---------------------------- | ------------------------------------------------------------ | ---------------------------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| bucketLifecycleConfiguration | Lifecycle configuration | BucketLifecycleConfiguration |

#### Response description

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Querying Lifecycle Configuration

#### Feature description

This API is used to query the lifecycle management configuration for a bucket.

#### Method prototype

```java
public BucketLifecycleConfiguration getBucketLifecycleConfiguration(String bucketName)
throws CosClientException, CosServiceException;

```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```java
// Entering the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
BucketLifecycleConfiguration queryLifeCycleRet =
        cosClient.getBucketLifecycleConfiguration(bucketName);
List<BucketLifecycleConfiguration.Rule> ruleLists = queryLifeCycleRet.getRules();
```


#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

- Success: the `BucketLifecycleConfiguration` class is returned, which contains the lifecycle rule of the bucket.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Deleting Lifecycle Configuration

#### Feature description

This API is used to delete the lifecycle configuration of a Bucket.

#### Method prototype

```java
public void deleteBucketLifecycleConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```java
// Bucket name in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucketLifecycleConfiguration(bucketName);
```


#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
