## 적용 시나리오

수명 주기 설정으로 규칙에 부합하는 객체를 지정한 조건에 자동으로 일부 조작을 진행시킬수 있습니다.

- 스토리지 클래스 전환: 생성한 객체를 지정한 시간 후에 저빈도 스토리지 클래스 STANDARD_IA 또는 보관 스토리지 클래스 ARCHIVE로 전환합니다.
- 만료 삭제: 객체의 만료 시간을 설정하여 객체가 만료된 후 자동으로 삭제되도록 합니다.

수명 주기 기능의 [기본 설명 문서](/document/product/436/17028)를 참조하십시오. 설정 시 [구성 요소](/document/product/436/17029)를 지정해야 합니다.

## 사용 방법
### COS 콘솔 사용
COS 콘솔로 수명 주기를 설정하는 것과 관련된 사항은 [수명 주기 관리](https://cloud.tencent.com/document/product/436/14605) 콘솔 가이드 문서를 참조하십시오.

### REST API 사용

REST API로 버킷 중의 객체 수명 주기를 구성 및 관리할 수 있습니다. 아래 API 문서 부분을 참조하십시오.

- [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280)
- [GET Buket lifecycle](https://cloud.tencent.com/document/product/436/8278)
- [DELETE Bucket lifecycle](https://cloud.tencent.com/document/product/436/8284)

### C++ SDK 사용

COS의 C++ SDK에서 이 방법을 제공하며 C++ SDK API 문서 [ 버킷 수명 주기 설정 부분](https://cloud.tencent.com/document/product/436/12302#put-bucket-lifecycle)을 참조하십시오.

절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. putBucketLifecycle와 GetBucketLifecycle를 실행하여 버킷 수명 주기와 인덱스 수명 주기를 별도로 설정합니다.

### 수명 주기 설정

예제 코드:

```
cloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// PutBucketLifecycleReq 의 구조 함수에 bucket_name을 입력해야 합니다
qcloud_cos::PutBucketLifecycleReq req(bucket_name);
qcloud_cos::PutBucketLifecycleResp resp;

// 규칙 설정
{
    qcloud_cos::LifecycleRule rule;
    rule.SetIsEnable(true);
    rule.SetId("lifecycle_rule00");

    // Filter를 설정하고 태그 키 datalevel과 값 backup의 태그를 가진 객체에 적용합니다
    qcloud_cos::LifecycleFilter filter;
    Lifecycle tag;
    tag.key = "datalevel";
    tag.value = "backup";
    filter.AddTag(tag);
    rule.SetFilter(filter);

    // 객체는 생성된 30일 후에 STANDARD_IA로 전환되도록 합니다
    qcloud_cos::LifecycleTransition transition1;
    transition1.SetDays(30);
    transition1.SetStorageClass("STANDARD_IA");
    rule.AddTransition(transition1);

    // 객체는 생성된 365일 후에 ARCHIVE 스토리지 유형으로 전환되도록 합니다
    qcloud_cos::LifecycleTransition transition2;
    transition2.SetDays(365);
    transition2.SetStorageClass("ARCHIVE");
    rule.AddTransition(transition2);

    req.AddRule(rule);
}

qcloud_cos::CosResult result = cos.PutBucketLifecycle(req, &resp);
// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 수명 주기 설정에 실패하였습니다. CosResult의 멤버 함수를 호출하여 requestID와 같은 오류 정보를 출력할 수 있습니다.
}
```

#### 수명 주기 검색
예제 코드:

```
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// GetBucketLifecycleReq의 구조 함수에 bucket_name을 입력해야 합니다
qcloud_cos::GetBucketLifecycleReq req(bucket_name);
qcloud_cos::GetBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.GetBucketLifecycle(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 수명 주기 구성 획득에 실패할 경우 CosResult의 멤버 함수를 호출하여 오류 정보(예: requestID 등)를 출력할 수 있습니다
}
```

### Python SDK 사용
COS의 Python SDK에서 이 방법을 제공하며 Python SDK API 문서 [버킷 수명 주기 구성 설정 부분](https://cloud.tencent.com/document/product/436/12270#.E8.AE.BE.E7.BD.AE-bucket-.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F.E9.85.8D.E7.BD.AE)을 참조하십시오.
### 수명 주기 설정
절차 설명

1. CosConfig 클래스로 구성하고 클라이언트 CosS3Client를 초기화합니다.
2. put_bucket_lifecycle() 방법을 실행여 버킷에 수명 주기 구성을 설정합니다.

수명 주기 설정의 예제 코드는 다음과 같습니다.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'       # 사용자의 SecretId로 대체합니다.
secret_key = 'xxxxxxx'      # 사용자의 secretKey로 대체합니다.
region = 'ap-beijing-1'     # 사용자의 지역으로 대체합니다.
token = ''                  # 임시 키를 사용하려면 Token이 전송되어야 합니다. 기본적으로 비어 있으며 입력하지 않아도 됩니다.

config = CosConfig(Access_id=secret_id, Access_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
lifecycle_config = {
    'Rule': [
        {
            'Status': 'Enabled',
            'Filter': {
                태그 키 datalevel과 값 backup의 태그를 가진 객체에 적용합니다
                'Tag': [
                    {
                        'Key': 'datalevel',
                        'Value': 'backup'
                    }
                ]
            },
            'Transition': [
                {
                    # 30일 후 Standard_IA로 전환합니다
                    'Days': 30,
                    'StorageClass': 'Standard_IA'
                },
                {
                    # 365일 후 Archive로 전환합니다
                    'Days': 365,
                    'StorageClass': 'Archive'
                }
            ],
            'Expiration': {
                # 3650일 후 만료되어 삭제됩니다
                'Days': 3650
            }
        }
    ]
}

response = client.put_bucket_lifecycle(
    Bucket=bucket,
    LifecycleConfiguration=lifecycle_config
)
```

#### 수명 주기 획득
절차 설명:

1. CosConfig 클래스를 사용하여 클라이언트 CosS3Client를 구성하고 초기화합니다.
2. get_bucket_lifecycle() 방법을 실행여 버킷에 수명 주기 구성을 획득합니다.

수명 주기 획득의 예제 코드는 다음과 같습니다

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # 사용자의 secretKey로 대체합니다.
secret_key = 'xxxxxxx'      # 사용자의 secretKey로 대체합니다.
region = 'ap-beijing-1'     # 사용자의 지역으로 대체합니다.
token = ''                  # 임시 키를 사용하려면 Token이 전송되어야 합니다. 기본적으로 비어 있으며 입력하지 않아도 됩니다.

config = CosConfig(Access_id=secret_id, Access_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
response = client.get_bucket_lifecycle(
    Bucket=bucket    
)
```

### PHP SDK 사용
COS의 PHP SDK에서 이 방법을 제공하며 PHP SDK API 문서 [ 수명 주기 설정](https://cloud.tencent.com/document/product/436/12267#putbucketlifecycle)을 참조하십시오.

### 수명 주기 설정
절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. putBucketLifecycle를 실행하여 버킷 수명 주기를 설정합니다.

아래 코드는 버킷 수명 주기의 설정 절차를 보여줍니다.

```php
## putBucketLifecycle(버킷 수명 주기 설정)
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv('COS_KEY'),
        'secretKey' => getenv('COS_SECRET'))));

//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
$bucket = 'lewzylu02-1252448703';

try {
    $result = $cosClient->putBucketLifecycle(array(
        'Bucket' => $bucket,
        'Rules' => array(
            array(
                'Status' => 'Enabled',
                'Filter' => array(
                    'Tag' => array(
                        'Key' => 'datalevel',
                        'Value' => 'backup'
                    )
                ),
                'Transitions' => array(
                   array(
                    # 30일 후 Standard_IA로 전환합니다
                    'Days' => 30,
                    'StorageClass' => 'Standard_IA'),
                array(
                    # 365일 후 Archive로 전환합니다
                    'Days' => 365,
                    'StorageClass' => 'Archive')
                ),
                'Expiration' => array(
                # 3650일 후 만료되어 삭제됩니다
                'Days' => 3650,
                )
            )
        )
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 수명 주기 획득
절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. getBucketLifecycle를 실행하여 버킷 수명 주기 정보를 획득합니다.

아래 코드는 버킷 수명 주기의 획득 절차를 보여줍니다.

```php
## getBucketLifecycle(버킷 수명 주기 획득)
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv('COS_KEY'),
        'secretKey' => getenv('COS_SECRET'))));

//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
$bucket = 'lewzylu02-1252448703';

try {
    $result = $cosClient->getBucketLifecycle(array(
        'Bucket' =>$bucket,
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 수명 주기 삭제
절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. deleteBucketLifecycle를 실행하여 버킷 수명 주기를 삭제합니다.

아래 코드는 버킷 수명 주기의 삭제 절차를 보여줍니다.

```php
## deleteBucketLifecycle(버킷 수명 주기 삭제)
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv('COS_KEY'),
        'secretKey' => getenv('COS_SECRET'))));

//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
$bucket = 'lewzylu02-1252448703';

try {
    $result = $cosClient->deleteBucketLifecycle(array(
        'Bucket' =>$bucket,
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
