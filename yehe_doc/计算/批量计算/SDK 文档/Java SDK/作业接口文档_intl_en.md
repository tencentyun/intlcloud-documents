
## Development Preparations
- For downloading and installing Java SDK, see [Java](https://intl.cloud.tencent.com/document/product/494/7245).
- - If this is your first time using BatchCompute, please see [Preparation](https://intl.cloud.tencent.com/document/product/599/10807).



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

## Submitting a Job

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();            
jobParams.put("Job.JobName", "batch-job");  // Job name
jobParams.put("Job.JobDescription", "demo job");  // Job description
jobParams.put("Job.Priority", 1);  // Job priority
jobParams.put("Job.Tasks.0.TaskName", "taskA");  // Task name
jobParams.put("Job.Tasks.0.TaskInstanceNum", 10);  // Number of concurrent task instances
jobParams.put("Job.Tasks.0.Application.DeliveryForm", "LOCAL");  // Package source
jobParams.put("Job.Tasks.0.Application.Command", "echo 'hello'");  // Command line
jobParams.put("Job.Tasks.0.EnvId", "env-gbyctcy9");  // Compute environment ID
jobParams.put("Job.Tasks.0.RedirectInfo.StdoutRedirectPath", "cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stdout/");  // Standard output address
jobParams.put("Job.Tasks.0.RedirectInfo.StderrRedirectPath", "cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stderr/");  // Standard error address
jobParams.put("Placement.Zone", "ap-guangzhou-2"); // Availability zone
jobParams.put("Version", "2017-03-12");
 
String submitRes = null;
String jobId = null;
try {
    submitRes = module.call("SubmitJob", jobParams);
    JSONObject result = new JSONObject(submitRes);
    System.out.println(result);

    result = result.getJSONObject("Response");
    jobId = result.getString("JobId");
    System.out.println(jobId);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```
## Terminating a Job

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // Job ID
jobParams.put("Version", "2017-03-12");

String termRes = null;
try {
    termRes = module.call("TerminateJob", jobParams);
    JSONObject result = new JSONObject(termRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```
## Deleting a Job

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // Job ID
jobParams.put("Version", "2017-03-12");

String delRes = null;
try {
    delRes = module.call("DeleteJob", jobParams);
    JSONObject result = new JSONObject(delRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```

## Viewing Job Submission Information

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // Job ID
jobParams.put("Version", "2017-03-12");

String desRes = null;
try {
    desRes = module.call("DescribeJobSubmitInfo", jobParams);
    JSONObject result = new JSONObject(desRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```

## Viewing Job Information

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // Job ID
jobParams.put("Version", "2017-03-12");

String desRes = null;
try {
    desRes = module.call("DescribeJob", jobParams);
    JSONObject result = new JSONObject(desRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```

## Viewing Job List

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("Version", "2017-03-12");

String desRes = null;
try {
    desRes = module.call("DescribeJobs", jobParams);
    JSONObject result = new JSONObject(desRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```
## Viewing Task Information

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // Job ID
jobParams.put("TaskName", "task A");  // Task name
jobParams.put("Version", "2017-03-12");

String desRes = null;
try {
    desRes = module.call("DescribeTask", jobParams);
    JSONObject result = new JSONObject(desRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```

## Terminating a Task Instance

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // Job ID
jobParams.put("TaskName", "taskA");  // Task name
jobParams.put("TaskInstanceIndex", 0);  // Task name
jobParams.put("Version", "2017-03-12");

String termRes = null;
try {
    termRes = module.call("TerminateTaskInstance", jobParams);
    JSONObject result = new JSONObject(termRes);
    System.out.println(result);
} catch (Exception e) {
    System.out.println("error..." + e.getMessage());
}
```
