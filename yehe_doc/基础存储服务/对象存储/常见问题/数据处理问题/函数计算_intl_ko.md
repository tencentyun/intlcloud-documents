### COS는 파일 압축 해제를 지원하나요?

파일 압축 해제 기능은 Tencent Cloud COS가 [SCF](https://intl.cloud.tencent.com/document/product/583)를 기반으로 사용자에게 제공하는 데이터 처리 솔루션입니다. 자세한 내용은 [파일 압축 해제 설정](https://intl.cloud.tencent.com/document/product/436/35663)을 참조하십시오.

### COS의 파일 압축 해제 기능은 하위 디렉터리의 압축 파일도 압축 해제하나요?

현재 파일 압축 해제 기능은 하위 디렉터리의 압축 패키지 압축 해제를 지원하지 않습니다. 직접 함수 로직을 변경하여 해당 시나리오를 구현할 수 있습니다.

### COS는 업로드 시 자동 파일 압축을 지원하나요?

지원하지 않습니다.

### COS는 CDN 자동 퍼지 설정을 지원하나요?

[SCF](https://intl.cloud.tencent.com/document/product/583)를 통해 자동 퍼지를 설정할 수 있습니다. 자세한 내용은 [CDN 캐시 퍼지 설정](https://intl.cloud.tencent.com/document/product/436/37273)을 참조하십시오.

### CDB의 데이터를 COS로 백업할 수 있나요?

[SCF](https://intl.cloud.tencent.com/document/product/583)를 통해 데이터베이스 백업 기능을 설정할 수 있습니다. 지정 버킷에 백업 함수 규칙을 설정하면 SCF에서 정기적으로 데이터베이스 백업 파일을 스캔하고 버킷에 파일을 저장합니다. 자세한 내용은 [CDB 백업 설정](https://intl.cloud.tencent.com/document/product/436/39629)을 참조하십시오.

