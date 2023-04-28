## 작업 시나리오
빠른 마이그레이션은 [온라인 마이그레이션](https://intl.cloud.tencent.com/document/product/213/35639)의 단순화된 버전입니다. 소스 서버 로그인 및 툴 다운로드와 같은 복잡한 작업 없이 일괄적으로 마이그레이션 작업을 생성할 수 있으며 소스 운영 체제 및 서비스 프로그램 등을 Tencent Cloud로 동기화할 수 있습니다. 본문은 빠른 마이그레이션을 사용하여 클라우드 서버를 CVM으로 마이그레이션하는 방법을 소개합니다.

빠른 마이그레이션은 Linux 및 Windows 운영 체제 모두에 적용할 수 있습니다. 또한 CVM 콘솔의 온라인 마이그레이션 페이지에서 마이그레이션 진행률을 쿼리할 수 있습니다.

## 사용 제한
 1. 빠른 마이그레이션 기능에는 소스 서버 환경에 대한 특정 요구 사항이 있습니다. 특히 클라우드 어시스턴트(예시: Alibaba Cloud ECS Cloud Assistant)를 설치하고 공중망 IP를 구성하고 VPC(클래식 네트워크는 지원되지 않음)를 사용해야 합니다.
 2.  현재 빠른 마이그레이션은 Alibaba Cloud 서버만 Tencent Cloud로 마이그레이션할 수 있습니다. 다른 플랫폼은 지원되지 않습니다.
 3.  빠른 마이그레이션 기능은 반복적으로 최적화되며 현재 특정 시나리오에서만 지원됩니다. 귀하의 요구 사항이 충족되지 않는 경우 [온라인 마이그레이션](https://intl.cloud.tencent.com/document/product/213/44338)을 사용하십시오.

## 마이그레이션 프로세스
빠른 마이그레이션 절차는 다음과 같습니다.
<img style="width:850px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/b9713fa4b1e2d1c977600323b1b976a2.png" />

## 마이그레이션 단계

### 1단계: 마이그레이션 준비
[](id:TencentAccessKey)
- **Tencent Cloud 콘솔에서 액세스 키 가져오기**
CAM 콘솔의 [API Keys 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 **SecretId 및 SecretKey**를 생성하고 가져옵니다. 자세한 지침은 [Root Account Access Key Management](https://intl.cloud.tencent.com/document/product/598/34228)를 참고하십시오.
>?서브 계정을 사용하여 콘솔에서 마이그레이션을 수행하려면 루트 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에 로그인하고 서브 계정에 QcloudCSMFullAccess 및 QcloudCVMFullAccess 권한을 부여해야 합니다.
[](id:AliAccessKey)
- **소스 클라우드 플랫폼에서 액세스 키 가져오기**
다음 단계에 따라 Alibaba Cloud의 AccessKeyID 및 AccessKeySecret을 가져옵니다.
 1. RAM 콘솔에 로그인하고 **신분 관리** > [**사용자**](https://ram.console.aliyun.com/users)를 선택합니다.
 2. **사용자 생성**을 클릭하고 액세스 모드로 **OpenAPI 액세스를 선택합니다(다른 옵션은 적용되지 않음)**. 그 다음 AccessKeyID 및 AccessKeySecret을 저장합니다. 자세한 지침은 [RAM 사용자 생성](https://help.aliyun.com/document_detail/93720.html)을 참고하십시오.
 3. 사용자 목록에서 대상 사용자를 찾고 **권한 추가**를 클릭하여 ECS 관리 권한(AliyunECSFullAccess) 및 ECS Cloud Assistant 관리 권한(AliyunECSAssistantFullAccess)을 추가합니다. 자세한 지침은 [RAM 사용자에게 권한 부여](https://help.aliyun.com/document_detail/116146.html)를 참고하십시오.
- **소스 서버에서 애플리케이션 일시 중지(선택 사항)**
마이그레이션의 영향을 받지 않도록 소스 서버의 모든 애플리케이션을 중지하는 것이 좋습니다.
- **소스 및 대상 데이터 백업(선택 사항)**
마이그레이션하기 전에 다음과 같은 방법으로 데이터를 백업하는 것이 좋습니다.
 - 소스 서버: 소스 서버 스냅샷 기능 또는 기타 방법을 사용하여 데이터를 백업할 수 있습니다.
 - 대상 CVM: [Creating Snapshot](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 대상 CVM 데이터를 백업할 수 있습니다.
- **대상 CVM 확인**
 마이그레이션 대상이 CVM 인스턴스인 경우 대상 CVM을 확인해야 합니다.
  <table>
<tr>
	<th style="width: 15%;">대상 CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		스토리지 공간: 대상 CVM의 클라우드 디스크(시스템 디스크 및 데이터 디스크 포함)는 소스 서버의 데이터를 저장하기에 충분한 저장 공간이 있어야 합니다.</li>
		<li>보안 그룹: 80, 443 및 3389 포트를 엽니다.</li>
		<li>
		대역폭 설정: 더 빠른 마이그레이션을 위해 양쪽 끝의 대역폭을 최대한 늘리는 것이 좋습니다. 마이그레이션 과정에서 대략 데이터 양만큼의 트래픽 소모가 발생하게 되며, 필요한 경우 미리 네트워크 과금 모드를 변경하시기 바랍니다.</li>
<li>
		네트워크 설정: 소스 또는 대상 서버가 IPv6만 지원하고 IPv4는 지원하지 않는 경우 <a href="https://intl.cloud.tencent.com/document/product/213/44340"> client.json 파일 매개변수 설명</a>을 참고하십시오.</li>
	  </ol>
	</td>
  </tr>
</table>
- **빠른 마이그레이션 페이지로 이동**
 1. CVM 콘솔에 로그인하고 **서비스 마이그레이션** > [**온라인 마이그레이션**](https://console.cloud.tencent.com/cvm/csm/online) 페이지로 이동합니다.
 2. **빠른 마이그레이션**을 클릭하여 **[빠른 마이그레이션 작업 생성](https://console.cloud.tencent.com/cvm/csm/online/oneClickMigration?rid=1)** 페이지로 이동합니다.  
![](https://staticintl.cloudcachetci.com/yehe/backend-news/mduI027_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230407161049.png)


### 2단계: 마이그레이션 작업 생성
1. **작업 구성**
작업 이름과 설명을 입력합니다.
2. **마이그레이션 소스 정보 구성**
소스 ISP는 기본적으로 Alibaba Cloud ECS로 선택되며 Alibaba Cloud 계정의 AccessKey 및 SecretKey를 입력해야 합니다([가져오는 방법](#AliAccessKey)). 그 다음 아래 이미지와 같이 **소스 서버 정보에 액세스할 수 있는 권한이 있는지 확인합니다.**
>!키를 비공개로 유지하고 마이그레이션 후 삭제 또는 비활성화하는 것이 좋습니다.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/6iz5493_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230407161205.png)
3. **마이그레이션 대상 구성**
대상 ISP는 기본적으로 CVM으로 선택되며 **CVM 사용 권한을 얻으려면** TencentCloud API의 SecretId 및 SecretKey([가져오는 방법](#TencentAccessKey))를 입력해야 합니다. [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 키 정보를 복사할 수 있습니다. API 키가 올바른지 확인하십시오. 그렇지 않으면 마이그레이션이 실패합니다.    
>!키를 비공개로 유지하고 마이그레이션 후 삭제 또는 비활성화하는 것이 좋습니다.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/P5Xt263_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230407161235.png)
4. **마이그레이션 정보 구성**
  1. 마이그레이션 소스 정보가 성공적으로 확인되면 **마이그레이션 소스 추가**를 클릭하고 팝업 창에서 대상 인스턴스를 선택합니다.
  2. 팝업창 좌측 상단의 **리전**을 선택하여 해당 리전의 **인스턴스 목록**을 가져옵니다.
  3. 대상 인스턴스를 선택하여 오른쪽의 **선택됨** 목록에 추가합니다.
 >?
 >- **여러 인스턴스, 여러 리전**에서 인스턴스를 일괄 마이그레이션하고 마이그레이션 소스를 여러 번 추가할 수 있습니다.
 >- 현재 최대 5개의 인스턴스를 일괄 마이그레이션할 수 있습니다.
 >
  4. **확인**을 클릭합니다. 그러면 마이그레이션 소스 정보 목록에 대상 인스턴스의 정보가 표시됩니다. 작업 열에서 **대상 정보 추가**를 클릭하여 마이그레이션 대상 정보를 구성할 수 있습니다.
  5. **마이그레이션 대상 추가** 팝업 창에서 리전 및 마이그레이션 대상 유형을 선택합니다.
 <table>
<thead>
<tr>
<th>구성 항목</th>
<th>필수</th>
<th>비고</th>
</tr>
</thead>
<tbody><tr>
<td>대상 리전</td>
<td>Yes</td>
<td>소스 서버를 마이그레이션할 Tencent Cloud 리전입니다. 리전에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/6091">리전 및 가용존</a>을 참고하십시오.</td>
</tr>
<tr>
<td>대상 유형</td>
<td>Yes</td>
<td>마이그레이션 소스가 마이그레이션될 Tencent Cloud 대상 유형입니다. <ul><li><strong>CVM 이미지</strong>: 마이그레이션 작업이 완료된 후 마이그레이션 소스에 대해 생성되는 Tencent Cloud 대상 이미지입니다. <br>이미지 이름: 마이그레이션 소스에 대해 생성된 Tencent Cloud 대상 이미지의 이름입니다. 이미지 이름이 대상 리전에 이미 있는 경우 마이그레이션 작업은 자동으로 이미지 이름에 작업 ID를 추가합니다. </li><li><strong>CVM 인스턴스</strong>: 마이그레이션 대상으로 사용할 대상 리전의 CVM 인스턴스입니다. <br>대상 인스턴스: 소스 서버와 동일한 운영 체제를 사용하는 대상 CVM 인스턴스를 선택하는 것이 좋습니다. 예를 들어 CentOS 7 소스 서버를 마이그레이션하려면 CentOS 7 CVM 인스턴스를 대상으로 선택합니다. 또한 대상 CVM 인스턴스의 시스템 디스크 및 데이터 디스크 용량이 소스 서버보다 커야 합니다.</li></ul></td>
</tr>
</tbody></table>
5. **생성을 클릭하고 마이그레이션 작업을 시작합니다. 안내 창이 나타납니다. 다음 사항에 유의하십시오.**
	- 마이그레이션 소스에서 작업을 실행하는 데 시간이 걸리므로 콘솔에서 진행률을 보려면 1분 정도 기다려야 합니다.
	- 소스 서버 환경이 비정상적이거나 잘못된 정보로 인해 마이그레이션 소스 가져오기에 실패한 경우 Tencent Cloud 콘솔에 실패 원인이 표시되지 않을 수 있습니다. 이 경우 작업을 다시 생성하거나 [온라인 마이그레이션](https://intl.cloud.tencent.com/document/product/213/44338)을 사용하십시오.

[](id:checkAfter)
### 3단계: 마이그레이션 후 확인
1. **마이그레이션 상태 및 진행률 보기**
성공적으로 생성된 마이그레이션 작업은 자동으로 실행됩니다. [마이그레이션 소스 페이지](https://console.cloud.tencent.com/cvm/csm/online?rid=1)에서 마이그레이션 소스 정보를 볼 수 있고 [마이그레이션 작업 페이지](https://console.cloud.tencent.com/cvm/csm/online?rid=1&tab=tasks)에서 작업 진행 상황을 볼 수 있습니다.
 - 마이그레이션 대상이 CVM인 경우 마이그레이션을 시작한 후에는 대상 CVM이 마이그레이션 모드에 들어가므로, 마이그레이션이 완료되어 마이그레이션 모드를 종료할 때까지 대상 CVM에 Reinstall the system, 종료, 폐기, 비밀번호 재설정 등의 작업을 실행하지 마시길 바랍니다.
 - 마이그레이션 대상이 CVM 이미지인 경우 마이그레이션이 시작된 후 계정에 릴레이 인스턴스 do_not_delete_csm_instance가 생성됩니다. 릴레이 인스턴스를 다시 설치, 종료 또는 폐기하거나 비밀번호를 재설정하지 마십시오. 마이그레이션이 완료되면 시스템에서 자동으로 종료됩니다.
2. **마이그레이션 작업이 종료될 때까지 대기**
마이그레이션 작업의 상태가 **성공**이면 마이그레이션이 성공적으로 완료되었음을 나타냅니다.
<dx-alert infotype="explain" title="">
- 데이터 전송에 필요한 시간은 소스 서버의 데이터 크기, 네트워크 대역폭 등에 따라 다릅니다. 마이그레이션 프로세스가 끝날 때까지 기다리십시오.
- 마이그레이션 작업이 시작된 후 마이그레이션 작업이 있는 행에서 **일시 중지**를 클릭하여 마이그레이션 작업을 중지할 수 있습니다.
- 마이그레이션 툴은 체크포인트 재시작을 지원하며, 작업을 일시 중단한 후 **시작/재시도**를 다시 클릭하면 마지막 일시 중지 지점부터 마이그레이션을 계속할 수 있습니다.
- 데이터 전송 중에 마이그레이션 작업을 일시 중지할 수 있습니다. 콘솔의 마이그레이션 작업에서 **일시 중지**를 클릭하면 마이그레이션 툴이 진행 중인 데이터 전송을 일시 중지합니다.
- 마이그레이션 프로세스가 너무 오래 걸리고 마이그레이션을 중지해야 하는 경우 먼저 마이그레이션 작업을 일시 중지하고 **삭제**를 클릭하여 마이그레이션 작업을 취소할 수 있습니다.
</dx-alert>
3. **마이그레이션 후 확인**
 - **마이그레이션 실패**:
문제 해결 방법은 로그 파일(기본적으로 마이그레이션 툴 디렉터리 아래 log 파일)의 오류 정보, 작업 가이드 또는 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 확인하십시오. 문제 해결 후 마이그레이션 작업 열에서 **시작/재시도**를 클릭하여 마이그레이션 작업을 다시 시작합니다.
 - **마이그레이션 성공**:
     - CVM으로 마이그레이션: 대상 CVM이 정상적으로 시작되는지, CVM의 데이터가 소스 서버의 데이터와 일치하는지, 네트워크 및 기타 시스템 서비스가 정상인지 확인합니다.
     - CVM 이미지로 마이그레이션: 마이그레이션 작업 행의 ‘CVM 이미지 ID’를 클릭하여 [CVM 이미지 페이지](https://console.cloud.tencent.com/cvm/image/index)로 이동하여 이미지 정보를 볼 수 있으며, 이 이미지를 사용하여 CVM 인스턴스를 생성할 수 있습니다.

문의 사항이나 마이그레이션에 문제가 있는 경우 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 참고하거나 [Contact Us](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 해결하실 수 있습니다.      
