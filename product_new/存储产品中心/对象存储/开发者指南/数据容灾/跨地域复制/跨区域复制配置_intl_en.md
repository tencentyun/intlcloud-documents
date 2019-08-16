## Applicable Scenarios
By configuring cross-region replication, you can copy object data from the source bucket to the designated destination bucket in another region. Cross-region replication is ideal for remote disaster recovery, compliance with industry-specific requirements, data migration and backup, access latency optimization, and easier data access to clusters in different regions.
## How to Use
### Using the COS Console
To configure a cross-region replication rule in the COS Console, see [Configuring Cross-region Replication](https://intl.cloud.tencent.com/document/product/436/19235) documentation.
### Using the REST API
You can configure and manage a cross-region replication rule through the REST API as described in the following API documents:
- [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) 
- [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) 
- [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) 

### Using the SDK for C++
This method is provided in the COS SDK for C++. For more information, see [Bucket Management](https://intl.cloud.tencent.com/document/product/436/31523) for the SDK.

Directions:
1. Initialize cosClient.
2. Run PutBucketReplication, GetBucketReplication, and DeleteBucketReplication to configure, get, and delete the cross-region replication rule, respectively.

#### Configuring a Cross-Region Replication Rule 
Sample code:

```
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// The constructor of PutBucketReplicationReq requires bucket_name to be passed in
qcloud_cos::PutBucketReplicationReq req(bucket_name);
req.SetRole("qcs::cam::uin/***:uin/****");
qcloud_cos::ReplicationRule rule("sevenyou_10m", "qcs:id/0:cos:cn-south:appid/***:sevenyousouthtest", "", "RuleId_01", true);
req.AddReplicationRule(rule)

qcloud_cos::PutBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.PutBucketReplication(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // Failed to set cross-region replication. You can call the member function of CosResult to output the error information such as requestID
}
```

#### Getting a Cross-Region Replication Rule 
Sample code:

```
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// The constructor of GetBucketReplicationReq requires bucket_name to be passed in
qcloud_cos::GetBucketReplicationReq req(bucket_name);
qcloud_cos::GetBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.GetBucketReplication(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // Failed to get the cross-region replication configuration. You can call the member function of CosResult to output the error information such as requestID
}
```

#### Deleting a Cross-Region Replication Rule 
Sample code:

```
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// The constructor of DeleteBucketReplicationReq requires bucket_name to be passed in
qcloud_cos::DeleteBucketReplicationReq req(bucket_name);
qcloud_cos::DeleteBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketReplication(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // Failed to delete the cross-region replication configuration. You can call the member function of CosResult to output the error information such as requestID
}
```
### Using the SDK for C
This method is provided in the COS SDK for C. For more information, see [Bucket Management](https://cloud.tencent.com/document/product/436/35559) for the SDK.

Directions:
1. Initialize cosClient.
2. Run PutBucketReplication, GetBucketReplication, and DeleteBucketReplication to configure, get, and delete the cross-region replication rule, respectively.

#### Configuring a Cross-Region Replication Rule
Sample code:

```
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

//create memory pool
cos_pool_create(&p, NULL);

//init request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//put bucket replication
cos_replication_params_t *replication_param = NULL;
replication_param = cos_create_replication_params(p);
cos_str_set(&replication_param->role, "qcs::cam::uin/100000616666:uin/100000616666");

cos_replication_rule_content_t *rule = NULL;
rule = cos_create_replication_rule_content(p);
cos_str_set(&rule->id, "Rule_01");
cos_str_set(&rule->status, "Enabled");
cos_str_set(&rule->prefix, "test1");
cos_str_set(&rule->dst_bucket, "qcs:id/0:cos:cn-east:appid/1253686666:replicationtest");
cos_list_add_tail(&rule->node, &replication_param->rule_list);

rule = cos_create_replication_rule_content(p);
cos_str_set(&rule->id, "Rule_02");
cos_str_set(&rule->status, "Disabled");
cos_str_set(&rule->prefix, "test2");
cos_str_set(&rule->storage_class, "Standard_IA");
cos_str_set(&rule->dst_bucket, "qcs:id/0:cos:cn-east:appid/1253686666:replicationtest");
cos_list_add_tail(&rule->node, &replication_param->rule_list);

rule = cos_create_replication_rule_content(p);
cos_str_set(&rule->id, "Rule_03");
cos_str_set(&rule->status, "Enabled");
cos_str_set(&rule->prefix, "test3");
cos_str_set(&rule->storage_class, "Standard_IA");
cos_str_set(&rule->dst_bucket, "qcs:id/0:cos:cn-east:appid/1253686666:replicationtest");
cos_list_add_tail(&rule->node, &replication_param->rule_list);

s = cos_put_bucket_replication(options, &bucket, replication_param, &resp_headers);
if (cos_status_is_ok(s)) {
printf("put bucket replication succeeded\n");
} else {
printf("put bucket replication failed\n");
}

//destroy memory pool
cos_pool_destroy(p);
```
#### Getting a Cross-Region Replication Rule
Sample code:

```
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

//create memory pool
cos_pool_create(&p, NULL);

//init request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//get bucket replication
cos_replication_params_t *replication_param2 = NULL;
replication_param2 = cos_create_replication_params(p);
s = cos_get_bucket_replication(options, &bucket, replication_param2, &resp_headers);

if (cos_status_is_ok(s)) {
printf("get bucket replication succeeded\n");
printf("ReplicationConfiguration role: %s\n", replication_param2->role.data);
cos_replication_rule_content_t *content = NULL;
cos_list_for_each_entry(cos_replication_rule_content_t, content, &replication_param2->rule_list, node) {
printf("ReplicationConfiguration rule, id:%s, status:%s, prefix:%s, dst_bucket:%s, storage_class:%s\n",
content->id.data, content->status.data, content->prefix.data, content->dst_bucket.data, content->storage_class.data);
}
} else {
printf("get bucket replication failed\n");
}

//destroy memory pool
cos_pool_destroy(p);
```
#### Deleting a Cross-Region Replication Rule

```
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

//create memory pool
cos_pool_create(&p, NULL);

//init request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//delete bucket cors
s = cos_delete_bucket_replication(options, &bucket, &resp_headers);
if (cos_status_is_ok(s)) {
printf("delete bucket replication succeeded\n");
} else {
printf("delete bucket replication failed\n");
}

//destroy memory pool
cos_pool_destroy(p);
```
