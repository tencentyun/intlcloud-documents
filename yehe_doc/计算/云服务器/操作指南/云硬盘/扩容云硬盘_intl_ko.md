## 작업 시나리오
CBS는 클라우드에서 확장 가능한 스토리지 디바이스이며 사용자는 CBS를 생성한 후 수시로 그 크기를 확장하여 스토리지 용량을 증가할 수 있습니다. 또한 CBS의 기존 데이터를 손실하지 않습니다.
CBS를 확장한 후에는 [파티션 및 파일 시스템(Windows) 확장](https://intl.cloud.tencent.com/document/product/362/6737) 또는 [파티션 및 파일 시스템(Linux) 확장](https://intl.cloud.tencent.com/document/product/362/6738)으로 확장된 부분의 용량을 기존 파티션 안으로 나누거나 확장된 부분의 용량을 독립된 새로운 파티션으로 포맷해야 합니다.
>! MBR 형식 파티션이 지원하는 디스크의 최대 용량은 2TB입니다. 만약 사용자의 디스크 파티션이 MBR 형식이고 2TB 이상으로 확장해야 하는 경우, 데이터 디스크를 다시 생성하고 마운트 하고 GPT 파티션 방식을 사용하여 데이터를 새로운 디스크에 복사할 것을 권장합니다.

## 데이터 디스크 확장
### CBS 콘솔로 확장
1. [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에 로그인합니다.
2. 타깃 CBS의 [More]>[Expand]을 선택합니다.
3. 필요한 새로운 용량 크기(반드시 현재 크기보다 크거나 같아야 함)를 선택합니다.
4. 결제를 완료합니다.
5. 타겟 클라우드 서비스의 운영 체제 유형에 따라 사용자는 [파티션 및 파일 시스템 (Windows) 확장](https://cloud.tencent.com/document/product/362/6737) 또는 [파티션 및 파일 시스템(Linux) 확장](https://cloud.tencent.com/document/product/362/6738)을 실행하여 확장된 부분의 용량을 기존 파티션 안으로 나누거나 확장된 부분의 용량을 독립된 새로운 파티션으로 포맷해야 합니다.

### CVM 콘솔로 확장
1. [CVM 인스턴스 리스트](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 타깃 CVM 라인의 [More]>[Resource Adjustment]>[하드 디스크 조정]을 선택합니다.
3. 필요한 새로운 용량 크기(반드시 현재 크기보다 크거나 같아야 함)를 선택합니다.
4. 결제를 완료합니다.
5. 타깃 클라우드 서비스의 운영 체제 유형에 따라 사용자는 [파티션 및 파일 시스템 (Windows) 확장](https://intl.cloud.tencent.com/document/product/362/6737) 또는 [파티션 및 파일 시스템 (Linux) 확장](https://intl.cloud.tencent.com/document/product/362/6738)으로 확장된 부분의 용량을 기존 파티션으로 나누거나 확장된 부분의 용량을 독립된 새로운 파티션으로 포맷해야 합니다.

### API로 확장
사용자는 ResizeCbsStorage 인터페이스를 사용하여 스냅샷을 생성할 수 있습니다. 자세한 내용은 [CBS 확장](https://intl.cloud.tencent.com/document/product/362/16310)을 참조하십시오.

## 시스템 디스크 확장
시스템 디스크 유형이 CBS인 경우, 시스템 디스크 확장이 지원되지만 CVM을 통한 [시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933) 작업만 수행될 수 있습니다.
