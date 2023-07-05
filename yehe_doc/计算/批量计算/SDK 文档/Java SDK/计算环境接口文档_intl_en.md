## Development Preparations
- For downloading and installing Java SDK, see [Java](https://intl.cloud.tencent.com/document/product/494/7245).
- If this is your first time using BatchCompute, please see [Preparation](https://intl.cloud.tencent.com/document/product/599/10807).


## Getting Started

```
import java.util.TreeMap;

import com.qcloud.QcloudApiModuleCenter;
import com.qcloud.Module.Batch;
import com.qcloud.Utilities.Json.JSONObject;

public class BatchDemo {
        public static void main(String[] args) {
                TreeMap<String, Object> config = new TreeMap<String, Object>();
                config.put("SecretId", "Your secretId");
                config.put("SecretKey", "Your secretKey");
                config.put("RequestMethod", "GET");
                config.put("DefaultRegion", "gz"); // Region, gz: guangzhou

                QcloudApiModuleCenter module = new QcloudApiModuleCenter(new Batch(), config);
        }
}
```

## Creating a Compute Environment

```
TreeMap<String, Object> envParams = new TreeMap<String, Object>();
envParams.put("ComputeEnv.EnvName", "batch-env");  // Compute environment name
envParams.put("ComputeEnv.EnvType", "MANAGED");
envParams.put("ComputeEnv.DesiredComputeNodeCount", 10);  // Number of desired nodes
envParams.put("ComputeEnv.EnvData.InstanceType", "S1.SMALL1");  // Instance type
envParams.put("ComputeEnv.EnvData.ImageId", "img-er9shcln"); // Image ID
envParams.put("ComputeEnv.EnvData.SystemDisk.DiskType", "LOCAL_BASIC");  // System disk type
envParams.put("ComputeEnv.EnvData.SystemDisk.DiskSize", 50);  // System disk capacity
envParams.put("ComputeEnv.EnvData.LoginSettings.Password", "B1[habcdB1[habcd");  // Login password
envParams.put("Placement.Zone", "ap-guangzhou-2");  // Availability zone
envParams.put("Version", "2017-03-12");

String createRes = null;
try {
    createRes = module.call("CreateComputeEnv", envParams);
    JSONObject result = new JSONObject(createRes);
    System.out.println(result);
            
    result = result.getJSONObject("Response");
    System.out.println(result.getString("EnvId"));
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```

## Modifying a Compute Environment

```
TreeMap<String, Object> envParams = new TreeMap<String, Object>();
envParams.put("EnvId", "env-cc44pzme");  // Compute environment ID
envParams.put("DesiredComputeNodeCount", 100);  // Number of desired nodes
envParams.put("Version", "2017-03-12");

String modRes = null;
try {
    modRes = module.call("ModifyComputeEnv", envParams);
    JSONObject result = new JSONObject(modRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```


## Deleting a Computer Cluster

```
TreeMap<String, Object> delParams = new TreeMap<String, Object>();
delParams.put("EnvId", "env-cc44pzme");  // Compute environment ID
delParams.put("Version", "2017-03-12");

String delRes = null;
try {
    delRes = module.call("DeleteComputeEnv", delParams);
    JSONObject result = new JSONObject(delRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```

## Viewing the Creation Information of the Compute Environment

```
TreeMap<String, Object> infoParams = new TreeMap<String, Object>();
infoParams.put("EnvId", "env-cc44pzme");  // Compute environment ID
infoParams.put("Version", "2017-03-12");

String infoRes = null;
try {
    infoRes = module.call("DescribeComputeEnvCreateInfo", infoParams);
    JSONObject result = new JSONObject(infoRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```


## Viewing the Compute Environment Information

```
TreeMap<String, Object> desParams = new TreeMap<String, Object>();
desParams.put("EnvId", "env-cc44pzme");  // Compute environment ID
desParams.put("Version", "2017-03-12");

String desRes = null;
try {
    desRes = module.call("DescribeComputeEnv", desParams);
    JSONObject result = new JSONObject(desRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```

## Viewing the List of Compute Environments

```
TreeMap<String, Object> listParams = new TreeMap<String, Object>();
listParams.put("Version", "2017-03-12");

String listRes = null;
try {
    listRes = module.call("DescribeComputeEnvs", listParams);
    JSONObject result = new JSONObject(listRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```

