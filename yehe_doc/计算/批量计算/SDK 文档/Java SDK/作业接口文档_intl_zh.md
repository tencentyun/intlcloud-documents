
## 开发准备
- 下载和安装 [Java SDK](https://intl.cloud.tencent.com/zh/document/product/494/7245) 。
- - 首次使用批量计算，参考 [开始前的准备](https://intl.cloud.tencent.com/document/product/599/10807)。



## 快速入门

```
import java.util.TreeMap;

import com.qcloud.QcloudApiModuleCenter;
import com.qcloud.Module.Batch;
import com.qcloud.Utilities.Json.JSONObject;

public class BatchDemo {
        public static void main(String[] args) {
                TreeMap<String, Object> config = new TreeMap<String, Object>();
                config.put("SecretId", "您的SecretId");
                config.put("SecretKey", "您的SecretKey");
                config.put("RequestMethod", "GET");
                config.put("DefaultRegion", "gz"); // 地域，gz: guangzhou

                QcloudApiModuleCenter module = new QcloudApiModuleCenter(new Batch(), config);
        }
}
```

## 提交作业

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();            
jobParams.put("Job.JobName", "batch-job");  // 作业名称
jobParams.put("Job.JobDescription", "demo job");  // 作业描述
jobParams.put("Job.Priority", 1);  // 作业优先级
jobParams.put("Job.Tasks.0.TaskName", "taskA");  // 任务名称
jobParams.put("Job.Tasks.0.TaskInstanceNum", 10);  // 任务实例并发数
jobParams.put("Job.Tasks.0.Application.DeliveryForm", "LOCAL");  // 程序包来源
jobParams.put("Job.Tasks.0.Application.Command", "echo 'hello'");  // 命令行
jobParams.put("Job.Tasks.0.EnvId", "env-gbyctcy9");  // 计算环境标识
jobParams.put("Job.Tasks.0.RedirectInfo.StdoutRedirectPath", "cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stdout/");  // 标准输出地址
jobParams.put("Job.Tasks.0.RedirectInfo.StderrRedirectPath", "cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stderr/");  // 标准错误地址
jobParams.put("Placement.Zone", "ap-guangzhou-2"); // 可用区
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
## 终止作业

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 作业标识
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
## 删除作业

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 作业标识
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

## 查看作业的提交信息

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 作业标识
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

## 查看作业信息

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 作业标识
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

## 查看作业列表

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
## 查看任务信息

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 作业标识
jobParams.put("TaskName", "task A");  // 任务名称
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

## 终止任务实例

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 作业标识
jobParams.put("TaskName", "taskA");  // 任务名称
jobParams.put("TaskInstanceIndex", 0);  // 任务名称
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
