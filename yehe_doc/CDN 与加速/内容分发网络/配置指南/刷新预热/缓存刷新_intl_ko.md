## 기능 소개

CDN은 기본 캐시 설정 기능을 제공하여 지정된 서비스 유형, 디렉터리 및 특정 URL과 같은 다양한 규칙에 따라 캐시 만료 시간을 설정하여 주기적으로 노드 캐시 리소스를 정리하고 원본 서버로 최신 리소스를 가져올 수 있습니다.

이외에도 CDN은 캐시 퍼지 기능을 제공하여 대량의 URL 지정과 디렉터리 퍼지 작업을 진행할 수 있습니다.

- URL 퍼지: CDN 모든 노드에서 해당 리소스의 캐시를 삭제합니다.
- 디렉터리 퍼지: “리소스 변경 퍼지” 모드를 선택합니다. 사용자가 해당 디렉터리의 리소스에 액세스하면 원본 가져오기로 Last-Modify 정보를 얻습니다. 캐시된 리소스와 일치하면 캐시된 리소스에 직접 반환하며, 일치하지 않으면 리소스를 다시 가져오고 다시 캐시해야 합니다. “전체 리소스 퍼지”를 선택한 경우, 사용자가 매칭된 디렉터리 리소스에 액세스하면 새 리소스가 사용자에게 직접 반환되고 새 리소스가 다시 캐시됩니다.

>? 퍼지가 성공적으로 실행된 후에는 노드의 해당 리소스는 유효하지 않은 캐시가 됩니다. 사용자가 다시 액세스하면 노드 원본 서버는 필요한 리소스를 불러오고 다시 노드에 캐시합니다. 따라서 대량의 퍼지 작업을 제출하면 더 많은 캐시가 삭제되어 원본 가져오기 요청이 갑자기 증가하여 원본 서버에 더 많은 부담이 가중됩니다.

## 적용 시나리오

### 새로운 리소스 배포

원본 서버의 새 리소스로 같은 이름의 이전 리소스를 덮어쓴 후, 전체 네트워크 사용자가 노드 캐시의 영향으로 이전 리소스에 액세스되는 것을 방지하기 위해 해당 리소스의 URL/디렉터리를 제출하여 퍼지할 수 있습니다. 전체 네트워크 캐시가 삭제된 후에는 전체 네트워크 사용자는 직접 최신 리소스에 액세스할 수 있습니다.

### 위반 리소스 정리

사이트에서 위반 리소스(음란물, 마약, 도박)가 발견된 경우 원본 서버 리소스를 삭제한 후에도 노드 캐시 리소스로 인해 계속 액세스할 수 있게 됩니다. 네트워크 환경 보호를 위해 URL 퍼지를 통해 캐시 리소스를 삭제하여 적절한 시기에 정리 작업을 진행할 수 있습니다.

## 운영 가이드

### 사용 방법

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 후, 왼쪽 메뉴에서 [Purge and Prefetch]를 클릭한 다음 필요에 따라 [Purge URL] 또는 [Purge Directory]를 제출하십시오.
![](https://main.qcloudimg.com/raw/a3442259ffa50bccb60dabf002ea6dfb.png)
![](https://main.qcloudimg.com/raw/d4b01354bab726ea890e8167ccdbaffe.png)

>? urlencode 기능을 활성화하면 URL 퍼지 및 디렉터리 퍼지가 중국어 문자를 자동으로 코딩 전환해 줍니다.

<span ID = "notes"></span>
[History]에서 시간 주기, 키워드, 퍼지 작업 유형을 지정하여 조회할 수 있으며, 키워드는 도메인 지정 조회 또는 완전한 URL/디렉터리 퍼지 조회만 가능합니다.
![](https://main.qcloudimg.com/raw/86e00c9652a635cf0a0007172119be92.png)

>? 콘솔은 한 번에 최대 10000개의 작업 기록을 반환할 수 있으며 완전한 excel 형식으로 내보내기를 지원합니다. 퍼지 작업이 비교적 많은 경우 분량을 나누어 조회하고 내보내십시오.

### 주의사항

**URL 퍼지**:

- 계정당 하루 최대 10000개의 URL 퍼지를 진행할 수 있으며, 한 번에 최대 1000개까지 제출할 수 있습니다. 중국 외 가속을 활성화한 사용자는 중국 외에서 하루 최대 10000개의 URL 퍼지를 진행할 수 있으며, 중국 내 제한과는 상호 독립적입니다.
- 퍼지 제출 시에는 `http://` 또는 `https://` 프로토콜 식별자가 반드시 존재해야 합니다.
- http://*. test.com/` 형식의 URL 퍼지는 지원되지 않으며, 와일드카드 서브도메인으로 가속 서비스를 액세스하더라도 퍼지할 때 해당 서브 도메인을 제출하여 퍼지해야 합니다.
- 퍼지 제출 시 URL 상의 도메인은 가속 서비스에 액세스해야 하며, 그렇지 않을 경우 제출이 실패됩니다.
- 기본적으로 URL 퍼지 작업 제출 시 URL 상의 도메인 가속 리전에 따라 전체 리전 퍼지를 진행합니다.

**디렉터리 퍼지**:

- 계정당 하루 최대 100개의 디렉터리 퍼지를 진행할 수 있으며, 한 번에 최대 20개까지 제출할 수 있습니다. 중국 외 가속을 활성화한 사용자는 중국 외에서 하루 100개의 디렉터리 퍼지를 진행할 수 있으며, 중국 내 제한과는 상호 독립적입니다.
- 퍼지 제출 시에는 `http://` 또는 `https://` 프로토콜 식별자가 반드시 존재해야 합니다.
- http://*. test.com/` 형식의 디렉터리 퍼지는 지원되지 않으며, 와일드카드 서브도메인으로 가속 서비스를 액세스하더라도 퍼지할 때 해당 서브 도메인을 제출하여 퍼지해야 합니다.
- 퍼지 제출 시 URL 상의 도메인은 가속 서비스에 액세스해야 하며, 그렇지 않을 경우 제출이 실패됩니다.

**서브 계정 권한 설정**:

- 디렉터리 퍼지, URL 퍼지 및 기록 퍼지 조회는 현재 최신 권한 시스템에 액세스하여 리소스(도메인) 차원의 권한 설정을 지원합니다.
- 할당 방식은 [권한 설정](https://intl.cloud.tencent.com/document/product/228/35229)을 참조하십시오.

## 사용 사례

### 디렉터리 퍼지 - 리소스 변경 퍼지

가속 도메인이 purge-test-1251991073.file.myqcloud.com이고 원본 서버가 Tencent Cloud Object Storage(COS)일 때 원본 서버 리소스는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/ed694acc98a8d3114c8a9922f7374a1b.png)

1. 리소스 1.txt 및 2.txt에 각각 액세스 요청을 시작합니다. X-Cache-Lookup: Hit From Disktank3 및 Server: NWS_SPMid에 따라 노드 히트를 판별하고, 노드가 직접 리소스를 리턴합니다.
   ![](https://main.qcloudimg.com/raw/9b307b80e7d1c759bb073eb9f2cf4b6c.png)
   ![](https://main.qcloudimg.com/raw/5fed8bff43d699f47235e5d0db1f2447.png)
2. 동일한 이름의 파일 1.txt가 원본 서버에서 대체될 때 파일 수정 시간이 변경되고 2.txt는 변경되지 않습니다.
   ![](https://main.qcloudimg.com/raw/798fd6a984813aa3a16eaf43856ff7c2.png)
   ![](https://main.qcloudimg.com/raw/bc0d40200fbc744ed34d8552a95c5671.png)
3. 이때 요청이 다시 시작됩니다. 캐시가 만료되지 않았으므로 액세스 리소스 1.txt는 여전히 이전 내용입니다.
   ![](https://main.qcloudimg.com/raw/b5769a3d7fddaeadfda229115ac59bb8.png)
4. 디렉터리 퍼지를 제출하고 [리소스 변경 퍼지]를 선택한 후, 퍼지가 완료될 때까지 기다립니다.
   ![](https://main.qcloudimg.com/raw/31346a963f189187852dde17a4bf0309.png)
5. 퍼지가 완료되면 1.txt Last-Modified 파일이 변경되므로 직접 원본 가져오기 요청이 진행되며, 2.txt 파일은 변경사항이 없어 디렉터리 퍼지가 제출되어도 노드 히트에 의해 반환됩니다.
   ![](https://main.qcloudimg.com/raw/0ea8c1e0e7caac970b3875d4b3987687.png)
   ![](https://main.qcloudimg.com/raw/84e599b1c9c655e62497fb4bdc8e7918.png)
