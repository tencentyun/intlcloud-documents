### 리스트 전달 완료 여부는 어떻게 확인하나요?

매니페스트 파일 생성 시간은 사용자의 설정에 따라 다릅니다. 일별 생성을 선택한 경우, 일반적으로 베이징 시간 기준 설정 다음 날 새벽에 리스트가 전달됩니다. 주별 생성을 선택한 경우, 일반적으로 해당 주의 마지막 날 새벽부터 리스트 생성이 전달되기 시작합니다.

리스트 전달 완료 후 공지를 받으려면 [SCF](https://console.cloud.tencent.com/scf) 콘솔에서 COS 트리거를 설정하면 됩니다. 이벤트 유형은 [파일 리스트 보고 전달 완료 이벤트]로 설정합니다.

![](https://main.qcloudimg.com/raw/cfb17f03a9d103911a414ef8ec09a713.png)

### 매니페스트 파일 보고는 어떻게 분석하나요?

매니페스트 파일 보고 생성 후 COS의 [COS Select](https://intl.cloud.tencent.com/document/product/436/32472) 기능으로 매니페스트 파일의 정보를 선별할 수 있습니다. 일부 작업 예시는 다음과 같습니다.

1. 스토리지 유형이 표준 스토리지인 파일 선별:
```
select * from cosobject s where s._7 = TO_STRING('Standard')
```
2. 5GB 미만의 파일 선별:
```
select * from cosobject s where s._4<5*1024*1024
```
3. 5GB를 초과하는 표준 스토리지 유형 파일 선별:
```
select * from cosobject s where s._4>5*1024*1024 AND s._7=TO_STRING('Standard')
```
4. 복사 상태가 'replica'(복사 완료)인 파일 선별:
```
select * from cosobject s where s._9=TO_STRING('replica')
```
5. 리스트 보고 중 앞부분 100개의 파일 기록 조회:
```
select * from cosobject s limit 100
```

### COS에서 어떻게 모든 파일 정보를 내보내나요?

버킷에 리스트 기능을 활성화하면 COS에서 정기적으로 매일 또는 매주 사용자 버킷의 객체 속성, 설정 상세 정보가 담긴 리스트 보고를 출력할 수 있습니다. 자세한 소개와 작업 가이드는 [리스트 기능 활성화](https://intl.cloud.tencent.com/document/product/436/30624) 문서를 참조하십시오.

>?
>- 현재 리스트 기능은 금융 클라우드 리전은 지원하지 않습니다.
>- 리스트 기능을 사용하는 경우 이에 해당하는 **관리 기능 요금**이 발생합니다. 가격 정보에 대한 자세한 내용은 [제품 가격](https://buy.cloud.tencent.com/price/cos)을 참조하십시오.

### COS에서 파일 리스트를 어떻게 획득하나요?

COS의 파일 리스트 획득 방법은 다음과 같습니다.

1. COS 콘솔을 통해 버킷에 [리스트 기능 활성화](https://intl.cloud.tencent.com/document/product/436/30624)를 진행합니다. 리스트 기능을 활성화하면 정기적으로 매일 또는 매주 사용자 버킷의 객체 속성, 설정 상세 정보가 담긴 리스트 보고를 출력할 수 있습니다. 리스트에 대한 자세한 내용은 [리스트 기능 개요](https://intl.cloud.tencent.com/document/product/436/30622)를 참조하십시오.
2. API로 [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) 인터페이스를 호출하여 모든 객체를 획득합니다. 인터페이스는 XML 포맷으로 반환되며 직접 처리해야 합니다.

### COS 리스트 기능을 잘못 설정하였습니다. 즉시 수동으로 재시작할 수 있나요?

COS의 리스트 기능은 매일 새벽 정기적으로 최신 설정을 가져와 다시 작업을 실행합니다. 현재 즉시 수동 트리거는 지원하지 않습니다. 리스트 설정을 변경한 후, 다음 날 새벽에 다시 작업을 실행할 때까지 대기하십시오.

### COS에서 파일 유형을 통해 수량을 통계할 수 있나요?

[리스트 기능](https://intl.cloud.tencent.com/document/product/436/30622)으로 매일 또는 매주 정해진 시간에 버킷에서 지정한 객체 또는 동일한 객체 접두사를 가진 객체를 스캔하여 리스트 보고를 출력하고, CSV 포맷의 파일로 지정한 버킷에 저장할 수 있습니다. 이후 다시 'fileFormat'을 통해 타깃 파일 포맷의 파일 수에 대한 통계를 진행합니다.

### 로컬 파일과 COS에 있는 파일과의 일치 여부를 어떻게 비교하나요?
HEAD Object, List Object 요청을 통해 하나 또는 다수 객체의 MD5를 획득하여 로컬 파일의 MD5와 비교할 수 있습니다. 대용량 버킷은 [리스트 기능](https://intl.cloud.tencent.com/document/product/436/30622) 비동기 획득 객체 리스트 및 해당 MD5 값을 사용할 수 있습니다. 작업 가이드는 [리스트 기능 활성화](https://intl.cloud.tencent.com/document/product/436/30624) 콘솔 문서를 참조하십시오.

### COS에서 '파일명', '크기', '객체 주소'를 획득하고 XLS 파일로 저장하여 내보낼 수 있는 방법에는 무엇이 있나요?

리스트 기능을 활성화합니다. 리스트 기능을 통해 자동으로 리스트 보고를 출력하고, CSV 포맷의 파일로 지정한 버킷에 저장할 수 있습니다. '파일 경로', '파일 크기', '객체의 최근 수정일', 'ETag', '스토리지 유형' 등 정보를 획득할 수도 있습니다. 객체 주소를 획득해야 하는 경우, 버킷 도메인으로 파일 경로를 스티칭하는 방법을 사용합니다. 자세한 내용은 [리스트 기능 개요](https://intl.cloud.tencent.com/document/product/436/30622)를 참조하십시오.

### COS 폴더의 파일 개수나 용량 점유율은 어떻게 조회하나요?

소량 파일은 콘솔을 통해 폴더 상세 정보를 조회하면 폴더의 파일 수 및 파일이 차지하는 용량을 확인할 수 있습니다. 버킷의 객체 수가 10000개를 초과하는 경우 [리스트 기능](https://intl.cloud.tencent.com/document/product/436/30622)을 통한 조회를 권장합니다.


