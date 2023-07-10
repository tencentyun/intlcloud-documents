## 로그

### COS(Cloud Object Storage)는 파일 업로드/다운로드/삭제 로그를 제공합니까?
COS는 소스 버킷의 액세스 세부 정보를 기록하는 [로그 관리](https://intl.cloud.tencent.com/document/product/436/16920) 기능을 제공하며, 이러한 로그는 더 나은 버킷 관리를 위해 대상 버킷에 저장됩니다. 파일 업로드/다운로드/삭제 로그를 얻으려면 액세스 로그 관리 기능을 활성화하여 파일 작업을 기록하십시오.

### COS에서 가장 많은 공용 네트워크 트래픽을 발생시키는 파일을 어떻게 쿼리합니까?

COS의 [로그 관리](https://intl.cloud.tencent.com/document/product/436/16920) 기능을 사용하여 버킷 액세스 로그를 다운로드하고 어떤 파일이 가장 많은 공용 네트워크 트래픽을 소비하는지 분석하는 프로그램을 작성할 수 있습니다. 통계 수집을 위해 DLC(Data Lake Compute)에 로그를 로딩할 수도 있습니다.

### COS의 대부분의 공용 네트워크 트래픽이 어떤 소스 IP에서 오는지 어떻게 쿼리합니까?
COS의 [로그 관리](https://intl.cloud.tencent.com/document/product/436/16920) 기능을 사용하여 버킷 액세스 로그를 다운로드하고 대부분의 공용 네트워크 트래픽이 어떤 소스 IP에서 발생하는지 분석하는 프로그램을 작성할 수 있습니다. 통계 수집을 위해 DLC에 로그를 로딩할 수도 있습니다.

### COS에서 공용 네트워크 다운스트림 트래픽 및 요청 수에 대한 임계값을 설정할 수 있습니까?
[클라우드 모니터링 콘솔](https://console.cloud.tencent.com/monitor)에서 [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916)를 통해 COS의 공용 네트워크 다운스트림 트래픽이 임계값에 도달하면 알람 알림을 받을 수 있습니다. COS는 임계값에 도달했을 때 서비스를 자동으로 일시 중단할 수 없습니다.

### 파일 삭제 로그를 보려면 어떻게 해야 합니까?

[로그 관리](https://intl.cloud.tencent.com/document/product/436/16920) 기능으로 발송된 로그를 조회하여 파일 삭제 로그를 조회할 수 있습니다. 액세스 로그 관리 기능이 활성화되면 로그 파일을 DLC에 로딩하여 삭제 로그를 필터링할 수 있습니다. 아래는 삭제 로그 샘플입니다. `reqMethod` 필드에서 `DELETE` 작업을 검색하여 이러한 로그를 얻을 수 있습니다.

```plaintext
1.0 examplebucket-125000000 ap-chengdu 2020-02-10T13:07:00Z examplebucket-125000000.cos.ap-chengdu.myqcloud.com DELETEObject 110.110.110.110 AKIDSuCmiBvppcdxShtPrCjhEUPF****-J6AsmEPu8NYMOhgx3HLExh - 0 0 / DELETE tencentcloud-cos-console 200 - - 746 146 USER - 100009682373 - 100009682373:100009682373 NWU0MTU1NzRfNWNiMjU4NjRfM2JkMV8yNGFiNGEw - - - - DELETE /filepath HTTP/1.1
```

액세스 로그 중 삭제 로그를 찾을 수 없는 경우 [라이프사이클 설정](https://intl.cloud.tencent.com/document/product/436/14605)에서 만료 시 삭제 규칙이 설정되어 있는지 확인하십시오.

### COS 버킷 구성 로그를 쿼리하려면 어떻게 해야 합니까?

버킷 구성 로그는 CloudAudit(CA)에 제공됩니다. [Viewing Event Details in Operation Record](https://intl.cloud.tencent.com/document/product/1021/40499)에 설명된 대로 이러한 로그를 검색할 수 있습니다.


### 버킷 생성/삭제 로그는 어디에서 쿼리할 수 있습니까?

버킷 생성 및 삭제 로그는 CA에 제공됩니다. `DeleteBucket` 및 `PutBucket` 이벤트를 선택하여 [Viewing Event Details in Operation Record](https://intl.cloud.tencent.com/document/product/1021/40499)에 설명된 대로 작업 로그를 필터링할 수 있습니다.



## 모니터링

### COS에서 트래픽을 조절할 수 있습니까?

아니요. 그러나 트래픽이 특정 임계값에 도달할 때 이메일 또는 SMS로 알람 및 푸시 알림을 트리거하도록 **클라우드 모니터링**에서 [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916)할 수 있습니다.

### 모니터링 대시보드의 요청 수/트래픽이 갑자기 증가하는 이유는 무엇입니까?

비즈니스의 요청 수 또는 트래픽이 비정상적으로 급증하는 경우 비즈니스가 핫링크될 수 있습니다. 버킷에 대해 공개 읽기가 활성화되어 있는지 확인해야 합니다. 비즈니스에 통제할 수 없는 위험을 초래할 수 있으므로 공개 읽기를 활성화하지 않는 것이 좋습니다. [최소 권한 원칙](https://intl.cloud.tencent.com/document/product/436/32972)에 따라 액세스 권한을 부여할 수 있습니다.

공개 읽기를 사용해야 하는 경우 버킷 보안을 보장하기 위해 다음 방법을 사용하는 것이 좋습니다.
1. 버킷에 대한 [로그 관리](https://intl.cloud.tencent.com/document/product/436/16920) 기능을 활성화하여 버킷 액세스 요청을 기록합니다.
2. [링크 도용 방지](https://intl.cloud.tencent.com/document/product/436/32466) 기능을 활성화하여 비정상적인 IP의 액세스 요청을 차단합니다.
3. [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916) 및 임계값을 설정하여 트래픽이 임계값을 초과하면 알람이 SMS 또는 이메일로 전송되도록 합니다.
