## 開発準備
- [Java SDK](https://cloud.tencent.com/document/sdk/Java)をダウンロードしてインストールします。
- 初めてBatchを使用する場合は、[始める前の準備](https://cloud.tencent.com/document/product/599/10807)を参照してください。
- ジョブ構成パラメータの詳細については、[ジョブ提出APIドキュメント](https://cloud.tencent.com/document/product/599/12683)を参照してください。

## クイックスタート

```
import java.util.TreeMap;

import com.qcloud.QcloudApiModuleCenter;
import com.qcloud.Module.Batch;
import com.qcloud.Utilities.Json.JSONObject;

public class BatchDemo {
        public static void main(String[] args) {
                TreeMap<String, Object> config = new TreeMap<String, Object>();
                config.put("SecretId", "お使いのSecretId");
                config.put("SecretKey", "お使いのSecretKey");
                config.put("RequestMethod", "GET");
                config.put("DefaultRegion", "gz"); //地域、gz：guangzhou

                QcloudApiModuleCenter module = new QcloudApiModuleCenter(new Batch(), config);
        }
}
```

## ジョブ提出

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();            
jobParams.put("Job.JobName", "batch-job");  // ジョブ名
jobParams.put("Job.JobDescription", "demo job");  // ジョブの説明
jobParams.put("Job.Priority", 1);  // ジョブの優先順位
jobParams.put("Job.Tasks.0.TaskName", "taskA");  // タスク名
jobParams.put("Job.Tasks.0.TaskInstanceNum", 10);  // タスクインスタンスの同時実行数
jobParams.put("Job.Tasks.0.Application.DeliveryForm", "LOCAL");  // パッケージソース
jobParams.put("Job.Tasks.0.Application.Command", "echo 'hello'");  // コマンドライン
jobParams.put("Job.Tasks.0.EnvId", "env-gbyctcy9");  // 計算環境タグ
jobParams.put("Job.Tasks.0.RedirectInfo.StdoutRedirectPath", "cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stdout/");  // 標準出力アドレス
jobParams.put("Job.Tasks.0.RedirectInfo.StderrRedirectPath", "cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stderr/");  // 標準エラーアドレス
jobParams.put("Placement.Zone", "ap-guangzhou-2"); // Availability Zone
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
パラメータの説明とエラーメッセージの詳細については、[ジョブ提出APIドキュメント](https://cloud.tencent.com/document/product/599/12683)を参照してください。

## ジョブ終了

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // ジョブタグ
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
パラメータの説明とエラーメッセージの詳細については、[ジョブ終了APIドキュメント](https://cloud.tencent.com/document/product/599/12689)を参照してください。

## ジョブ削除

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // ジョブタグ
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
パラメータの説明とエラーメッセージの詳細については、[ジョブ削除APIドキュメント](https://cloud.tencent.com/document/product/599/12682)を参照してください。

## ジョブ提出情報の確認

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // ジョブタグ
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
パラメータの説明とエラーメッセージの詳細については、[ジョブ提出情報の確認APIドキュメント](https://cloud.tencent.com/document/product/599/12687)を参照してください。

## ジョブ情報の確認

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // ジョブタグ
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
パラメータの説明とエラーメッセージの詳細については、[ジョブ情報の確認APIドキュメント](https://cloud.tencent.com/document/product/599/12685)を参照してください。

## ジョブリストの確認

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
パラメータの説明とエラーメッセージの詳細については、[ジョブリストの確認APIドキュメント](https://cloud.tencent.com/document/product/599/12686)を参照してください。

## タスク情報の確認

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // ジョブタグ
jobParams.put("TaskName", "task A");  // タスク名
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
パラメータの説明とエラーメッセージの詳細については、[タスク情報の確認APIドキュメント](https://cloud.tencent.com/document/product/599/12684)を参照してください。

## タスクインスタンスの終了

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // ジョブタグ
jobParams.put("TaskName", "taskA");  // タスク名
jobParams.put("TaskInstanceIndex", 0);  // タスク名
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
パラメータの説明とエラーメッセージの詳細については、[タスクインスタンスの終了APIドキュメント](https://cloud.tencent.com/document/product/599/12688)を参照してください。

