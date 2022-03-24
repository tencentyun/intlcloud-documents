## 작업 시나리오

본문은 온라인 마이그레이션 기능을 사용하여 자체 구축 데이터 센터(IDC) 또는 클라우드 플랫폼과 같은 소스 환경에서 지정된 Tencent Cloud CVM으로 원본 서버의 시스템 및 애플리케이션 등을 마이그레이션하는 작업 단계를 소개합니다.

문서에는 **콘솔 마이그레이션** 및 **툴 마이그레이션**의 두 가지 방법이 있으며 문서의 단계를 참고하여 원본 호스트를 Tencent Cloud CVM으로 마이그레이션할 수 있습니다.


<dx-alert infotype="explain" title="">
원본 서버 형식은 물리 서버, 버츄얼 머신 또는 기타 클라우드 플랫폼 CVM일 수 있습니다. 기타 클라우드 플랫폼에는 AWS, Google Cloud Platform, VMware, Alibaba Cloud, Huawei Cloud 등의 가상 컴퓨터가 있습니다.
</dx-alert>


## 작업 단계

<dx-tabs>
::: 콘솔 마이그레이션[](id:consoleMigrate)

### 준비 사항[](id:prerequisites)

- Tencent Cloud 계정이 있어야 합니다.
- 서브 계정으로 콘솔 마이그레이션하는 경우, 루트 계정을 사용하여 [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에 로그인하고 서브 계정에 'QcloudCSMFullAccess' 권한을 부여해야 합니다.
- [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 'SecretId' 및 'SecretKey'를 생성 및 획득합니다.
- 마이그레이션 툴 압축 패키지 [다운로드](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)
- 마이그레이션할 때, 현재 사용하고 있는 애플리케이션에 영향을 줄 수 있으므로, 원본 서버의 애플리케이션 사용을 잠시 중지할 것을 권장합니다. 


### 데이터 백업
- 원본 CVM: 원본 서버 스냅샷 기능 등의 방식을 선택해 데이터를 백업할 수 있습니다.
- 타깃 CVM: [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 데이터를 백업할 수 있습니다.


### 콘솔 마이그레이션 툴 가져오기
마이그레이션 툴 압축 패키지 [클릭하여 가져오기](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip).

### 마이그레이션 사전 점검

마이그레이션하기 전에 원본 호스트와 대상 CVM을 별도로 확인해야 합니다. 다음 표를 확인하십시오.

<table>
  <tr>
	<th>Linux 원본 호스트</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtio 확인 및 설치, 작업의 세부 사항은 다음을 참고하십시오. 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 시스템 Virtio 드라이버 확인</a>.</li>
		<li>실행 
		<code>which rsync</code> rsync가 설치되어 있는지 확인하는 명령어입니다. 설치되어 있지 않다면 <a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">Rsync 설치 방법</a>을 참고하여 설치를 진행하십시오.</li>
		<li>SELinux의 활성화 여부를 확인하십시오. SELinux가 활성화되어 있으면 <a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">SELinux 비활성화 방법</a>을 참고하여 비활성화하십시오.</li>
		<li>Tencent Cloud API로 마이그레이션 요청이 이루어진 후 Cloud API는 현재의 UNIX 타임을 사용하여 생성된
		Token을 검사합니다. 현재 시스템 시간이 올바른지 확인하십시오.</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">타깃 CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		스토리지 공간: 대상 CVM의 CBS(시스템 디스크 및 데이터 디스크 포함)에는 원본측에서 데이터를 로드할 수 있는 충분한 저장 공간이 있어야 합니다.</li>
		<li>보안 그룹: 443 포트 및 80 포트는 보안 그룹에서 제한할 수 없습니다.</li>
		<li>
		대역폭 설정: 더 빠른 마이그레이션을 위해 양쪽 끝의 대역폭을 최대한 늘리는 것이 좋습니다. 마이그레이션 과정에서 대략 데이터 양만큼의 트래픽 소모가 발생하게 되며, 필요한 경우 미리 네트워크 과금 모드를 변경하시기 바랍니다.</li>
		<li>
		대상 ECS와 원본 호스트의 운영 체제 유형이 동일한지 여부: 운영 체제가 일치하지 않으면 후속 이미지의 정보가 실제 운영 체제와 일치하지 않을 수 있으므로 대상 CVM의 운영 체제는 원본 호스트의 운영 체제 유형과 일치하는 것이 좋습니다. 예를 들어 CentOS
		7 시스템의 원본 호스트를 마이그레이션할 때 CentOS 7 시스템의 CVM을 마이그레이션 대상으로 선택합니다.</li>
	  </ol>
	</td>
  </tr>
</table>



<dx-alert infotype="explain" title="">
- 원본 서버는 `sudo ./go2tencentcloud_x64 --check`와 같은 툴 명령어를 사용하여 자동으로 점검할 수 있습니다.
- go2tencentcloud 마이그레이션 툴은 실행 시작 시 자동 점검하도록 기본 설정되어 있습니다. 점검 과정을 건너뛰고 강제 마이그레이션 하려면 client.json 파일의 `Client.Extra.IgnoreCheck` 필드를 `true`로 설정합니다.
- go2tencentcloud 마이그레이션 툴 세부 정보는 [마이그레이션 툴 설명](https://intl.cloud.tencent.com/document/product/213/44340)을 참고하십시오.
</dx-alert>



### 마이그레이션 시작
1. 마이그레이션 툴 go2tencentcloud.zip을 원본 호스트에 다운로드하거나 업로드하고 다음 명령을 실행하여 해당 디렉터리로 들어갑니다.
    1. 다음 명령어를 순서대로 실행하여 go2tencentcloud.zip의 압축을 풀고 디렉터리로 들어갑니다.
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. 다음 명령어를 순서대로 실행하여 go2tencentcloud_console.zip의 압축을 풀고 디렉터리로 들어갑니다.
```sh
unzip go2tencentcloud_console.zip
```
```sh
cd go2tencentcloud_console
```
2. (옵션)원본 서버에서 마이그레이션하지 않을 파일과 디렉터리를 제외합니다.  
Linux 원본 호스트에 마이그레이션할 필요가 없는 파일 또는 디렉터리가 있는 경우 [rsync_excludes_linux.txt 파일](https://intl.cloud.tencent.com/document/product/213/44340)에 추가합니다.
3. 마이그레이션할 원본을 가져옵니다.
   1. 본문은 64비트 Linux 원본 호스트를 예시로, go2tencentcloud 파일 디렉터리에 입력하고 다음 명령어를 순서대로 실행하여 root 권한으로 툴을 실행합니다.
```shell
chmod +x go2tencentcloud_x64
```
```shell
sudo ./go2tencentcloud_x64
```
안내에 따라 [준비 사항](#prerequisites)에서 얻은 계정 API 액세스 키의 'SecretId'와 'SecretKey'를 입력하고 **Enter**를 누릅니다. 아래 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png"/>
<br>마이그레이션 툴의 인터페이스에 다음 이미지와 같은 정보가 나타나면 마이그레이션 소스가 콘솔로 성공적으로 가져오기 되었음을 의미하며 콘솔로 이동하여 마이그레이션 소스를 볼 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
<br><a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">온라인 마이그레이션 콘솔</a>에 로그인하여 가져온 마이그레이션 소스가 ‘온라인’ 상태임을 확인할 수 있습니다. 아래 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
Import source server successfully 메시지가 표시되지 않으면 마이그레이션 원본 가져오기가 실패했음을 의미합니다. 로그(기본적으로 마이그레이션 툴 디렉터리의 logs/log 파일) 조회를 통해 문제를 해결한 후 마이그레이션 툴을 다시 실행한 후 마이그레이션 소스를 가져올 수 있습니다.
<dx-alert infotype="notice" title="">
마이그레이션 소스를 성공적으로 가져온 후 마이그레이션 작업이 완료될 때까지 인스턴스에서 마이그레이션 툴을 닫지 마십시오. 그렇지 않으면 마이그레이션 소스가 오프라인되고 마이그레이션 작업을 완료할 수 없습니다.
</dx-alert>

4. 온라인 마이그레이션 콘솔로 이동하여 마이그레이션 작업을 생성합니다.
    1. [온라인 마이그레이션 콘솔](https://console.cloud.tencent.com/cvm/csm/online?rid=1)에 로그인하여 대상 마이그레이션 소스가 있는 행 우측의 **마이그레이션 작업 생성**을 클릭합니다.
    2. ‘마이그레이션 작업 생성’ 팝업 창에서 [마이그레이션 작업 설정 설명](https://intl.cloud.tencent.com/document/product/213/44338)을 참고하여 설정합니다.
    예를 들어 Linux 원본 호스트를 Tencent Cloud 광저우 리전의 클라우드 서버로 마이그레이션하기 위한 마이그레이션 작업 설정은 다음 이미지와 같습니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)
5. 마이그레이션 작업 실행
<dx-alert infotype="explain" title="">
실행 예정 작업은 이 단계를 건너뛸 수 있으며, 예약된 실행 시간에 도달하면 자동으로 마이그레이션 작업이 시작됩니다.
</dx-alert>
마이그레이션 작업 생성 후 **마이그레이션 작업** 탭을 클릭하여 마이그레이션 작업을 볼 수 있습니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png)
마이그레이션 작업은 작업 행 우측의 **시작/재시도**를 클릭하여 시작할 수 있습니다. 이 때 작업 상태가 ‘마이그레이션 중’으로 변경됩니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png)
6. 마이그레이션 작업이 종료될 때까지 기다립니다.
마이그레이션 작업의 상태가 ‘성공’이면 마이그레이션이 성공적으로 완료되었음을 나타냅니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)


### 마이그레이션 사후 점검
 - 마이그레이션 결과가 실패인 경우, 로그 파일(마이그레이션 툴 디렉터리 안의 log 파일로 기본 설정)의 오류 정보 출력, 가이드 문서 또는 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 확인하여 문제를 해결하거나 복구하시기 바랍니다. 복구 후 마이그레이션 작업 열에서 **재시도**를 클릭하여 마이그레이션 작업을 다시 시작합니다.
 - 마이그레이션 성공 시, 대상 CVM이 정상적으로 실행되는지, 대상 CVM의 데이터가 소스 CVM과 일치하는지, 네트워크가 정상적인지 또는 다른 시스템 서비스가 정상적인지 등을 확인하시기 바랍니다.


문의 사항이나 마이그레이션 오류 문제 등이 있다면 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 조회하거나 [문의하기](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 해결하실 수 있습니다.

:::
::: 툴 마이그레이션[](id:toolMigrate)

### 준비 사항

- Tencent Cloud 계정이 있어야 합니다.
- 마이그레이션할 때, 현재 사용하고 있는 애플리케이션에 영향을 줄 수 있으므로, 원본 서버의 애플리케이션 사용을 잠시 중지할 것을 권장합니다. 
- [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 'SecretId' 및 'SecretKey'를 생성 및 획득합니다.
- 마이그레이션 툴 압축 패키지 [다운로드](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip).
- 원본 호스트와 타깃 CVM이 마이그레이션 조건을 충족하는지 확인합니다. 예를 들어, 타깃 CVM의 CBS에는 반드시 원본 호스트 데이터를 저장할 충분한 스토리지 용량이 확보되어야 합니다.


### 마이그레이션 툴 가져오기  

마이그레이션 툴 압축 패키지 [클릭하여 가져오기](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip).



### 데이터 백업
- 원본 CVM: 원본 서버 스냅샷 기능 등의 방식을 선택해 데이터를 백업할 수 있습니다.
- 타깃 CVM：[스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 데이터를 백업할 수 있습니다.


### 인터넷 환경에 따라 마이그레이션 시나리오 확정

소스 서버와 타깃 CVM의 네트워크 환경에 따라 적합한 이전 모델을 결정하십시오.
현재 마이그레이션 툴은 기본 모드와 내부 네트워크 마이그레이션 모드를 지원합니다. 내부 마이그레이션 모드는 3가지 시나리오로 나뉘며, 마이그레이션 모드/시나리오에 따라 소스 서버와 타깃 CMV에 대한 네트워크 요구 조건이 다릅니다. 소스 서버와 타깃 CVM이 모두 공용 네트워크로 액세스할 수 있는 경우 직접 기본 모드를 사용해 마이그레이션할 수 있으며, 소스 서버와 타깃 CVM 중 하나라도 공용 네트워크로 직접 액세스할 수 없는 경우 먼저 [VPC 피어링 연결](https://intl.cloud.tencent.com/zh/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) 또는 [Direct Connect](https://intl.cloud.tencent.com/zh/document/product/216) 등의 방법으로 연결 터널을 구축한 후 내부 네트워크 모드로 마이그레이션합니다.



### 마이그레이션 사전 점검

마이그레이션하기 전에 원본 호스트와 대상 CVM을 별도로 확인해야 합니다. 다음 표를 확인하십시오.


<table>
  <tr>
	<th style="width: 15%;">타깃 CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		스토리지 공간: 대상 CVM의 CBS(시스템 디스크 및 데이터 디스크 포함)에는 원본측에서 데이터를 로드할 수 있는 충분한 저장 공간이 있어야 합니다.</li>
		<li>보안 그룹: 443 포트 및 80 포트는 보안 그룹에서 제한할 수 없습니다.</li>
		<li>
		대역폭 설정: 더 빠른 마이그레이션을 위해 양쪽 끝의 대역폭을 최대한 늘리는 것이 좋습니다. 마이그레이션 과정에서 대략 데이터 양만큼의 트래픽 소모가 발생하게 되며, 필요한 경우 미리 네트워크 과금 모드를 변경하시기 바랍니다.</li>
		<li>
		대상 ECS와 원본 호스트의 운영 체제 유형이 동일한지 여부: 운영 체제가 일치하지 않으면 후속 이미지의 정보가 실제 운영 체제와 일치하지 않을 수 있으므로 대상 CVM의 운영 체제는 원본 호스트의 운영 체제 유형과 일치하는 것이 좋습니다. 예를 들어 CentOS
		7 시스템의 원본 호스트를 마이그레이션할 때 CentOS 7 시스템의 CVM을 마이그레이션 대상으로 선택합니다.</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th>Linux 원본 호스트</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtio 확인 및 설치, 작업의 세부 사항은 다음을 참고하십시오. 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 시스템 Virtio 드라이버 확인</a>.</li>
		<li>실행 
		<code>which rsync</code> rsync가 설치되어 있는지 확인하는 명령어입니다. 설치되어 있지 않다면 <a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">Rsync 설치 방법</a>을 참고하여 설치를 진행하십시오.</li>
		<li>SELinux의 활성화 여부를 확인하십시오. SELinux가 활성화되어 있으면 <a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">SELinux 비활성화 방법</a>을 참고하여 비활성화하십시오.</li>
		<li>Tencent Cloud API로 마이그레이션 요청이 이루어진 후 Cloud API는 현재의 UNIX 타임을 사용하여 생성된 
		Token을 검사합니다. 현재 시스템 시간이 올바른지 확인하십시오.</li>
		<li>원본 호스트의 로그인 방법을 확인합니다. AWS 원본 호스트가 SSH를 사용하는 경우 
		키 쌍 방식 로그인, 비밀번호 방식 로그인을 권장합니다.</li>
	  </ol>
	</td>
  </tr>
</table>



<dx-alert infotype="explain" title="">
- 원본 서버는 `sudo ./go2tencentcloud_x64 --check`와 같은 툴 명령어를 사용하여 자동으로 점검할 수 있습니다.
- go2tencentcloud 마이그레이션 툴은 실행 시작 시 자동 점검하도록 기본 설정되어 있습니다. 점검 과정을 건너뛰고 강제 마이그레이션 하려면 client.json 파일의 `Client.Extra.IgnoreCheck` 필드를 `true`로 설정합니다.
- go2tencentcloud 마이그레이션 툴 세부 정보는 [마이그레이션 툴 설명](https://intl.cloud.tencent.com/document/product/213/44340)을 참고하십시오.
</dx-alert>



### 마이그레이션 시작

1. (옵션)원본 서버와 타깃 CVM의 연결 터널을 구축합니다. 
  - [내부 네트워크 마이그레이션 모드](https://intl.cloud.tencent.com/document/product/213/44341)를 선택하는 경우 [VPC 피어링 연결](https://intl.cloud.tencent.com/zh/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) 또는 [Direct Connect](https://intl.cloud.tencent.com/zh/document/product/216) 등의 방법으로 소스 서버와 타깃 CVM 간의 연결 터널을 구축해야 합니다.
  - [공용 네트워크 마이그레이션 모드](https://intl.cloud.tencent.com/document/product/213/44340)를 선택한 경우 이 단계를 건너뛰십시오.
2. 마이그레이션 툴 go2tencentcloud.zip을 원본 호스트에 다운로드하거나 업로드하고 다음 명령을 실행하여 해당 디렉터리로 들어갑니다.
    1. 다음 명령어를 순서대로 실행하여 go2tencentcloud.zip의 압축을 풀고 디렉터리로 들어갑니다.
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. 다음 명령어를 순서대로 실행하여 go2tencentcloud_tool.zip의 압축을 풀고 디렉터리로 들어갑니다.
```sh
unzip go2tencentcloud_tool.zip
```
```sh
cd go2tencentcloud_tool
```
3. `user.json` 파일을 설정합니다.
`user.json`은 소스 서버와 타깃 CVM을 설정하는 파일로, 설정 항목은 다음과 같습니다.
  - 계정 API 호출 키 SecretId와 SecretKey. 자세한 정보는 [액세스 키](https://intl.cloud.tencent.com/document/product/598/32675)를 참고하십시오.
  - 타깃 CVM 소재 리전. CVM 리전 관련 내용은 [리전 및 가용존](https://intl.cloud.tencent.com/document/product/213/6091)을 참고하십시오.
  - 타깃 CVM 인스턴스 ID. [인스턴스 리스트](https://console.cloud.tencent.com/cvm/instance/index?rid=1) 페이지에서 확인할 수 있습니다.
  - 소스 서버 데이터 디스크 설정(선택사항)  
4. `client.json` 파일을 설정합니다.
`client.json`은 마이그레이션 모드와 기타 마이그레이션 설정 항목을 설정하는 파일입니다. 어떤 마이그레이션 시나리오를 선택하든 client.json의 `Client.Net.Mode` 항목에 상응하는 매개변수 값을 설정해야 합니다.
5. (옵션)원본 서버에서 마이그레이션하지 않을 파일과 디렉터리를 제외합니다.  
Linux 원본 호스트에 마이그레이션할 필요가 없는 파일 또는 디렉터리가 있는 경우 [rsync_excludes_linux.txt 파일](https://intl.cloud.tencent.com/document/product/213/44340)에 추가합니다.
6. 툴을 실행합니다.
예를 들어 64비트 Linux 원본 호스트에서 go2tencentcloud 파일 디렉터리에 입력하고 다음 명령어를 실행하여 root 권한으로 툴을 실행합니다.
```
sudo ./go2tencentcloud_x64
```
툴을 실행한 후, 마이그레이션 과정이 완료될 때까지 기다려 주시기 바랍니다.
마이그레이션 성공 시 콘솔에 출력되는 내용은 다음 이미지와 같습니다.
 ![](https://main.qcloudimg.com/raw/238ce694355a59836762df4f9a716f6f.png)



### 마이그레이션 사후 점검
 - 마이그레이션 결과가 실패인 경우, 로그 파일(마이그레이션 툴 디렉터리 안의 log 파일로 기본 설정)의 오류 정보 출력, 가이드 문서 또는 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 확인하여 문제를 해결하거나 복구하시기 바랍니다. 복구 후 마이그레이션 작업 작업 열에서 **시작/재시도**를 클릭하여 마이그레이션 작업을 다시 시작합니다.
 - 마이그레이션 성공 시, 대상 CVM이 정상적으로 실행되는지, 대상 CVM의 데이터가 소스 CVM과 일치하는지, 네트워크가 정상적인지 또는 다른 시스템 서비스가 정상적인지 등을 확인하시기 바랍니다.


문의 사항이나 마이그레이션 오류 문제 등이 있다면 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 조회하거나 [문의하기](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 해결하실 수 있습니다.

:::
</dx-tabs>









