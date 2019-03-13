## 1.簡単な説明
Batchのジョブ構成はJSONフォーマットで提供されます。この構成の簡単な説明を以下に示します。次のジョブには2つのタスクが含まれています。

```
{
    "JobName": "TestJob",       // ジョブ名
    "JobDescription": "for test ",    // ジョブの説明
    "Priority": "1",            // ジョブの優先順位
    "Tasks": [                  // タスクリスト（この例には2つのタスクが含まれています）
        {       
            // タスク1（最も単純化されたタスク構成、重要ではないオプションをすべて削除） 
            "TaskName": "Task1",   // タスク1の名前
            "Application": {        // タスク実行コマンド
                "DeliveryForm": "LOCAL",    // アプリケーションの納品方法
                "Command": "echo hello"     // コマンドの具体的な内容（helloの出力）
                
            },
            "ComputeEnv": {         // 計算環境構成
                "EnvType": "MANAGED",   // 計算環境のタイプ、ホスト型および非ホスト型
                "EnvData": {        // 具体的な構成（現在はホスト型で、CVMインスタンス作成の説明を参照してください）
                    "InstanceType": "S1.SMALL1",    // CVMインスタンスタイプ
                    "ImageId": "img-m4q71qnf",      // CVMイメージID
                }
            },
            "RedirectInfo": {       // 標準出力リダイレクト構成           
                "StdoutRedirectPath": "cos://dondonbatchv5- 1251783334.cosgz.myqcloud.com/logs/",  // 標準出力（置き換える必要あり）
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"    // 標準エラー（置き換える必要あり）
            },
            "Authentications": [        // 認証関連情報（オプション、本人以外のCOSへのアクセスシナリオに使用）
                {
                    "Scene": "COS",     // シナリオ（現在はCOS）
                    "SecretId": "***",  // SecretId（置き換える必要あり）
                    "SecretKey": "***"  // SecretKey（置き換える必要あり）
                }
            ]
        },
        {
            // タスク2
            "TaskName": "Task2",   // タスク2の名前
            "TaskInstanceNum": 1,   // タスク2同時実行インスタンス数
            "Application": {        // タスク実行コマンド
                "DeliveryForm": "LOCAL",    // ローカルコマンドの実行
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // コマンドの具体的な内容（フィボナッチ合計）
            },
            "ComputeEnv": {         // 計算環境構成
                "EnvType": "MANAGED",   // 計算環境のタイプ、ホスト型および非ホスト型
                "EnvData": {        // 具体的な構成（現在はホスト型で、CVMインスタンス作成の説明を参照してください）
                    "InstanceType": "S1.SMALL1",    // CVMインスタンスタイプ
                    "ImageId": "img-m4q71qnf",      // CVMイメージID（置き換え可能）
                    "VirtualPrivateCloud": {        //CVMネットワーク構成（オプション）
                        "VpcId": "vpc-cg18la4l",             // VpcId（置き換える必要あり）
                        "SubnetId": "subnet-8axej2jc"           // SubnetId（置き換える必要あり）
                    },
                    "SystemDisk": {                 //CVMシステムディスク構成
                        "DiskType": "CLOUD_BASIC",
                        "DiskSize": 50
                    },
                    "DataDisks": [                  //CVMデータディスク構成
                        {
                            "DiskType": "CLOUD_BASIC",
                            "DiskSize": 50
                        }
                    ]
                }
            },
            "RedirectInfo": {       // 標準出力リダイレクト構成           
                "StdoutRedirectPath": "cos://dondonbatchv5- 1251783334.cosgz.myqcloud.com/logs/",  // 標準出力（置き換える必要あり）
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"    // 標準エラー（置き換える必要あり）
            },
            "MaxRetryCount": 1,         // 最大再試行回数
            "Authentications": [        // 認証関連情報（オプション、本人以外のCOSへのアクセスシナリオに使用）
                {
                    "Scene": "COS",     // シナリオ（現在はCOS）
                    "SecretId": "***",  // SecretId（置き換える必要あり）
                    "SecretKey": "***"  // SecretKey（置き換える必要あり）
                }
            ]
        }
    ],
    "Dependences": [
        {
            "StartTask": "Task1", 
            "EndTask": "Task2"
        }
    ]
}
```
## 2.詳細な説明

### I. ジョブ（Job）
ジョブは、Batchによって提出された単位であり、自体の情報に加えて、1つ以上のタスク（Task）情報およびTask間の依頼関係も含まれています

名前 | タイプ  | 必須項目 | 説明  
-----|------|-----|------
JobName | String | いいえ | ジョブ名
JobDescription | String | いいえ | ジョブの説明
Priority | Integer | はい | ジョブ優先度、タスク（Task）、タスクインスタンス（TaskInstance）はジョブの優先度を引き継ぎます
Tasks.N | array of Task objects | はい | タスク情報
Dependences.N | array of Dependence objects | いいえ |  依頼情報

### II. タスク（Task）
1つのジョブには複数のタスクを含めることができ、タスクは主にバッチデータ計算中、実際の計算プロセスが依存する環境（モデル、システム、イメージ）、実行されるコードパッケージとコマンドライン、ストレージ、ネットワークなどの関連情報を説明します。

名前 | タイプ  | 必須項目 | 説明 | 例
-----|------|-----|------|------
TaskName | String | はい | ジョブ内で唯一のタスク名 | Task1
TaskInstanceNum | Integer | はい | タスクインスタンスの実行数 | 1
Application | Application object | はい | アプリケーション情報 | 
ComputeEnv  | ComputeEnv object | はい | 実行環境情報 |
RedirectInfo | RedirectInfo object | はい | リダイレクトパス |
InputMappings | array of InputMapping object | いいえ | 入力マッピング |
OutputMappings | array of OutputMapping object | いいえ | 出力マッピング |
Authentications | array of Authentication object | いいえ | 認証情報 |
MaxRetryCount | Integer | いいえ | タスクが失敗した後の最大再試行回数 | 3
Timeout | Integer | いいえ | タスク開始後のタイムアウト時時、単位は秒です | 3600

#### Application
名前 | タイプ  | 必須項目 | 説明 | 例
-----|------|-----|------|------
Command | String | はい | タスク実行コマンド
DeliveryForm | String | はい | アプリケーションの納品方法 | LOCAL ローカル、PACKAGE リモートコードパッケージ
PackagePath | String | いいえ | リモートコードパッケージパス、.tgzフォーマットでなければなりません | ```http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz``` （PACKAGE方式のみ）

#### ComputeEnv
名前 | タイプ  | 必須項目 | 説明 | 例
-----|------|-----|------|------
EnvType | String | はい | 計算環境管理タイプ、ホスト型と非ホスト型の両方が含まれます | LOCAL ローカル、PACKAGE リモートコードパッケージ）
EnvData | EnvData object | はい | 計算環境の具体的なパラメータ |

#### EnvData
名前 | タイプ  | 必須項目 | 説明 | 例
-----|------|-----|------|------
InstanceType | String | はい | CVMインスタンスタイプ、ホスト型が必要 | img-m4q71qnf
ImageId | String | はい | CVMイメージID、ホスト型が必要 | S1.SMALL1
others | others | いいえ | CVM APIドキュメント[インスタンスの作成](https://cloud.tencent.com/document/api/213/9384)で提供されているパラメータを参照してください | SystemDisk、DataDisks、VirtualPrivateCloudなどをサポートします

#### RedirectInfo
名前 | タイプ  | 必須項目 | 説明 | 例
-----|------|-----|------|------
StdoutRedirectPath | String | いいえ | 標準出力リダイレクトパス | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/
StderrRedirectPath | String | いいえ | 標準エラーリダイレクトパス | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/

#### InputMapping
名前 | タイプ  | 必須項目 | 説明 | 例
-----|------|-----|------|------|------
SourcePath | String | はい | ソースパス | 	cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/input/
DestinationPath | String | はい | ターゲットパス | /data/input/

#### OutputMapping
名前 | タイプ  | 必須項目 | 説明 | 例 
-----|------|-----|------|------|------
SourcePath | String | はい | ソースパス | /data/output/
DestinationPath | String | はい | ターゲットパス | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/output/

#### Authentication 
入力されたCOSパス（ストレージマッピング、ログリダイレクト）が本人のCOSアドレスである場合は、入力する必要はありません。他の人のCOSにアクセスする必要があるときは、対応するアクセス暗号鍵を記入する必要があります。

名前 | タイプ  | 必須項目 | 説明  
-----|------|-----|------
Scene | String | はい | COSなどの認証シナリオ
SecretId | String | はい | SecretId
SecretKey | String | はい | SecretKey 

### III. タスク依頼（Dependence）
タスク間の前後関係を説明します。例えば、ジョブに2つのタスクが含まれている場合、StartTaskはTask1、EndTaskはTask2、Task2はTask1が実行された後に開始され、Task2が実行された後、ジョブの実行が完了します。

名前 | タイプ  | 必須項目 | 説明 | 例
-----|------|-----|------|------
StartTask | String | はい | 依存関係の開始タスク名 | Task1
EndTask | String | はい | 依存関係の終了タスク名 | Task2


