## 開発準備
- [Java SDK](https://cloud.tencent.com/document/sdk/Java)をダウンロードしてインストールします。
- 初めてBatchを使用する場合は、[始める前の準備](https://cloud.tencent.com/document/product/599/10807)を参照してください。
- 計算環境構成パラメータの詳細については、[計算環境の作成APIドキュメント](https://cloud.tencent.com/document/product/599/12691)を参照してください。

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

## 計算環境の作成

```
TreeMap<String, Object> envParams = new TreeMap<String, Object>();
envParams.put("ComputeEnv.EnvName", "batch-env");  //　計算環境名
envParams.put("ComputeEnv.EnvType", "MANAGED");
envParams.put("ComputeEnv.DesiredComputeNodeCount", 10);  // 目標ノード数
envParams.put("ComputeEnv.EnvData.InstanceType", "S1.SMALL1");  // インスタンスタイプ
envParams.put("ComputeEnv.EnvData.ImageId", "img-er9shcln"); // イメージタグ
envParams.put("ComputeEnv.EnvData.SystemDisk.DiskType", "LOCAL_BASIC");  // システムディスクのタイプ
envParams.put("ComputeEnv.EnvData.SystemDisk.DiskSize", 50);  // システムディスクのサイズ
envParams.put("ComputeEnv.EnvData.LoginSettings.Password", "B1[habcdB1[habcd");  // ログインパスワード
envParams.put("Placement.Zone", "ap-guangzhou-2");  // Availability Zone
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
パラメータの説明とエラーメッセージの詳細については、[計算環境の作成APIドキュメント](https://cloud.tencent.com/document/product/599/12691)を参照してください。

## 計算環境の変更

```
TreeMap<String, Object> envParams = new TreeMap<String, Object>();
envParams.put("EnvId", "env-cc44pzme");  // 計算環境タグ
envParams.put("DesiredComputeNodeCount", 100);  // 目標ノード数
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
パラメータの説明とエラーメッセージの詳細については、[計算環境の変更APIドキュメント](https://cloud.tencent.com/document/product/599/13637)を参照してください。
 
## 計算クラスタの削除
 
```
TreeMap<String, Object> delParams = new TreeMap<String, Object>();
delParams.put("EnvId", "env-cc44pzme");  // 計算環境タグ
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
パラメータの説明とエラーメッセージの詳細については、[計算環境の削除APIドキュメント](https://cloud.tencent.com/document/product/599/12692)を参照してください。
 
## 計算環境作成情報の確認
 
```
TreeMap<String, Object> infoParams = new TreeMap<String, Object>();
infoParams.put("EnvId", "env-cc44pzme");  // 計算環境タグ
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
パラメータの説明とエラーメッセージの詳細については、[計算環境作成情報の確認APIドキュメント](https://cloud.tencent.com/document/product/599/14604)を参照してください。
 
## 計算環境情報の確認
 
```
TreeMap<String, Object> desParams = new TreeMap<String, Object>();
desParams.put("EnvId", "env-cc44pzme");  // 計算環境タグ
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
パラメータの説明とエラーメッセージの詳細については、[計算環境情報の確認APIドキュメント](https://cloud.tencent.com/document/product/599/12694)を参照してください。

## 計算環境リストの確認

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
パラメータの説明とエラーメッセージの詳細については、[計算環境リストの確認APIドキュメント](https://cloud.tencent.com/document/product/599/12695)を参照してください。

