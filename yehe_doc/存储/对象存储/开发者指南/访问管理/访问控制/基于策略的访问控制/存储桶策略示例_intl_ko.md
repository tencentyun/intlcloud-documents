>버킷 정책을 추가할 때, 반드시 업무상 필요에 따라 최소 권한 원칙에 근거하여 권한을 부여해야 합니다. 다른 사용자에게 모든 리소스 `(resource:*)`, 또는 작업 `(action:*)`에 대한 모든 권한을 부여하면 권한 범위가 너무 광범위해 데이터 보안에 리스크가 발생할 수 있습니다.

## 개요
본 문서는 서브넷, 위탁자 및 VPC ID를 제한하는 버킷 정책 예시를 소개합니다. 해당 버킷 정책을 이용해 버킷 및 데이터의 특정 액세스를 제어할 수 있습니다. 액세스 정책 언어에 관한 자세한 내용은 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023)를 참조하십시오.
>
>- COS 콘솔을 이용해 버킷 정책을 설정할 때, 사용자에게 버킷 소유와 관련된 권한(예: 버킷 위치 얻기, 버킷 권한 나열)을 부여해야 합니다.
>- 버킷 정책의 크기는 20KB로 제한됩니다.


### 예시 1: 서브넷 10.1.1.0/24 IP 대역 및 vpcid의 aqp5jrc1에 대한 요청 제한
구문 예시는 다음과 같습니다.
```
{
  "Statement": [
    {
      "Action": [
        "name/cos:*"
      ],
      "Condition": {
        "ip_equal": {
          "qcs:ip": [
            "10.1.1.0/24"
          ]
        },
        "string_equal": {
          "vpc:requester_vpc": [
            "vpc-aqp5jrc1"
          ]
        }
      },
      "Effect": "deny",
      "Principal": {
        "qcs": [
          "qcs::cam::anyone:anyone"
        ]
      },
      "Resource": [
        "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}
```


### 예시 2: vpcid의 aqp5jrc1 및 특정 위탁자와 특정 버킷에 대한 요청 제한
구문 예시는 다음과 같습니다.
```
{
  "Statement": [
    {
      "Action": [
        "name/cos:*"
      ],
      "Condition": {
        "string_equal": {
          "vpc:requester_vpc": [
            "vpc-aqp5jrc1"
          ]
        }
      },
      "Effect": "allow",
      "Principal": {
        "qcs": [
          "qcs::cam::uin/100000000001:uin/100000000002"
        ]
      },
      "Resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}
```
