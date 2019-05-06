## 개요
본문에서는 서브넷, 대리인과 VPC ID를 제한하는 버킷 정책 예시를 소개합니다. 이 버킷 정책을 사용하여 버킷 및 해당 데이터에 대한 지정 접근을 제어할 수 있습니다. 관련 접근 정책 언어에 대한 더 많은 정보는 [접근 정책 언어 개요](https://cloud.tencent.com/document/product/436/18023)를 참조하십시오.
>!
>- COS 콘솔을 사용하여 버킷 정책을 구성할 때, 버킷 위치 획득 및 버킷 권한 나열과 같은 사용자가 소유한 버킷의 관련 권한을 부여해야 합니다.
- 버킷 정책의 크기는 20KB로 제한됩니다.


### 예시 1: 서브넷 10.1.1.0/24 IP 주소 범위에서 출처하고 vpcid가 aqp5jrc1인 요청을 제한합니다.
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
        "qcs::cos:ap-guangzhou:uid/1251668577:jimmyyantest-1251668577/*"
      ]
    }
  ],
  "version": "2.0"
}
```


### 예시 2: vpcid가 aqp5jrc1, 지정 의뢰인 및 지정 버킷의 요청을 제한합니다.
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
          "qcs::cam::uin/3280754170:uin/100005212150"
        ]
      },
      "Resource": [
        "qcs::cos:ap-beijing:uid/1252921383:x3cmplay-1252921383/*"
      ]
    }
  ],
  "version": "2.0"
}
```

