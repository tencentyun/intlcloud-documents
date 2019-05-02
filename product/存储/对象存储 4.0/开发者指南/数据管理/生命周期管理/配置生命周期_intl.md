## Use Cases

With lifecycle configuration, the predefined action can be automatically performed when a rule applies to objects. For example:

- Transition: Transition objects to STANDARD_IA storage or ARCHIVE storage after a specified time of period.
- Expiration: Automatically delete objects after they reach the specified expiration time.

For more information, see [Instructions](/document/product/436/17028) on lifecycle. You need to specify [configuration elements](/document/product/436/17029) during lifecycle configuration.

## Directions
### Via the COS Console
For more information on lifecycle configuration on the COS Console, see [Lifecycle Management](https://cloud.tencent.com/document/product/436/14605) in Console Guide.

### Via REST API

You can configure and manage the lifecycle of objects in a bucket using the REST API, as described in the following API documentation:

- [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280)
- [GET Buket lifecycle](https://cloud.tencent.com/document/product/436/8278)
- [DELETE Bucket lifecycle](https://cloud.tencent.com/document/product/436/8284)

### Via C++ SDK

This method is provided in the C++ SDK for COS. See [Put Bucket Lifecycle](https://cloud.tencent.com/document/product/436/12302#put-bucket-lifecycle) in C++ SDK API Documentation.

Steps:

1. Initialize client cosClient.
2. Execute putBucketLifecycle and GetBucketLifecycle to configure and retrieve the bucket lifecycle.

#### Configure the lifecycle

Sample code:

```
cloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// The bucket_name is required in the constructor of PutBucketLifecycleReq.
qcloud_cos::PutBucketLifecycleReq req(bucket_name);
qcloud_cos::PutBucketLifecycleResp resp;

// Set rules
{
    qcloud_cos::LifecycleRule rule;
    rule.SetIsEnable(true);
    rule.SetId("lifecycle_rule00");
	
    // Set filters. Here filter out objects with the tag key of "datalevel" and tag value of "backup" so that the rule applies only to these objects.
    qcloud_cos::LifecycleFilter filter;
    Lifecycle tag;
    tag.key = "datalevel";
    tag.value = "backup";
    filter.AddTag(tag);
    rule.SetFilter(filter);

    // Transition objects to STANDARD_IA 30 days after creation.
    qcloud_cos::LifecycleTransition transition1;
    transition1.SetDays(30);
    transition1.SetStorageClass("STANDARD_IA");
    rule.AddTransition(transition1);
	
    // Transition objects to ARCHIVE 365 days after creation.
    qcloud_cos::LifecycleTransition transition2;
    transition2.SetDays(365);
    transition2.SetStorageClass("ARCHIVE");
    rule.AddTransition(transition2);
	
    req.AddRule(rule);
}

qcloud_cos::CosResult result = cos.PutBucketLifecycle(req, &resp);
// If the call is successful, call resp's member functions to get the response content.
if (result.IsSucc()) {
    // ...
} else {
    // If the lifecycle configuration fails, call CosResult's member functions to output error information, such as requestID.
}
```

#### Retrieve the lifecycle
Sample code:

```
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// The bucket_name is required in the constructor of GetBucketLifecycleReq.
qcloud_cos::GetBucketLifecycleReq req(bucket_name);
qcloud_cos::GetBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.GetBucketLifecycle(req, &resp);

// If the call is successful, call resp's member functions to get the response content.
if (result.IsSucc()) {
    // ...
} else {
    // If fail to obtain the lifecycle configuration, call CosResult's member functions to output error information, such as requestID.
}
```

### Via Python SDK
This method is provided in the Python SDK for COS. See [Configure Bucket Lifecycle](https://cloud.tencent.com/document/product/436/12270#.E8.AE.BE.E7.BD.AE-bucket-.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F.E9.85.8D.E7.BD.AE) in Python SDK API Documentation.
#### Configure the lifecycle
Steps:

1. Use the CosConfig library for configuration, and initialize client CosS3Client.
2. Execute put_bucket_lifecycle() to configure the bucket lifecycle.

The sample code is as follows:

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # Replaced with user's secretId
secret_key = 'xxxxxxx'      # Replaced with user's secretKey
region = 'ap-beijing-1'     # Replaced with user's Region
token = ''                  # Token is required to use a temporary key. It is optional. Default is empty.

config = CosConfig(Access_id=secret_id, Access_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
lifecycle_config = {
    'Rule': [
        {
            'Status': 'Enabled',
            'Filter': {
                # Apply to objects with the tag key of "datalevel" and tag value of "backup"
                'Tag': [
                    {
                        'Key': 'datalevel',
                        'Value': 'backup'
                    }
                ]
            },
            'Transition': [
                {
                    # Transition to Standard_IA 30 days after creation
                    'Days': 30,
                    'StorageClass': 'Standard_IA'
                },
                {
                    # Transition to Archive 365 days after creation
                    'Days': 365,
                    'StorageClass': 'Archive'
                }
            ],
            'Expiration': {
                # Delete after the expiration period of 3650 days is reached
                'Days': 3650
            }
        }
    ]
}

response = client.put_bucket_lifecycle(
    Bucket=bucket,
    LifecycleConfiguration=lifecycle_config
)
```

#### Obtain the lifecycle
Steps:

1. Use the CosConfig class for configuration, and initialize CosS3Client.
2. Execute get_bucket_lifecycle() to obtain the bucket lifecycle.

The following code is used to obtain lifecycle configuration:

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # Replaced with user's secretId
secret_key = 'xxxxxxx'      # Replaced with user's secretKey
region = 'ap-beijing-1'     # Replaced with user's Region
token = ''                  # Token is required to use a temporary key. It is optional. Default is empty.

config = CosConfig(Access_id=secret_id, Access_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
response = client.get_bucket_lifecycle(
    Bucket=bucket    
)
```

### Via PHP SDK
This method is provided in the PHP SDK for COS. See [Put Bucket Lifecycle](https://cloud.tencent.com/document/product/436/12267#putbucketlifecycle) in PHP SDK API Documentation.

#### Configure the lifecycle
Steps:

1. Initialize client cosClient.
2. Execute putBucketLifecycle to configure the bucket lifecycle.

The following code shows how to configure the bucket lifecycle:

```php
## putBucketLifecycle (Configure bucket lifecycle)
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv('COS_KEY'),
        'secretKey' => getenv('COS_SECRET'))));

//The bucket name entered must be in a format of {name}-{appid}
$bucket = 'lewzylu02-1252448703';

try {
    $result = $cosClient->putBucketLifecycle(array(
        'Bucket' => $bucket,
        'Rules' => array(
            array(
                'Status' => 'Enabled',
                'Filter' => array(
                    'Tag' => array(
                        'Key' => 'datalevel',
                        'Value' => 'backup'
                    )
                ),
                'Transitions' => array(
                   array(
                    # Transition to Standard_IA 30 days after creation
                    'Days' => 30,
                    'StorageClass' => 'Standard_IA'),
                array(
                    # Transition to Archive 365 days after creation
                    'Days' => 365,
                    'StorageClass' => 'Archive')
                ),
                'Expiration' => array(
                # Delete after the expiration period of 3650 days is reached
                'Days' => 3650,
                )
            )
        )
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### Obtain the lifecycle
Steps:

1. Initialize client cosClient.
2. Execute getBucketLifecycle to obtain the bucket lifecycle.

The following code shows how to obtain the bucket lifecycle:

```php
## getBucketLifecycle (Obtain  bucket  lifecycle)
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv('COS_KEY'),
        'secretKey' => getenv('COS_SECRET'))));

//The bucket name entered must be in a format of {name}-{appid}
$bucket = 'lewzylu02-1252448703';

try {
    $result = $cosClient->getBucketLifecycle(array(
        'Bucket' =>$bucket,
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### Delete the lifecycle
Steps:

1. Initialize client cosClient.
2. Execute deleteBucketLifecycle to delete the bucket lifecycle.

The following code shows how to delete the bucket lifecycle:

```php
## deleteBucketLifecycle (Delete bucket lifecycle)
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv('COS_KEY'),
        'secretKey' => getenv('COS_SECRET'))));

//The bucket name entered must be in a format of {name}-{appid}
$bucket = 'lewzylu02-1252448703';

try {
    $result = $cosClient->deleteBucketLifecycle(array(
        'Bucket' =>$bucket,
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

