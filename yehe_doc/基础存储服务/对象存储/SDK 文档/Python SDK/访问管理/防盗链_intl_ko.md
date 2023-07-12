## 소개

본문은 버킷 Referer 에 대한 얼로우/블록리스트의 API 개요 및 SDK 예시 코드를 제공합니다.

>! COS PYTHON SDK v5.1.9.7 이상의 버전이 필요합니다.
>

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 버킷 Referer 설정 | 버킷 Referer 얼로우 또는 블록리스트 설정 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 버킷 Referer 쿼리 | 버킷 Referer 얼로우 또는 블록리스트 쿼리 |

## 버킷 Referer 설정

#### 기능 설명

지정된 버킷의 Referer의 얼로우 또는 블록리스트를 설정합니다(PUT Bucket referer).

#### 메소드 프로토타입

```python
put_bucket_referer(Bucket, RefererConfiguration, **kwargs)
```

#### 요청 예시

```python
# secret_id, secret_key, region 등을 포함한 사용자 속성을 설정합니다. Appid는 CosConfig에서 제거되었습니다. 매개변수 Bucket에 Appid를 포함시키십시오. Bucket은 BucketName-Appid로 구성됩니다.
secret_id = 'SecretId'     # 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
secret_key ='SecretKey'   # 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
                           # COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
token = None               # 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  
client = CosS3Client(config)
referer_config = {
    'Status': 'Enabled',
    'RefererType': 'White-List',
    'EmptyReferConfiguration': 'Allow',
    'DomainList': {
        'Domain': [
            '*.qq.com',
            '*.qcloud.com'
        ]
    }
}
response = client.put_bucket_referer(
    Bucket='examplebucket-1250000000',
    RefererConfiguration=referer_config
)
```

#### 매개변수 설명

| 매개변수 이름                                   | 매개변수 설명                                                     | 유형                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName                               | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String                                   |
| RefererConfiguration | 버킷 Referer 설정                                               | Dict |

RefererConfiguration 설명:

| 매개변수 이름          | 매개변수 설명                                         | 유형    | 필수 입력 여부 |
| -------------- | ----------------------------------------------- | ------ | ---- |
| Status         | 링크 도용 방지 활성화 여부. 열거 값: Enabled、Disabled           | String | 필수   |
| RefererType    | 링크 도용 방지 유형. 열거 값: Black-List, White-List          | String | 필수   |
| DomainList         | 유효한 도메인 목록                                 | Dict | 필수   |
| Domain         | 유효한 도메인. 포트 및 IP 지원, 와일드카드\* 지원, 다중 지원        | List | 필수   |
| EmptyReferConfiguration | 빈 Refer 액세스 허용 여부. 열거 값: Allow、Deny | String | 옵션  |

#### 반환 결과 설명
해당 메소드의 반환값은 None입니다.

## 버킷 Referer 쿼리

#### 기능 설명

지정된 버킷의 Referer의 얼로우 또는 블록리스트를 쿼리합니다(GET Bucket referer).

#### 메소드 프로토타입

```python
get_bucket_referer(Bucket, **kwargs)
```

#### 요청 예시

```python
response = client.get_bucket_referer(
    Bucket='examplebucket-1250000000'
)
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명  | 유형  |
| ----------- | -------- | ---- |
| bucketName  | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String                                   |

#### 반환 결과 설명
버킷의 Referer 설정을 반환합니다. RefererConfiguration 설명을 참고하십시오.

## 버킷 Referer 삭제

#### 기능 설명

지정된 버킷의 Referer의 얼로우 또는 블록리스트를 삭제합니다(DELETE Bucket referer).

#### 메소드 프로토타입

```python
delete_bucket_referer(Bucket, **kwargs)
```

#### 요청 예시

```python
response = client.delete_bucket_referer(
    Bucket='examplebucket-1250000000'
)
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명  | 유형  |
| ----------- | -------- | ---- |
| bucketName  | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String                                   |

#### 반환 결과 설명
해당 메소드의 반환값은 None입니다.
