## 개발 준비
- [Java SDK](https://cloud.tencent.com/document/sdk/Java)를 다운로드 및 설치합니다.
- 처음 Batch Compute을 사용할 경우, [시작 전 준비](https://cloud.tencent.com/document/product/599/10807)를 참조하십시오.
- 더 많은 작업 구성 매개변수를 알아보려면 [작업 제출 API 문서](https://cloud.tencent.com/document/product/599/12683)를 참조하십시오.

## 시작 가이드

```
import java.util.TreeMap;

import com.qcloud.QcloudApiModuleCenter;
import com.qcloud.Module.Batch;
import com.qcloud.Utilities.Json.JSONObject;

public class BatchDemo {
        public static void main(String[] args) {
                TreeMap<String, Object> config = new TreeMap<String, Object>();
                config.put("SecretId", "나의 SecretId");
                config.put("SecretKey", "나의 SecretKey");
                config.put("RequestMethod", "GET");
                config.put("DefaultRegion", "gz"); // 지역, gz: guangzhou

                QcloudApiModuleCenter module = new QcloudApiModuleCenter(new Batch(), config);
        }
}
```

## 작업 제출

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();            
jobParams.put("Job.JobName", "batch-job");  // 작업 이름
jobParams.put("Job.JobDescription", "demo job");  // 작업 설명
jobParams.put("Job.Priority", 1);  // 작업 우선 순위
jobParams.put("Job.Tasks.0.TaskName", "taskA");  // 태스크 이름
jobParams.put("Job.Tasks.0.TaskInstanceNum", 10);  // 태스크 인스턴스 동시 발생 수
jobParams.put("Job.Tasks.0.Application.DeliveryForm", "LOCAL");  // 프로그램 패키지 출처
jobParams.put("Job.Tasks.0.Application.Command", "echo 'hello'");  // 명령행
jobParams.put("Job.Tasks.0.EnvId", "env-gbyctcy9");  // 컴퓨팅 환경 ID
jobParams.put("Job.Tasks.0.RedirectInfo.StdoutRedirectPath", "cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stdout/");  // 표준 출력 주소
jobParams.put("Job.Tasks.0.RedirectInfo.StderrRedirectPath", "cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stderr/");  // 표준 오류 주소
jobParams.put("Placement.Zone", "ap-guangzhou-2"); // 가용 영역
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
더 많은 매개변수 설명 및 오류 정보는 [작업 제출 API 문서](https://cloud.tencent.com/document/product/599/12683)를 참조하십시오.

## 작업 종료

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 작업 ID
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
더 많은 매개변수 설명 및 오류 정보는 [작업 종료 API 문서](https://cloud.tencent.com/document/product/599/12689)를 참조하십시오.

## 작업 삭제

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 작업 ID
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
더 많은 매개변수 설명 및 오류 정보는 [작업 삭제 API 문서](https://cloud.tencent.com/document/product/599/12682)를 참조하십시오.

## 작업의 제출 정보 보기

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 작업 ID
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
더 많은 매개변수 설명 및 오류 정보는 [작업의 제출 정보 보기 API 문서](https://cloud.tencent.com/document/product/599/12687)를 참조하십시오.

## 작업 정보 보기

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 작업 ID
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
더 많은 매개변수 설명 및 오류 정보는 [작업 정보 보기 API 문서](https://cloud.tencent.com/document/product/599/12685)를 참조하십시오.

## 작업 목록 보기

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
더 많은 매개변수 설명 및 오류 정보는 [작업 목록 보기 API 문서](https://cloud.tencent.com/document/product/599/12686)를 참조하십시오.

## 태스크 정보 보기

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 작업 ID
jobParams.put("TaskName", "task A");  // 태스크 이름
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
더 많은 매개변수 설명 및 오류 정보는 [태스크 정보 보기 API 문서](https://cloud.tencent.com/document/product/599/12684)를 참조하십시오.

## 태스크 인스턴스 종료

```
TreeMap<String, Object> jobParams = new TreeMap<String, Object>();
jobParams.put("JobId", "job-8kwnzki7");  // 작업 ID
jobParams.put("TaskName", "taskA");  // 태스크 이름
jobParams.put("TaskInstanceIndex", 0);  // 태스크 이름
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
더 많은 매개변수 설명 및 오류 정보는 [태스크 인스턴스 종료 API 문서](https://cloud.tencent.com/document/product/599/12688)를 참조하십시오.

