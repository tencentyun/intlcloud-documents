## 소개

본문은 버킷 Referer 에 대한 화이트/블랙리스트의 API 개요 및 SDK 예시 코드를 제공합니다.

>! COS PYTHON SDK v5.1.9.7 및 이후의 버전이 필요합니다.
>

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 버킷 Referer 설정 | 버킷 Referer 화이트 또는 블랙리스트 설정 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 버킷 Referer 쿼리| 버킷 Referer 화이트 또는 블랙리스트 쿼리 |

## 버킷 Referer 설정

#### 기능 설명

버킷의 Referer의 화이트 또는 블랙리스트를 설정합니다(PUT Bucket referer).

#### 메소드 프로토타입

```python
put_bucket_referer(Bucket, RefererConfiguration, **kwargs)
```

#### 요청 예시

```python
# secret_id, secret_key, region를 포함한 사용자 속성을 설정합니다. secret_id와 secret_key는 CAM 콘솔에 로그인하여 조회 및 관리하십시오.
# APPID는 설정에서 삭제되었으니 매개변수 Bucket에 APPID를 입력하십시오. Bucket은 BucketName-APPID로 구성됩니다.
secret_id = 'secret_id'     # 사용자 secret_id로 변경
secret_key = 'secret_key'     # 사용자 secret_key로 변경
region = 'ap-beijing'    # 사용자 region으로 변경
token = None               # 임시 키를 사용할 경우 Token 입력. 기본값이 null이면 입력하지 않음
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

| 매개변수 이름                 | 매개변수 설명                                                     | 유형             | 필수 입력 여부 |
| -------------- | ----------------------------------------------- | ------ | ---- |
| Status         | 링크 도용 방지 활성화 여부, 열거 값: Enabled, Disabled           | String | 필수   |
| RefererType    | 링크 도용 방지 유형 열거 값: Black-List, White-List          | String | 필수   |
| DomainList         | 적용 도메인 리스트                                 | Dict | 필수   |
| Domain         | 적용 도메인. 포트, IP, 와일드 카드\* 지원, 복수 지원.        | List | 필수   |
| EmptyReferConfiguration | 빈 Refer 액세스 허용 여부, 열거 값: Allow, Deny | String | 옵션  |

#### 반환 결과 설명
해당 메소드의 반환값은 None입니다.

## 버킷 Referer 쿼리

#### 기능 설명

버킷의 Referer의 화이트 또는 블랙리스트를 쿼리합니다(PUT Bucket referer).

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
버킷의 Referer 설정 반환으로 RefererConfiguration 설명을 참고하십시오.

## 버킷 Referer 삭제

#### 기능 설명

버킷 Referer의 화이트리스트 또는 블랙리스트를 삭제합니다(DELETE Bucket referer).

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
