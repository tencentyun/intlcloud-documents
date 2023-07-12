### COS API는 S3 프로토콜을 지원합니까?

COS는 AWS S3 호환 API를 제공합니다. 자세한 내용은 [AWS S3 SDK로 COS 액세스](https://intl.cloud.tencent.com/document/product/436/32537)를 참고하시기 바랍니다.

### API 인터페이스를 호출할 때 ‘Request has expired’ 등의 오류가 발생합니다. 어떻게 해야 하나요?

두 가지 경우에 위와 같은 오류가 발생합니다.
- 요청 시작 시점이 서명 유효 기간을 초과했기 때문입니다.
- 로컬 시스템 시간과 해당 지역 시간이 일치하지 않기 때문입니다.

첫 번째 원인에 해당하는 경우 유효한 서명을 인증 받아 다시 API를 호출하십시오. 두 번째 원인에 해당하는 경우 로컬 시스템 시간을 해당 지역 시간에 맞춰 주십시오.

### 업로드를 완료하지 못한 파일을 삭제하려면 어떤 API를 호출해야 하나요? 

업로드가 완료되지 않은 파일 목록을 불러오려면 ListMultipartUploads 인터페이스를 호출합니다. 그 후 Abort Multipart upload 인터페이스를 호출해 멀티파트 업로드를 중단한 후 이미 업로드된 부분을 삭제합니다.

### 대량 삭제 인터페이스를 호출하면 올바르게 반환되지만 실제로 파일은 삭제되지 않습니다. 어떻게 해야 하나요?

삭제된 파일 경로를 검사해 주십시오. 파일 경로는 `/`로 시작하지 않아도 됩니다.



### COS에 UploadPart 멀티파트 업로드 요청 시 NoSuchUpload가 반환되는 이유는 무엇입니까？

**uploadId**와 **partNumber**가 동일할 때, 나중에 전송되는 파트가 이전 파트를 덮어씁니다. **uploadId**가 존재하지 않을 경우 ‘404 오류, NoSuchUpload’가 반환됩니다. 자세한 내용은 [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750)를 참고하십시오.

### API로 어떻게 객체 스토리지 유형을 수정할 수 있나요?

사용자는 PUT Object – Copy 인터페이스를 호출하여 x-cos-storage-class 매개변수를 수정하는 방법으로 객체 스토리지 유형을 바꿀 수 있습니다. 자세한 사항은 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)를 참고하십시오.

### COS에서 서명 유효 기간을 없애려면 어떻게 설정해야 하나요?

COS 서명은 타임스탬프로 기한을 넘겼는지 여부를 판단하기 때문에 유효 기간을 없앨 수는 없습니다. 사용자가 유효 기간이 없는 인증키로 서명을 생성하여 장기간 유효한 서명을 쓰고 싶다면 타임스탬프를 길게(예: 현재 시간으로부터 50년 후 만료) 설정할 수 있습니다. 임시 키의 최대 유효 기간이 2시간이기 때문에 서명을 생성하면 유효 기간은 2시간 이내가 됩니다.

### COS는 API 청구서 조회 기능을 지원합니까?

COS는 청구서 조회 API를 제공하지 않습니다. 콘솔 [청구서 상세](https://console.cloud.tencent.com/expense/bill/summary)를 통해 조회하시기 바랍니다. API를 통해 청구서 상세 내역을 조회해야 하는 경우, [청구서 상세 내역 조회](https://intl.cloud.tencent.com/document/product/555/30756) 과금 문서를 참고하십시오.

### API를 통한 스토리지 객체 크기 조회가 지원됩니까?

[GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) 인터페이스를 통해 객체 크기를 조회할 수 있습니다.

### API를 통해 객체 이름을 수정하는 방법은 무엇입니까?

[PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)를 통해 객체를 복사하고 객체 이름을 지정하여 이름을 변경할 수 있습니다.

### API를 통해 버킷 도메인을 획득하는 방법은 무엇입니까? 

[HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) 인터페이스를 통해 버킷 도메인을 획득합니다. 응답 헤더의 ‘x-cos-bucket-region’ 매개변수 값은 버킷 소재 리전을 표시합니다.

### API를 통해 버킷 크기를 획득하는 방법은 무엇입니까?

COS에는 버킷 크기를 획득하는 API가 없습니다. [클라우드 모니터링 인터페이스](https://intl.cloud.tencent.com/document/product/248/37269)를 통해 버킷의 각 스토리지 유형의 스토리지 용량을 획득한 후 버킷 스토리지 용량을 합산할 수 있습니다.

### API를 통해 사용량 내역을 조회하는 방법은 무엇입니까?

다음 3가지 방법을 참고하시기 바랍니다.

1. [API 요청 툴](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeDosageCosDetailByDate&SignVersion=)을 사용하여 조회 진행.

### COS에 디렉터리 작업 API 인터페이스가 있습니까?

COS 자체에는 폴더 및 디렉터리의 개념이 없습니다. 콘솔에 표시되는 폴더는 / 로 끝나는 빈 객체입니다.

### API를 통해 디렉터리/폴더를 생성하는 방법은 무엇입니까?

[PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) 인터페이스 호출을 통해 구현합니다. 파일명이 ‘/’로 끝나는 빈 파일로 디렉터리 형식을 생성할 수 있습니다.

>?COS 자체에는 폴더나 디렉터리의 개념이 없습니다. COS는 사용자의 편의를 위해 콘솔, COSbrowser 등 시각화된 툴에 [폴더] 또는 [디렉터리]를 재현했습니다. 구체적인 구현 방법은 파일 이름이 `/`로 끝나고, 콘텐츠가 비어있는 객체를 통해 전통적인 폴더 표시 방법으로 재현한 것입니다.

### API를 통해 디렉터리/폴더를 삭제하는 방법은 무엇입니까?

COS API는 단일 파일 삭제만을 지원합니다. 전체 디렉터리 삭제는 [GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) 인터페이스를 사용하여 지정 접두사(prefix 매개변수)로 시작하는 모든 파일을 획득한 후, [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)를 통해 구현할 수 있습니다. 

### COS INTELLIGENT TIERING이 Object가 속한 티어링 스토리지를 구분하는 방법은 무엇입니까?

[객체 메타데이터 조회](https://intl.cloud.tencent.com/document/product/436/7745)인터페이스가 반환한 **x-cos-storage-tier**를 통해 객체가 속한 스토리지 레이어를 획득합니다.

### COS가 API를 통해 객체 검색하는 방법은 무엇입니까?

[HEAD Object 인터페이스](https://intl.cloud.tencent.com/document/product/436/7745)를 통해 해당 객체 존재 여부를 확인할 수 있습니다. 특정 객체 검색이 필요한 경우, [Get Bucket 인터페이스](https://intl.cloud.tencent.com/document/product/436/30614)를 통해 버킷 내부 모든 객체를 획득한 후 확인을 진행할 수 있습니다.

### COS GET Object 인터페이스 사용 시, 동적 지정된 반환 콘텐츠는 첨부파일로 다운로드 가능합니까? 

GET Object 인터페이스 사용 시, url에 **response-content-disposition** 매개변수를 포함하며, 첨부파일 다운로드 시 **attachment**으로 값을 설정하면 됩니다. 이런 유형의 GET Object 요청은 서명을 포함해야 하며, COS 서명 툴을 통해 서명을 생성할 수 있습니다.

### COS의 putObjectCopy 호출 시 NoSuchKey 표시가 뜹니다. 어떻게 처리해야 합니까?

소스 파일이 있는지 확인하시기 바랍니다. 소스 파일이 있다면 일반적으로 폴더 뒤에 ‘/’를 추가하지 않았기 때문에 오류가 발생합니다. ‘/’ 추가 후 재시도하십시오.

### API를 통해 일정 object를 획득하는 request 횟수를 지원합니까?

 COS는 API를 통해 일정 object를 획득하는 request 횟수를 지원하지 않습니다. 분석 로그를 통해 작업을 진행할 수 있으며,  먼저 [로그 관리 기능 활성화](https://intl.cloud.tencent.com/document/product/436/17040) 후 로그 분석을 통해 획득할 수 있습니다.



