CBS(Cloud Block Storage)의 연장은 만료로 인한 데이터 손실을 효과적으로 피할 수 있으므로 중요한 데이터 설정에 대한 정기적 알림을 권장합니다.

## 엘라스틱 CBS 연장
- 엘라스틱 CBS가 만료되기 전에 연장하면 만료 후 디스크가 언마운트되어 읽기 및 쓰기의 불가능을 방지할 수 있습니다.
- 엘라스틱 CBS가 만료 후(14 일 이내) 종료되기 전에 복구하면 데이터 손실을 방지할 수 있습니다.

### 콘솔로 연장

1. [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에 로그인하십시오.
2. CBS가 있는 라인에서 [연장]을 클릭하십시오.
3. CBS 연장 페이지에서 연장 시간을 선택하고 [확인]을 클릭한 후 관련 연장 프로세스를 완료하십시오.

### API로 연장
RenewDisk 인터페이스를 사용하여 엘라스틱 CBS를 연장할 수 있습니다. 자세한 내용은 [CBS 연장](https://cloud.tencent.com/document/product/362/16319)을 참조하십시오.

### 콘솔로 복구

1. [CBS 휴지통](https://console.cloud.tencent.com/cvm/recycle/cbs)에 로그인하십시오.
2. CBS가 있는 라인에서 [복구]을 클릭하십시오.
3. 관련 결제 프로세스를 완료하십시오.
 [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에 로그인하여 방금 복구한 리소스를 조회할 수 있습니다.

## 비엘라스틱 CBS 연장

### 콘솔로 연장
비엘라스틱 CBS는 CVM 인스턴스의 라이프사이클에 따라 다릅니다. 연장해야 할 경우 구체적인 작업은 [인스턴스 연장](/doc/product/213/6143)을 참조하십시오.

### API로 연장
비엘라스틱 CBS는 CVM 인스턴스의 라이프사이클에 따라 다릅니다 . RenewInstance 인터페이스를 사용하여 비엘라스틱 CBS를 연장할 수 있습니다. 자세한 작업은 [인스턴스(정액 요금제 연장) 인터페이스](https://cloud.tencent.com/doc/Api/229/1348)를 참조하십시오.
작업 중 문제가 발생하면 [관련 문의](https://cloud.tencent.com/document/product/362/34345)를 통해 문의하십시오.

