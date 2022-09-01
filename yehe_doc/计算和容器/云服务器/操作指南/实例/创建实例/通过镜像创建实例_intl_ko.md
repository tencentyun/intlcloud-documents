## 작업 시나리오
사용자 정의 이미지를 사용하여 동일한 운영 체제/응용 프로그램/데이터를 보유한 CVM 인스턴스를 손쉽게 생성해, 업무와 딜리버리 효율을 향상시킬 수 있습니다. 본 문서는 사용자 정의 이미지를 사용하여 인스턴스를 생성하는 방법에 대해 안내합니다.


## 전제 조건
인스턴스를 생성할 계정 및 리전에 사용자 정의 이미지가 생성되어 있어야 합니다.
사용자 정의 이미지를 생성하지 않았다면 아래의 방법을 참고하시기 바랍니다.
<table>
	<tr><th>이미지 보유 현황</th><th>작업 방법</th></tr>
	<tr><td>로컬 혹은 기타 플랫폼에 이미지를 보유하고 있다면</td><td> 로컬 또는 기타 플랫폼의 서버 시스템 디스크 이미지 파일을 Cloud Virtual Machine(CVM)의 사용자 정의 이미지로 가져올 수 있습니다. 자세한 작업 방식은 <a href="https://intl.cloud.tencent.com/document/product/213/4945">미러 이미지 가져오기 개요</a>를 참조 바랍니다.</td></tr>
	<tr><td>보유한 사용자 정의 이미지가 없으나 템플릿으로 사용할 인스턴스가 있다면</td><td> 자세한 작업 방식은 <a href="https://intl.cloud.tencent.com/document/product/213/4942">커스텀 미러 구축</a>을 참조 바랍니다.</td></tr>
	<tr><td>기타 리전에 사용자 정의 이미지를 보유하고 있다면</td><td> 사용자 정의 이미지를 인스턴스를 생성할 리전으로 복사할 수 있습니다. 자세한 작업 방식은 <a href="https://intl.cloud.tencent.com/document/product/213/4943">미러 복사</a>를 참조 바랍니다.</td></tr>
	<tr><td>기타 계정에 사용자 정의 이미지를 보유하고 있다면</td><td> 사용자 정의 이미지를 인스턴스를 생성할 리전의 계정으로 공유할 수 있습니다. 자세한 작업 방식은 <a href="https://intl.cloud.tencent.com/document/product/213/4944">사용자 정의 이미지 공유</a>를 참조 바랍니다.</td></tr>
</table>

## 작업 단계

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/instance/index?rid=1)에 로그인합니다.
2. 왼쪽 메뉴의 **Images**를 클릭하여 이미지 관리 페이지에 접속합니다.
3. 이미지 관리 페이지 상단의 상태에서 리전을 선택합니다.
4. 이미지의 출처에 따라 탭을 선택하여 이미지 리스트 인터페이스에 접속합니다.
 - **Public Images** 탭: 공용 이미지 인터페이스로 이동합니다.
 - **Custom Image** 탭: 사용자 정의 이미지 인터페이스로 이동합니다.
 - **Shared Image** 탭: 공유 이미지 인터페이스로 이동합니다.
5. 사용 대기 중인 이미지의 작업 열에서 **Create Instance**를 클릭합니다.
![](https://main.qcloudimg.com/raw/4c5806f49da53595d31ad07662bf363a.png)
6. 팝업 창에서 **확인**을 클릭합니다.
7. 인터페이스 안내에 따라 인스턴스 정보를 구성하여 인스턴스 생성을 완료합니다.
리전 및 이미지 정보는 자동으로 입력되며, 필요에 따라 다른 인스턴스 정보를 구성할 수 있습니다. 세부 정보는 [구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참조 바랍니다.
<dx-alert infotype="explain" title="">
선택하신 사용자 정의 이미지에 하나 또는 그 이상의 데이터 디스크 스냅샷이 포함되어 있다면, 시스템이 해당 스냅샷에 따라 동일한 수량의 Cloud Block Storage(CBS)를 자동으로 생성하여 데이터 디스크로 삼습니다. 각 CBS의 용량은 해당하는 스냅샷과 동일하며, CBS 용량을 확장할 수는 있지만 축소는 불가능합니다.
</dx-alert>



## 관련 문서
[RunInstances](https://intl.cloud.tencent.com/document/product/213/33237) API 인터페이스를 호출하여 사용자 정의 이미지로 인스턴스를 생성할 수도 있습니다.


<dx-alert infotype="explain" title="">
전체 이미지를 사용하여 인스턴스를 생성하는 경우 [DescribeImages](https://intl.cloud.tencent.com/document/product/213/33272) API를 호출하여 이미지와 연결된 스냅샷 ID를 얻고 인스턴스 생성을 위해 RunInstances API를 호출할 때 스냅샷 ID 매개변수를 전달하십시오. 그렇지 않으면 생성된 CBS와 해당 스냅샷 ID가 일치하지 않고 스냅샷 데이터를 롤백할 수 없으며 데이터 디스크에 데이터가 없어 정상적으로 마운트할 수 없습니다.
</dx-alert>
