## Preparations

- Download and install the SDK for your language in Tencent Cloud SDK Center.
- If this is your first time using BatchCompute, please see [Preparation](https://intl.cloud.tencent.com/document/product/599/10807).
- For more information about API parameters, see [API Documentation](https://intl.cloud.tencent.com/document/product/599/30458).

## Access Steps
Tencent Cloud provides an [Online Generation Tool](https://console.cloud.tencent.com/api/explorer?Product=batch&Version=2017-03-12) for an interactive experience as well as sample code for different SDKs.
1. Select **BatchCompute** and find the corresponding API.
2. Enter **Personal key** and **Input parameters** according to the help prompts.
3. (Optional) Select **Only view required parameters**.
4. In the **Code generation** column on the right, copy the different language code to local execution.
5. Before the producer is used, a real request is initiated in the **Online calling** column to verify whether the results meet expectations.

## Sample Codes

### Submitting a Job (Python Version)

```python
from tencentcloud.common import credential
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException 
from tencentcloud.batch.v20170312 import batch_client, models 
try: 
    cred = credential.Credential("your secret id", "your secret key") 
    httpProfile = HttpProfile()
    httpProfile.endpoint = "batch.tencentcloudapi.com"

    clientProfile = ClientProfile()
    clientProfile.httpProfile = httpProfile
    client = batch_client.BatchClient(cred, "ap-guangzhou", clientProfile) 

    req = models.SubmitJobRequest()
    params = '{"Placement":{"Zone":"ap-guangzhou-3"},"Job":{"JobName":"demo","JobDescription":"test job","Priority":1,"Tasks":[{"TaskName":"task","TaskInstanceNum":1,"Application":{"Command":"echo hello"},"ComputeEnv":{"EnvData":{"InstanceType":"S2.SMALL1","ImageId":"img-enf3kukl","SystemDisk":{"DiskType":"CLOUD_PREMIUM","DiskSize":50}}},"MaxRetryCount":1,"Timeout":3600}]}}'
    req.from_json_string(params)

    resp = client.SubmitJob(req) 
    print(resp.to_json_string()) 

except TencentCloudSDKException as err: 
    print(err) 
```


### Querying a Job (Python Version)

```python
from tencentcloud.common import credential
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException 
from tencentcloud.batch.v20170312 import batch_client, models 
try: 
    cred = credential.Credential("your secret id", "your secret key") 
    httpProfile = HttpProfile()
    httpProfile.endpoint = "batch.tencentcloudapi.com"

    clientProfile = ClientProfile()
    clientProfile.httpProfile = httpProfile
    client = batch_client.BatchClient(cred, "ap-guangzhou", clientProfile) 

    req = models.DescribeJobRequest()
    params = '{"JobId":"job-mhgy1dot"}'
    req.from_json_string(params)

    resp = client.DescribeJob(req) 
    print(resp.to_json_string()) 

except TencentCloudSDKException as err: 
    print(err) 
```


### Submitting a Job (Java Version)

```java
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.profile.ClientProfile;
import com.tencentcloudapi.common.profile.HttpProfile;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;

import com.tencentcloudapi.batch.v20170312.BatchClient;

import com.tencentcloudapi.batch.v20170312.models.SubmitJobRequest;
import com.tencentcloudapi.batch.v20170312.models.SubmitJobResponse;

public class SubmitJob
{
    public static void main(String [] args) {
        try{

            Credential cred = new Credential("your secret id", "your secret key");
            
            HttpProfile httpProfile = new HttpProfile();
            httpProfile.setEndpoint("batch.tencentcloudapi.com");

            ClientProfile clientProfile = new ClientProfile();
            clientProfile.setHttpProfile(httpProfile);            
            
            BatchClient client = new BatchClient(cred, "ap-guangzhou", clientProfile);
            
            String params = "{\"Placement\":{\"Zone\":\"ap-guangzhou-3\"},\"Job\":{\"JobName\":\"demo\",\"JobDescription\":\"test job\",\"Priority\":1,\"Tasks\":[{\"TaskName\":\"task\",\"TaskInstanceNum\":1,\"Application\":{\"Command\":\"echo hello\"},\"ComputeEnv\":{\"EnvData\":{\"InstanceType\":\"S2.SMALL1\",\"ImageId\":\"img-enf3kukl\",\"SystemDisk\":{\"DiskType\":\"CLOUD_PREMIUM\",\"DiskSize\":50}}},\"MaxRetryCount\":1,\"Timeout\":3600}]}}";
            SubmitJobRequest req = SubmitJobRequest.fromJsonString(params, SubmitJobRequest.class);
            
            SubmitJobResponse resp = client.SubmitJob(req);
            
            System.out.println(SubmitJobRequest.toJsonString(resp));
        } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
        }

    }
    
}
```

### Querying a Job (Java Version)

```java
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.profile.ClientProfile;
import com.tencentcloudapi.common.profile.HttpProfile;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;

import com.tencentcloudapi.batch.v20170312.BatchClient;

import com.tencentcloudapi.batch.v20170312.models.DescribeJobRequest;
import com.tencentcloudapi.batch.v20170312.models.DescribeJobResponse;

public class DescribeJob
{
    public static void main(String [] args) {
        try{

            Credential cred = new Credential("your secret id", "your secret key");
            
            HttpProfile httpProfile = new HttpProfile();
            httpProfile.setEndpoint("batch.tencentcloudapi.com");

            ClientProfile clientProfile = new ClientProfile();
            clientProfile.setHttpProfile(httpProfile);            
            
            BatchClient client = new BatchClient(cred, "ap-guangzhou", clientProfile);
            
            String params = "{\"JobId\":\"job-mhgy1dot\"}";
            DescribeJobRequest req = DescribeJobRequest.fromJsonString(params, DescribeJobRequest.class);
            
            DescribeJobResponse resp = client.DescribeJob(req);
            
            System.out.println(DescribeJobRequest.toJsonString(resp));
        } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
        }

    }
    
}
```
