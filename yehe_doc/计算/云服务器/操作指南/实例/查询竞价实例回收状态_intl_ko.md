
CVM 스팟 인스턴스 모드는 가격, 재고 등의 이유로 시스템 자체적으로 인스턴스를 회수하는 것으로 인스턴스 회수 전에 사용자 정의 작업의 편의를 위해 인스턴스 내부에서 Metadata 메커니즘으로 회수 상태를 획득할 수 있는 인터페이스를 제공합니다. 자세한 사용 방법은 다음과 같습니다. 

## Metadata 설명
인스턴스 메타데이터는 인스턴스 관련 데이터를 의미하며 실행 중인 인스턴스 설정 및 관리에 사용할 수 있습니다. 인스턴스 내부를 통해 인스턴스 메타데이터에 액세스하고 관련 정보를 획득할 수 있습니다. 자세한 내용은 [인스턴스 메타데이터 조회](https://intl.cloud.tencent.com/document/product/213/4934)를 참고하십시오.


## Metadata를 통해 스팟 인스턴스 회수 상태 정보 획득
cURL 툴 및 HTTP의 GET 요청을 통해 metadata에 액세스하고 스팟 인스턴스 회수 상태 정보를 획득합니다.
```
curl metadata.tencentyun.com/latest/meta-data/spot/termination-time
```
- 다음과 같이 반환된 정보는 스팟 인스턴스 회수 시간을 의미합니다. 
>?스팟 인스턴스의 운영 체제에 설정한 회수 시간으로 시간대 기준은 UTC +8입니다. 
>
```
2018-08-18 12:05:33
```
- 404가 반환되었다면 해당 인스턴스는 스팟 인스턴스가 아니거나 회수가 트리거되지 않았음을 의미합니다. 

작업에 대한 자세한 내용은 [인스턴스 메타데이터 조회](https://intl.cloud.tencent.com/document/product/213/4934)를 참고하십시오.

