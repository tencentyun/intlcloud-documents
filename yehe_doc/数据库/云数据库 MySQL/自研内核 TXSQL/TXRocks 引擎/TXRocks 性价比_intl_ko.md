TXRocks는 InnoDB에 필적하는 성능을 가지고 있습니다. 그러나 LSM Tree 구조는 InnoDB의 half-full 페이지 및 조각으로 인해 발생하는 낭비와 더 많은 저장 공간을 절약하여 가성비가 매우 높습니다.

## 배경 정보
TXRocks는 TencentDB 제품에서 InnoDB에 대한 중요한 보완책으로 사용됩니다. 유사한 성능으로 더 많은 저장 공간을 절약하기 위해 더욱 최적화되고 개선되었습니다. 다음은 공간 사용 및 성능 측면에서 두 엔진을 비교한 것입니다.

## TXRocks는 InnoDB보다 적은 공간 사용
![](https://qcloudimg.tencent-cloud.cn/raw/9a25d5d5f89ea06cd60790873d2c8eef.png)
**테스트 시나리오**: 두 스토리지 엔진 모두 SysBench의 기본 구성과 기본 테이블 구조를 사용합니다. 각 테이블에는 80만 개의 레코드가 포함되어 있으며 총 테이블 수는 4개에서 512개로 점차 증가합니다.
지정된 테스트 조건에서 TXRocks와 InnoDB의 공간 사용량은 위와 같습니다. 디스크 사용량은 Y축에 표시됩니다.
테스트 데이터에서 볼 수 있듯이 데이터 볼륨이 클수록 TXRocks의 디스크 사용량 증가가 느려지고 TXRocks의 저장 공간 활용도가 높아집니다(최상의 경우 InnoDB가 사용하는 공간의 42.71%만 사용). 반복성이 높은 접두사가 있는 데이터 레코드의 경우 TXRocks가 더 높은 압축률과 저장 가성비를 보입니다.

## TXRocks와 InnoDB의 성능이 유사함
![](https://qcloudimg.tencent-cloud.cn/raw/edc342ca0973e20e4d96ef88a8477b89.png)
**테스트 시나리오**: 8코어 32GB MEM 인스턴스와 각각 5백만 행의 데이터가 포함된 6개의 테이블이 테스트에 사용됩니다. 각 테스트 case는 콜드 인스턴스 재시작 후 수행되며 1200초 동안 실행됩니다.
지정된 테스트 조건에서 TXRocks와 InnoDB 간의 성능 비교는 위와 같습니다. TXRocks와 InnoDB가 비슷한 성능을 가지고 있음을 알 수 있습니다.
**sysbench 명령의 주요 매개변수**:
```
sysbench --table-size=5000000 --tables=6 --threads=32 --time=1200
```

## 결론
TXRocks는 TencentDB for MySQL 스토리지 엔진으로 InnoDB와 비슷한 성능을 가지고 있지만 저장 공간을 덜 사용합니다. 비즈니스 성능을 보장할 뿐만 아니라 스토리지 비용도 절감합니다. 자세한 내용은 [TXRocks 개요](https://intl.cloud.tencent.com/document/product/236/47015)를 참고하십시오.
