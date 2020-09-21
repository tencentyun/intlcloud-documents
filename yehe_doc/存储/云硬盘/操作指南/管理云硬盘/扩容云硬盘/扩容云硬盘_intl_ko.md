## 작업 시나리오
CBS는 클라우드에서 확장 가능한 스토리지 디바이스로서, 사용자는 CBS를 생성한 이후에도 CBS의 기존 데이터 손실없이 수시로 그 크기를 확장하여 스토리지 용량을 추가할 수 있습니다.
CBS 용량을 확장한 후에는 [파티션 및 파일 시스템(Windows) 용량 확장](https://intl.cloud.tencent.com/document/product/362/31601) 또는 [파티션 및 파일 시스템(Linux) 용량 확장](https://intl.cloud.tencent.com/document/product/362/31602)을 통해 용량 확장 부분의 용량을 기존 파티션 안에 나누거나, 용량 확장 부분의 용량을 독립된 새 파티션 형식으로 포맷해야 합니다.
>MBR 형식의 파티션이 지원하는 디스크 최대 용량은 2TB입니다. 만약 사용자의 디스크 파티션이 MBR 형식이고 2TB 이상으로 용량 확장해야 하는 경우, 데이터 디스크 하나를 다시 생성 및 마운트한 다음 GPT 파티션 방식을 사용하여 데이터를 새 디스크에 복사하시기를 권장합니다.

## 데이터 디스크 용량 확장
### CBS 콘솔에서 용량 확장
1. [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에 로그인합니다.
2. 타깃 CBS의 [More]>[Expand]를 선택합니다.
3. 필요한 용량 크기(반드시 현재 용량보다 크거나 같아야 함)를 선택합니다.
4. 결제를 완료합니다.
5. 타깃 클라우드 서비스의 운영 체제 유형에 따라 사용자는 [파티션 및 파일 시스템(Windows) 용량 확장](https://intl.cloud.tencent.com/document/product/362/31601) 또는 [파티션 및 파일 시스템(Linux) 용량 확장](https://intl.cloud.tencent.com/document/product/362/31602)을 실행하여 용량 확장 부분의 용량을 기존 파티션 안에 나누거나, 용량 확장 부분의 용량을 독립된 새 파티션 형식으로 포맷해야 합니다.

### CVM 콘솔에서 용량 확장
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 타깃 CVM이 있는 행에서 [More]>[Resource Adjustment]>[데이터 디스크 용량 확장]을 선택합니다.
3. 필요한 용량 크기(반드시 현재 용량보다 크거나 같아야 함)를 선택합니다.
4. 결제를 완료합니다.
5. 타깃 클라우드 서비스의 운영 체제 유형에 따라 사용자는 [파티션 및 파일 시스템(Windows) 용량 확장](https://intl.cloud.tencent.com/document/product/362/31601) 또는 [파티션 및 파일 시스템 (Linux) 용량 확장](https://intl.cloud.tencent.com/document/product/362/31602)을 통해 용량 확장 부분의 용량을 기존 파티션 안에 나누거나, 용량 확장 부분의 용량을 독립된 새 파티션 형식으로 포맷해야 합니다.

### API로 용량 확장
ResizeCbsStorage 인터페이스를 사용하여 지정 CBS를 용량 확장할 수 있습니다. 자세한 작업 방식은 [CBS 용량 확장](https://intl.cloud.tencent.com/document/product/362/16310)을 참조 바랍니다.

## 시스템 디스크 용량 확장
시스템 디스크의 유형이 CBS라면 시스템 디스크 용량 확장이 지원되지만, CVM에서 [시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933) 작업으로만 구현할 수 있습니다.
