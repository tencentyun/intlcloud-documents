## 1. 간략 설명
Batch Compute 작업 구성은 JSON 형식으로 제공됩니다. 아래에 구성 간략 설명을 제공하였으며 아래 작업은 2개의 태스크를 포함합니다.

```
{
    "JobName": "TestJob",       // 작업 이름
    "JobDescription": "for test ",    // 작업 설명
    "Priority": "1",            // 작업 우선 순위
    "Tasks": [                  // 태스크 목록(본 예시에 2개 태스크 포함)
        {       
            // 태스크 1(가장 간소화된 태스크 구성으로 모든 비필수 옵션 제외) 
            "TaskName": "Task1",   // 태스크 1 이름
            "Application": {        // 태스크 실행 명령
                "DeliveryForm": "LOCAL",    // 애플리케이션 딜리버리 방식
                "Command": "echo hello"     // 명령 내용(hello 출력)
                
            },
            "ComputeEnv": {         // 컴퓨팅 환경 구성
                "EnvType": "MANAGED",   // 컴퓨팅 환경 유형, 관리 및 비관리
                "EnvData": {        // 구체적인 구성(현재 관리됨임. CVM 인스턴스 생성 설명 참조)
                    "InstanceType": "S1.SMALL1",    // CVM 인스턴스 유형
                    "ImageId": "img-m4q71qnf",      // CVM 이미지 ID
                }
            },
            "RedirectInfo": {       // 표준 출력 리디렉션 구성           
                "StdoutRedirectPath": "cos://dondonbatchv5- 1251783334.cosgz.myqcloud.com/logs/",  // 표준 출력(교체 필요)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"    // 표준 오류(교체 필요)
            },
            "Authentications": [        // 인증 관련 정보(옵션, 타인 COS 시나리오 접근에 사용)
                {
                    "Scene": "COS",     // 환경(현재는 COS)
                    "SecretId": "***",  // SecretId(교체 필요)
                    "SecretKey": "***"  // SecretKey(교체 필요)
                }
            ]
        },
        {
            // 태스크 2
            "TaskName": "Task2",   // 태스크 2 이름
            "TaskInstanceNum": 1,   // 태스크 2 동시 발생 인스턴스 수
            "Application": {        // 태스크 실행 명령
                "DeliveryForm": "LOCAL",    // 로컬 명령 실행
                "Command": "python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "   // 명령의 구체적인 내용(피보나치 수열 총합)
            },
            "ComputeEnv": {         // 컴퓨팅 환경 구성
                "EnvType": "MANAGED",   // 컴퓨팅 환경 유형, 관리 및 비관리
                "EnvData": {        // 구체적인 구성(현재 관리됨임. CVM 인스턴스 생성 설명 참조)
                    "InstanceType": "S1.SMALL1",    // CVM 인스턴스 유형
                    "ImageId": "img-m4q71qnf",      // CVM 이미지 ID(교체 가능)
                    "VirtualPrivateCloud": {        //CVM 네트워크 구성(옵션)
                        "VpcId": "vpc-cg18la4l",             // VpcId(교체 필요)
                        "SubnetId": "subnet-8axej2jc"           // SubnetId(교체 필요)
                    },
                    "SystemDisk": {                 //CVM 시스템 디스크 구성
                        "DiskType": "CLOUD_BASIC",
                        "DiskSize": 50
                    },
                    "DataDisks": [                  //CVM 데이터 디스크 구성
                        {
                            "DiskType": "CLOUD_BASIC",
                            "DiskSize": 50
                        }
                    ]
                }
            },
            "RedirectInfo": {       // 표준 출력 리디렉션 구성           
                "StdoutRedirectPath": "cos://dondonbatchv5- 1251783334.cosgz.myqcloud.com/logs/",  // 표준 출력(교체 필요)
                "StderrRedirectPath": "cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/"    // 표준 오류(교체 필요)
            },
            "MaxRetryCount": 1,         // 최대 다시 시도 수
            "Authentications": [        // 인증 관련 정보(옵션, 타인 COS 시나리오 접근에 사용)
                {
                    "Scene": "COS",     // 환경(현재는 COS)
                    "SecretId": "***",  // SecretId(교체 필요)
                    "SecretKey": "***"  // SecretKey(교체 필요)
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
## 2. 상세 설명

### I. 작업(Job)
작업은 Batch 제출 유닛으로 자체 정보 외에도 1개 또는 여러 개의 태스크(Task) 정보 및 Task 간의 의존 관계를 포함합니다.

이름 | 유형 | 필수 여부 | 설명  
-----|------|-----|------
JobName | String | 아니요 | 작업 이름
JobDescription | String | 아니요 | 작업 설명
Priority | Integer | 네 | 작업 우선순위로 태스크(Task)와 태스크 인스턴스(TaskInstance)는 작업과 같은 우선순위를 가집니다.
Tasks.N | array of Task objects | 네 | 태스크 정보
Dependences.N | array of Dependence objects | 아니요 |  의존 정보

### II. 태스크(Task)
1개의 작업은 여러 개의 태스크를 포함할 수 있으며, 태스크는 주로 배치 처리 데이터 컴퓨팅에서 실제 컴퓨팅 과정이 의존하는 환경(모델, 시스템, 이미지), 실행할 코드 패키지와 명령행, 저장, 네트워크 등 관련 정보를 설명합니다.

이름 | 유형 | 필수 여부 | 설명 | 예제
-----|------|-----|------|------
TaskName | String | 네 | 작업 내 유일한 태스크 이름 | Task1
TaskInstanceNum | Integer | 네 | 태스크 인스턴스 실행 개수 | 1
Application | Application object | 네 | 애플리케이션 정보 | 
ComputeEnv  | ComputeEnv object | 네 | 실행 환경 정보 |
RedirectInfo | RedirectInfo object | 네 | 리디렉션 경로 |
InputMappings | array of InputMapping object | 아니요 | 입력 매핑 |
OutputMappings | array of OutputMapping object | 아니요 | 출력 매핑 |
Authentications | array of Authentication object | 아니요 | 라이센싱 정보 |
MaxRetryCount | Integer | 아니요 | 태스크 실패 후 최대 다시 시도 횟수 | 3
Timeout | Integer | 아니요 | 태스크 시작 후 초 단위의 타임아웃 시간 | 3600

#### Application
이름 | 유형 | 필수 여부 | 설명 | 예제
-----|------|-----|------|------
Command | String | 네 | 작업 실행 명령
DeliveryForm | String | 네 | 애플리케이션 딜리버리 방식 | LOCAL 로컬, PACKAGE 원격 코드 패키지
PackagePath | String | 아니요 | 원격 코드 패키지 경로, 반드시 .tgz 형식이어야 함 | ```http://batchdemo-1251783334.cosgz.myqcloud.com/codepkg/codepkg.tgz```(PACKAGE 방식만 가능)

#### ComputeEnv
이름 | 유형 | 필수 여부 | 설명 | 예제
-----|------|-----|------|------
EnvType | String | 네 | 컴퓨팅 환경 관리 유형으로 관리와 비관리 두 가지를 포함 | LOCAL 로컬, PACKAGE 원격 코드 패키지
EnvData | EnvData object | 네 | 컴퓨팅 환경 구체적인 매개변수 |

#### EnvData
이름 | 유형 | 필수 여부 | 설명 | 예제
-----|------|-----|------|------
InstanceType | String | 네 | CVM 인스턴스 유형, 관리 유형은 반드시 입력해야 함 | img-m4q71qnf
ImageId | String | 네 | CVM 이미지 ID, 호스팅 유형은 반드시 입력해야 함 | S1.SMALL1
others | others | 아니요 | CVM API 문서 [인스턴스 생성](https://cloud.tencent.com/document/api/213/9384)에서 제공한 매개변수 참조 | SystemDisk, DataDisks, VirtualPrivateCloud 등 지원

#### RedirectInfo
이름 | 유형 | 필수 여부 | 설명 | 예제
-----|------|-----|------|------
StdoutRedirectPath | String | 아니요 | 표준 출력 리디렉션 경로 | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/
StderrRedirectPath | String | 아니요 | 표준 오류 리디렉션 경로 | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/logs/

#### InputMapping
이름 | 유형 | 필수 여부 | 설명 | 예제
-----|------|-----|------|------|------
SourcePath | String | 네 | 소스 경로 | 	cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/input/
DestinationPath | String | 네 | 대상 경로 | /data/input/

#### OutputMapping
이름 | 유형 | 필수 여부 | 설명 | 예제 
-----|------|-----|------|------|------
SourcePath | String | 네 | 소스 경로 | /data/output/
DestinationPath | String | 네 | 대상 경로 | cos://dondonbatchv5-1251783334.cosgz.myqcloud.com/output/

#### Authentication 
입력한 COS 경로(저장 매핑, 로그 리디렉션)가 본인 COS 주소인 경우, 입력할 필요가 없습니다. 다른 사람의 COS에 접근해야 할 경우, 해당 접근 키를 입력해야 합니다.

이름 | 유형 | 필수 여부 | 설명  
-----|------|-----|------
Scene | String | 네 | 라이센싱 시나리오, 예: COS
SecretId | String | 네 | SecretId
SecretKey | String | 네 | SecretKey 

### III. 태스크 의존 관계(Dependence)
태스크 간의 선후 관계를 설명합니다. 예를 들어 작업은 2개의 태스크를 포함하는 경우 StartTask는 Task1, EndTask는 Task2이면 Task1 실행을 완료해야만 Task2가 시작되고 Task2 실행을 완료해야 작업 실행이 완료됩니다.

이름 | 유형 | 필수 여부 | 설명 | 예제
-----|------|-----|------|------
StartTask | String | 네 | 의존 관계의 시작 태스크 이름 | Task1
EndTask | String | 네 | 의존 관계의 종료 태스크 이름 | Task2


