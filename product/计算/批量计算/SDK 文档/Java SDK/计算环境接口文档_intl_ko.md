## 개발 준비
- [Java SDK](https://cloud.tencent.com/document/sdk/Java)를 다운로드 및 설치합니다.
- 처음 Batch Compute을 사용할 경우, [시작 전 준비](https://cloud.tencent.com/document/product/599/10807)를 참조하십시오.
- 더 많은 컴퓨팅 환경 구성 매개변수를 알아보려면 [컴퓨팅 환경 생성 API 문서](https://cloud.tencent.com/document/product/599/12691)를 참조하십시오.

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

## 컴퓨팅 환경 생성

```
TreeMap<String, Object> envParams = new TreeMap<String, Object>();
envParams.put("ComputeEnv.EnvName", "batch-env");  // 컴퓨팅 환경 이름
envParams.put("ComputeEnv.EnvType", "MANAGED");
envParams.put("ComputeEnv.DesiredComputeNodeCount", 10);  // 예상 노드 수
envParams.put("ComputeEnv.EnvData.InstanceType", "S1.SMALL1");  // 인스턴스 유형
envParams.put("ComputeEnv.EnvData.ImageId", "img-er9shcln"); // 이미지 ID
envParams.put("ComputeEnv.EnvData.SystemDisk.DiskType", "LOCAL_BASIC");  // 시스템 디스크 유형
envParams.put("ComputeEnv.EnvData.SystemDisk.DiskSize", 50);  // 시스템 디스크 크기
envParams.put("ComputeEnv.EnvData.LoginSettings.Password", "B1[habcdB1[habcd");  // 로그인 비밀번호
envParams.put("Placement.Zone", "ap-guangzhou-2");  // 가용 영역
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
더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 생성 API 문서](https://cloud.tencent.com/document/product/599/12691)를 참조하십시오.

## 컴퓨팅 환경 수정

```
TreeMap<String, Object> envParams = new TreeMap<String, Object>();
envParams.put("EnvId", "env-cc44pzme");  // 컴퓨팅 환경 ID
envParams.put("DesiredComputeNodeCount", 100);  // 예상 노드 수
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
더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 수정 API 문서](https://cloud.tencent.com/document/product/599/13637)를 참조하십시오.
 
## 컴퓨팅 클러스터 삭제
 
```
TreeMap<String, Object> delParams = new TreeMap<String, Object>();
delParams.put("EnvId", "env-cc44pzme");  // 컴퓨팅 환경 ID
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
더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 삭제 API 문서](https://cloud.tencent.com/document/product/599/12692)를 참조하십시오.
 
## 컴퓨팅 환경 생성 정보 보기
 
```
TreeMap<String, Object> infoParams = new TreeMap<String, Object>();
infoParams.put("EnvId", "env-cc44pzme");  // 컴퓨팅 환경 ID
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
더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 생성 정보 보기 API 문서](https://cloud.tencent.com/document/product/599/14604)를 참조하십시오.
 
## 컴퓨팅 환경 정보 보기
 
```
TreeMap<String, Object> desParams = new TreeMap<String, Object>();
desParams.put("EnvId", "env-cc44pzme");  // 컴퓨팅 환경 ID
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
더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 정보 보기 API 문서](https://cloud.tencent.com/document/product/599/12694)를 참조하십시오.

## 컴퓨팅 환경 목록 보기

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
더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 목록 보기 API 문서](https://cloud.tencent.com/document/product/599/12695)를 참조하십시오.

