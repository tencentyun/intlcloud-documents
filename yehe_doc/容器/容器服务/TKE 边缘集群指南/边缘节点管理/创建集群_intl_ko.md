>?현재 페이지 인터페이스는 API의 이전 버전이며 향후 점검이 중단될 수 있습니다. TKE API 3.0 버전은 보다 표준화된 인터페이스 정의와 액세스 지연 시간을 현저히 감소시켰으며, [TKE API 3.0](https://intl.cloud.tencent.com/zh/document/product/457/32029) 사용을 권장합니다.
>

## API 설명
이 인터페이스(CreateCluster)는 클러스터를 생성하는 데 사용됩니다.

인터페이스 요청 도메인:
```
ccs.api.qcloud.com
```

* 클러스터 생성 시 클러스터 내 노드(CVM)의 수와 설정을 지정해야 합니다.
* 클러스터의 모든 노드는 일반 클라우드 디스크입니다.
* 계정은 기본적으로 5개의 클러스터만 생성할 수 있으며 [티켓 제출](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS)을 통해 할당량을 늘릴 수 있습니다.
* 클러스터는 20개 노드로 제한되며, 할당량을 늘리기 위해 [티켓 제출](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS)을 할 수 있으며, 또한 [CVM 인스턴스 구매 한도](https://cloud.tencent.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E8%B4%AD%E4%B9%B0%E9%99%90%E5%88%B6) 문서에 설명된 전체 수량 한도를 준수합니다.
* CPU 및 메모리의 특정 **비례 제한**에 대해서는 [CVM 인스턴스 구성](https://cloud.tencent.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE)을 참고하십시오.
* 대역폭을 변경해야 하는 경우 노드가 성공적으로 생성된 후 인터페이스 [UpdateInstanceBandwidthHour](https://cloud.tencent.com/doc/api/229/1345)를 사용하여 변경하십시오 **공용망 대역폭을 지정하지 않을 경우 기본값은 0**입니다.
* 지원되는 노드 유형 **(각 가용존에서 구매한 모델이 다름)**, 자세한 내용은 [CVM 인스턴스 설정](https://cloud.tencent.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE)을 참고하십시오.


## 입력 매개변수
다음 요청 매개변수 목록은 인터페이스 요청 매개변수만 나열하며, 기타 매개변수는 [공통 요청 매개변수](https://cloud.tencent.com/document/product/457/9463)를 참고하십시오.

| 매개변수 이름 | 설명 |유형 | 필수  | 
|---------|---------|---------|---------|
| clusterName|클러스터 이름| String|Yes| 
| clusterDesc| 클러스터 설명|String|No| 
| clusterCIDR| 클러스터 컨테이너 및 서비스 IP를 할당하는 데 사용되는 CIDR은 VPC CIDR 또는 동일한 VPC 내의 다른 클러스터 CIDR과 충돌하지 않아야 함|String|Yes| 
| ignoreClusterCIDRConflict | ClusterCIDR 충돌 오류 무시 여부, 기본값: 0<br>0: 충돌을 무시하지 않음(오류 반환)<br>1: 충돌 무시(계속 생성)|Int|No| 
| zoneId| 가용존, [가용존 쿼리](/doc/api/213/9455) 인터페이스에서 반환된 Zone 필드 입력| String|Yes|
| goodsNum|구매한 노드 수, 최대 100개|Int|Yes| 
| cpu| CPU 코어 수, 특정 제한 사항은 상기 참고 |Int|Yes|  
| mem|  메모리 크기(GB), 특정 제한 사항은 상기 참고 |Int|Yes| 
| osName| 시스템 이름. centos7.2x86_64 또는 ubuntu16.04.1 LTSx86_64, 클러스터의 모든 노드가 이 시스템을 사용하고 확장 노드도 이 시스템을 자동으로 사용|String| Yes| 
| instanceType| 자세한 내용은 [CVM 인스턴스 구성](https://cloud.tencent.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE)을 참고하십시오. 기본값: S1.SMALL1|String|No| 
| cvmType| 노드 유형. 기본값: 사용량 과금<br>PayByHour: 사용량 과금  <br>PayByMonth: 정액 과금제<br>|String|No| 
| renewFlag|정액 과금제 및 자동 연장 표시. 값 범위:<br><li>NOTIFY_AND_AUTO_RENEW: 만료 알림 자동 연장<br><li>NOTIFY_AND_MANUAL_RENEW: 만료 알림 자동 연장 안됨<br><li>DISABLE_NOTIFY_AND_MANUAL_RENEW: 만료 알림 없고 자동 연장 안됨<br><br>기본값: NOTIFY_AND_AUTO_RENEW. 이 매개변수가 NOTIFY_AND_AUTO_RENEW로 지정되면 계정 잔액 충분 시 인스턴스 만료 후 매월 자동 연장. [InstanceChargePrepaid](https://cloud.tencent.com/document/api/213/9451#instancechargeprepaid)를 참고하십시오.|String|No|
| bandwidthType|대역폭 유형<br>정액 과금제 호스트: PayByMonth: 대역폭 사용 시간 과금, PayByTraffic: 트래픽 과금<br> 사용량 과금 호스트: PayByHour: 대역폭 사용 시간 과금, PayByTraffic: 트래픽 과금<br>네트워크 과금 방식의 차이는 [네트워크 대역폭 구매](/doc/product/213/509)를 참고하십시오.|  String|Yes|
| bandwidth| 공용망 대역폭 ( Mbps ), 트래픽 과금 시 최대 공용망 대역폭|Int| Yes| 
| wanIp| 공용 IP 활성화 여부<br>0: 활성화되지 않음<br>1: 활성화<br>bandwidth가 0보다 크면 활성화 여부를 선택할 수 있으며 기본적으로 공용 IP 활성화; bandwidth가 0이면 공용 IP가 할당되지 않음| Int| No|
| vpcId| VPC ID, [VPC 목록 쿼리](/doc/api/215/1372) 인터페이스에서 반환된 unVpcId(VPC 통합 ID) 필드 입력| String| Yes|
| subnetId| 서브넷 ID. [서브넷 목록 쿼리](/doc/api/215/1371) 인터페이스에서 반환된 unSubnetId(서브넷 통합 ID) 필드를 입력하십시오. |String|  Yes| 
| isVpcGateway| 공용망 게이트웨이 여부에 관계없이 공용망 게이트웨이는 공용 IP가 있고 VPC 아래에 있는 경우에만 정상적으로 사용<br>0: 공용망 게이트웨이가 아님<br>1: 공용망 게이트웨이|Int|Yes|  
| rootSize|시스템 디스크 크기. Linux 시스템 조정 범위: 20 - 50G, 증분: 1| Int| Yes| 
|rootType|시스템 디스크 유형. 시스템 디스크 유형 제한은 [CVM 인스턴스 설정](https://cloud.tencent.com/doc/product/213/2177)을 참고하십시오. 값 범위:<br><li>LOCAL_BASIC: 로컬 디스크<br><li>LOCAL_SSD: 로컬 SSD 디스크<br><li>CLOUD_BASIC: 일반 CBS<br><li>CLOUD_SSD: SSD CBS<br><br>기본 값: CLOUD_BASIC.|String|No|
| storageSize| 데이터 디스크 크기( GB ). 증분은 10, 0: 데이터 디스크 불필요. 최대 디스크 값은 [디스크 제품 소개](/doc/product/213/498)를 참고하십시오.|Int| Yes| 
|storageType|데이터 디스크 유형. 데이터 디스크 유형 제한은 [CVM 인스턴스 설정](https://cloud.tencent.com/doc/product/213/2177)을 참고하십시오. 값 범위:<br><li>LOCAL_BASIC: 로컬 디스크<br><li>LOCAL_SSD: 로컬 SSD 디스크<br><li>CLOUD_BASIC: 일반 CBS<br><li>CLOUD_PREMIUM: 프리미엄 CBS<br><li>CLOUD_SSD: SSD CBS<br><br>기본 값: CLOUD_BASIC.<br>|String|No|
| password| 노드 비밀번호. 미설정 시 랜덤 생성되어 내부 메시지로 전달. 노드 비밀번호는 8 - 16자리여야 하며, [ a - z, A - Z ], [ 0 - 9 ] 및  [ ( )  & # 96;~ ! @ # $ % ^ & * - + = & #124; { }  [ ] : ; ' < > ,. ?  /  ]의 특수 기호 필수 포함|String| No| 
| keyId| [키](/doc/product/213/503) ID. 키가 연결되면 해당 키를 사용하여 노드 로그인 가능. keyId는 인터페이스 [키 쿼리](/doc/api/229/%E6%9F%A5%E8%AF%A2%E5%AF%86%E9%92%A5)를 통해 얻을 수 있음. 키와 비밀번호는 동시 지정할 수 없으며 Windows 운영 체제에서는 키 지정 미지원| String| No|
| period|정액 과금제 노드 구매 시간. 단위: 월. cvmType이 PayByMonth일 때 이 매개변수는 필수 항목. | Int| No| 
| sgId|  보안 그룹 ID, 기본값: 보안 그룹 미연결. [보안 그룹 목록 쿼리](/doc/api/213/1232) 인터페이스에서 반환된 sgId 필드를 입력하십시오.|String|No| 
| masterSubnetId|  클러스터 Master VPC 서브넷의 IP를 점유하며, 이 매개변수는 Master가 점유하는 IP가 위치한 서브넷을 지정. 서브넷은 클러스터와 동일한 VP C에 있어야 함. |String|No| 
|userScript|Base64로 인코딩된 사용자 스크립트. 이 스크립트는 k8s 컴포넌트가 실행된 후 실행됨. 사용자는 스크립트의 재진입 및 재시도 로직을 확인해야 함. 스크립트 및 생성된 로그 파일은 노드의 /data/ccs_userscript/ 경로에서 확인 가능|String| No| 

## 출력 매개변수
 
| 매개변수 이름 | 설명 | 유형 |
|---------|---------|---------|
| code | 일반 오류 코드. 0: 성공, 다른 값: 실패. [응답 오류](/doc/api/457/9469) 참고|Int | 
| codeDesc | 서비스 에러 코드. 성공하면 Success를 반환하고, 오류 시에는 특정 비즈니스 오류 원인 반환|String |
| message | 인터페이스와 관련된 모듈 오류 정보 설명. [응답 오류](/doc/api/457/9469) 참고|String | 
| requestId|작업 ID |Int |
| clusterId|클러스터 ID |Int |

## 예시
### 입력
```
  https://domain/v2/index.php?Action=CreateCluster
  &cvmType=PayByHour
  &period=1
  &zoneId=xxxx
  &cpu=1
  &mem=2
  &osName=centos7.2x86_64
  &bandwidthType=PayByTraffic
  &bandwidth=1&wanIp=1
  &vpcId=vpc-xxxxx
  &subnetId=subnet-hadbzxag
  &isVpcGateway=0
  &storageType=CLOUD_PREMIUM
  &storageSize=50
  &rootType=CLOUD_PREMIUM
  &rootSize=50
  &mountTarget=/var/lib/docker
  &dockerGraphPath=/var/lib/docker
  &goodsNum=1
  &sgId=sg-fxdfnvua
  &securityService=0
  &monitorService=1
  &clusterDesc=tete
  &clusterCIDR=xxx.xxx.xxx.xxx/xx
  &ignoreClusterCIDRConflict=0
  &projectId=0
  &asEnabled=0
  &unschedulable=0
  &clusterName=xxxxx
  &clusterVersion=1.8.13
  &instanceType=S3.SMALL2
  &password=xxxxx
  &instanceName=xxxx
  &기타 공용 매개변수
```
### 출력
```
{
    "data":{
        "code":0,
        "message":"",
        "codeDesc":"Success",
        "data":{
            "requestId":xxxx,
            "clusterId":"cls-xxxxxx"
        }
    },
    "message":"",
    "code":0
}
```
