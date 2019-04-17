## InstanceSet

인스턴스 세부 정보 리스트

다음 API에 참조됨: DescribeInstances.

| 이름 | 유형 |  설명 |
|------|------|-------|
| InstanceName | String | 인스턴스 이름 |
| InstanceId | String | 인스턴스 ID |
| Appid | Integer | 사용자의 Appid |
| ProjectID | Integer | 프로젝트 ID |
| RegionID | Integer | 지역 ID 1--광저우, 4--상하이, 5-- 홍콩, 6--토론토, 7--상하이 금융, 8--베이징, 9--싱가포르, 11--선전 금융, 15--미국 서부(실리콘 밸리), 16--청두, 17--독일, 18--한국, 19--충칭, 21--인도, 22--미국 동부(버지니아), 23--태국, 24--러시아, 25--일본 |
| ZoneID | Integer | 지역 ID |
| VpcID | Integer | VPC ID, 예: 75101 |
| SubnetID | Integer | VPC의 서브넷 ID, 예: 46315 |
| Status | Integer | 인스턴스 현재 상태, 0: 초기화 대기, 1: 프로세스 중, 2: 진행 중, -2: 격리됨, -3: 삭제 대기 |
| WanIp | String | 인스턴스 VIP |
| Port | Integer | 인스턴스 포트 번호 |
| Createtime | String | 인스턴스 생성 시간 |
| Size | Float | 인스턴스 용량 크기(MB) |
| SizeUsed | Float | 인스턴스 현재 사용된 용량(MB) |
| Type | Integer | 인스턴스 유형, 1: Redis 2.8 클러스터 버전, 2: Redis 2.8 마스터/슬레이브 버전, 3: CKV마스터/슬레이브 버전(Redis3.2), 4: CKV클러스터 버전(Redis3.2), 5: Redis 2.8 스탠드 얼로운, 7: Redis 4.0 클러스터 버전 |
| AutoRenewFlag | Integer | 인스턴스 자동 갱신 설정 여부의 식별, 1: 자동 갱신이 설정됨, 0: 자동 갱신이 설정되지 않음 |
| DeadlineTime | String | 인스턴스 만료 기간 |
| Engine | String | 엔진: Redis 커뮤니티 버전, Tencent Cloud CKV |
| ProductType | String | 제품 유형: Redis 2.8클러스터 버전, Redis 2.8 마스터/슬레이브 버전, Redis 3.2 마스터/슬레이브 버전(CKV 마스터/슬레이브 버전), Redis 3.2 클러스터 버전(CKV 클러스터 버전), Redis 2.8 스탠드 얼로운, Redis 4.0 클러스터 버전 |
| UniqVpcID | String | VPC ID, 예: vpc-fk33jsf43kgv |
| UniqSubnetID | String | VPC의 서브넷 ID, 예: subnet-fd3j6l35mm0 |
| BillingMode | Integer | 요금제: 0 - 사용량 기반 요금제, 1 - 연/월정액 요금제 |

## ProductConf

제품 정보

다음 API에 참조됨: DescribeProductInfo.

| 이름 | 유형 |  설명 |
|------|------|-------|
| Type | Integer | 제품 유형, 2 - Redis 마스터/슬레이브 버전, 3 - CKV 마스터/슬레이브 버전, 4 - CKV 클러스터 버전, 5 - Redis 스탠드 얼로운, 7 - Redis 클러스터 버전 |
| TypeName | String | 제품 이름, Redis 마스터/슬레이브 버전, CKV 마스터/슬레이브 버전, CKV 클러스터 버전, Redis 스탠드 얼로운, Redis 클러스터 버전 |
| MinBuyNum | Integer | 구매 시 최소 수량 |
| MaxBuyNum | Integer | 구매 시 최대 수량 |
| Saleout | Boolean | 제품 매진 여부 |
| Engine | String | 제품 엔진, Tencent Cloud CKV 또는 Redis 커뮤니티 버전 |
| Version | String | 호환 버전, Redis-2.8, Redis-3.2, Redis-4.0 |
| TotalSize | Array of String | 사양 총 크기(G) |
| ShardSize | Array of String | 샤딩당 크기(G) |
| ReplicaNum | Array of String | 복제본 수량 |
| ShardNum | Array of String | 샤딩 수량 |
| PayMode | String | 지원하는 요금제, 1 - 연/월정액 요금제, 0 - 사용량 기반 요금제 |
| EnableRepicaReadOnly | Boolean | 복제본 읽기 전용 지원 여부 |

## RedisBackupSet

인스턴스의 백업 배열

다음 API에 참조됨: DescribeInstanceBackups.

| 이름 | 유형 |  설명 |
|------|------|-------|
| StartTime | String | 백업 시작 시간 |
| BackupID | String | 백업 ID |
| BackupType | String | 백업 유형. manualBackupInstance: 사용자가 시작한 수동 백업. systemBackupInstance: 새벽에 시스템이 시작한 백업 |
| Status | Integer | 백업 상태.  1: "백업이 기타 프로세스에 잠김", 2: “백업 정상, 어떠한 프로세스에도 잠기지 않음", -1: "백업이 만료됨", 3: “백업 내보내기 중", 4: “백업 내보내기 성공" |
| Remark | String | 백업의 주석 정보 |
| Locked | Integer | 백업 잠김 여부, 0: 잠기지 않음 1: 이미 잠김 |

## RegionConf

지역 정보

다음 API에 참조됨: DescribeProductInfo.

| 이름 | 유형 |  설명 |
|------|------|-------|
| RegionID | String | 지역 ID |
| RegionName | String | 지역 이름 |
| RegionShortName | String | 지역 약식 이름 |
| Area | String | 지역 소재 영역 이름 |
| ZoneSet | Array of [ZoneCapacityConf](#ZoneCapacityConf) | 가용 영역 정보 |

## TradeDealDetail

주문 거래 정보

다음 API에 참조됨: DescribeInstanceDealDetail.

| 이름 | 유형 |  설명 |
|------|------|-------|
| DealID | String | 주문 번호 ID, 클라우드 API 호출 시 이 ID 사용 |
| DealName | String | 긴 주문 ID, 주문 문제를 고객 서비스에게 피드백할 때 이 ID 사용 |
| ZoneID | Integer | 가용 영역 ID |
| GoodsNum | Integer | 주문이 연결한 인스턴스 수 |
| Creater | String | 사용자 uin 생성 |
| CreatTime | String | 주문 생성 시간 |
| OverdueTime | String | 주문 타임아웃 시간 |
| EndTime | String | 주문 완료 시간 |
| Status | Integer | 주문 상태 1: 미지불, 2: 지불 완료 미발송, 3: 발송 중, 4: 발송 성공, 5: 발송 실패, 6: 환불 완료, 7: 주문 종료됨, 8: 주문 만료됨, 9: 주문 무효됨, 10: 제품 무효됨, 11: 대지급 거절, 12: 지불 중 |
| Description | String | 주문 상태 설명 |
| Price | Integer | 주문 실제 총 가격(USD) |
| InstanceIDs | Array of String | 인스턴스 ID |

## ZoneCapacityConf

가용 영역 내 제품 정보

다음 API에 참조됨: DescribeProductInfo.

| 이름 | 유형 |  설명 |
|------|------|-------|
| ZoneID | String | 가용 영역 ID, 예: ap-guangzhou-3 |
| ZoneName | String | 가용 영역 이름 |
| IsSaleout | Boolean | 가용 영역 매진 여부 |
| IsDefault | Boolean | 기본 가용 영역 여부 |
| NetWorkType | Array of String | 네트워크 유형: basenet -- 기본 네트워크, vpcnet -- VPC |
| ProductSet | Array of [ProductConf](#ProductConf) | 가용 영역 내 제품 사양 등 정보 |
| OldZoneID | Integer | 가용 영역 ID, 예: 100003 |
