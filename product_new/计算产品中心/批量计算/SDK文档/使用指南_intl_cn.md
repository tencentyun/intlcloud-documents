## 开发准备

- 选择不同语言的 SDK，下载和安装 。
- 首次使用批量计算，参考 [开始前的准备](https://intl.cloud.tencent.com/document/product/599/10807)。
- 了解更多接口参数，参考 [API 文档](https://intl.cloud.tencent.com/document/product/599/30458)。

## 接入步骤
腾讯云提供了一个代码 [在线生成工具](https://console.cloud.tencent.com/api/explorer?Product=batch&Version=2017-03-12)，以交互式的体验，提供不同语言 SDK 代码示例。
1. 产品选择“批量计算”，找到对应的接口。
2. 根据帮助提示，填写“个人密钥”和“输入参数”。
3. （可选）勾选“只看必选参数”。
4. 在右侧“代码生成”栏中，复制不同语言的代码到本地执行。
5. 在生产使用前，在“在线调用”栏中发起真实请求，验证结果是否符合预期。

## 代码示例

### 提交作业（Python 版本）

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


### 查询作业（Python 版本）

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


### 提交作业（Java 版本）

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

### 查询作业（Java 版本）

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
