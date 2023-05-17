## 작업 시나리오

본문은 CVM 콘솔의 **프라이빗 네트워크** 모드에서 온라인 마이그레이션을 통해 IDC 또는 클라우드 플랫폼의 소스 서버에서 CVM으로 시스템 및 애플리케이션을 마이그레이션하는 방법을 설명합니다.

공용 네트워크 마이그레이션에 비해 내부 네트워크 마이그레이션은 전송 속도가 빨라 마이그레이션 효율성이 크게 향상되고 원본 시스템의 공용 네트워크 액세스 기능에 제한이 없으며 마이그레이션을 유연하게 구성할 수 있습니다.


## 준비 사항[](id:prerequisites)
- Tencent Cloud 계정이 있어야 합니다.
- 서브 계정으로 콘솔 마이그레이션하는 경우, 루트 계정을 사용하여 [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에 로그인하고 서브 계정에 'QcloudCSMFullAccess' 권한을 부여해야 합니다.
- [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 'SecretId' 및 'SecretKey'를 생성 및 획득합니다.
- 마이그레이션 툴 압축 패키지를 [다운로드](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)합니다.
- 마이그레이션할 때, 현재 사용하고 있는 애플리케이션에 영향을 줄 수 있으므로, 원본 서버의 애플리케이션 사용을 잠시 중지할 것을 권장합니다.


## 작업 단계

### 데이터 백업
- 원본 호스트: 원본 서버 스냅샷 기능 등의 방식을 선택해 데이터를 백업할 수 있습니다.
- 타깃 CVM: [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 데이터를 백업할 수 있습니다.

### 콘솔 마이그레이션 툴 가져오기  
마이그레이션 툴 압축 패키지를 [가져오기](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)합니다.

### 인터넷 환경에 따라 마이그레이션 시나리오 확정

소스 서버와 타깃 CVM의 네트워크 환경에 따라 적절한 마이그레이션 모드를 선택합니다.
현재 CVM 콘솔은 공용 및 프라이빗 네트워크 모드에서 온라인 마이그레이션을 지원합니다. 프라이빗 네트워크 모드는 세 가지 시나리오에 적용됩니다. 각 마이그레이션 모드 또는 시나리오에는 원본 서버 및 대상 CVM에 대한 네트워크 요구 사항이 다릅니다. 원본 서버와 타깃 CVM이 모두 공용 네트워크에 액세스할 수 있는 경우 마이그레이션에 기본 모드를 사용할 수 있습니다. 소스 서버 또는 타깃 CVM이 공용 네트워크에 직접 액세스할 수 없는 경우 마이그레이션을 위해 프라이빗 네트워크 모드를 사용하기 전에 [Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) 또는 [Direct Connect](https://intl.cloud.tencent.com/document/product/216)를 통해 둘 사이에 연결을 설정해야 합니다.

### 마이그레이션 사전 점검
마이그레이션하기 전에 실제 상황에 따라 다음 표의 내용을 확인하십시오.
- 마이그레이션 타깃이 CVM인 경우 원본 호스트와 타깃 CVM을 확인해야 합니다.
- 마이그레이션 타깃이 CVM 이미지인 경우 원본 호스트만 확인하면 됩니다.

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
	<th style="width: 15%;">타깃 CVM(옵션)</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		스토리지 공간: 타깃 CVM의 CBS(시스템 디스크 및 데이터 디스크 포함)에는 원본측에서 데이터를 로드할 수 있는 충분한 저장 공간이 있어야 합니다.</li>
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


## 마이그레이션 시작
1. 원본 서버와 Tencent Cloud 간에 프라이빗 네트워크 연결을 설정합니다.
 - 마이그레이션 대상이 CVM인 경우 [Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037) 또는 [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003)를 사용하여 원본 서버와 대상 CVM 간의 연결을 설정합니다.
 - 마이그레이션 대상이 CVM 이미지인 경우[Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037) 또는 [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003)를 사용하여 원본 서버와 Tencent Cloud VPC 간의 연결을 설정합니다.
2. 마이그레이션 툴 go2tencentcloud.zip을 원본 호스트에 다운로드하거나 업로드하고 다음 명령을 실행하여 해당 디렉터리로 들어갑니다.
 i. 다음 명령어를 순서대로 실행하여 go2tencentcloud.zip의 압축을 풀고 디렉터리로 들어갑니다.
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
 ii. 다음 명령어를 순서대로 실행하여 go2tencentcloud-linux.zip의 압축을 풀고 디렉터리로 들어갑니다.
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
 `go2tencentcloud` 디렉터리에 있는 파일은 마이그레이션되지 않으므로 이 디렉터리에 마이그레이션할 파일을 두지 마십시오.
</dx-alert>

3. (옵션)원본 서버에서 마이그레이션하지 않을 파일과 디렉터리를 제외합니다. 
Linux 원본 호스트에 마이그레이션할 필요가 없는 파일 또는 디렉터리가 있는 경우 [rsync_excludes_linux.txt 파일](https://intl.cloud.tencent.com/document/product/213/44340)에 추가합니다.

4. (옵션) 네트워크 프록시를 설정합니다.
 - 마이그레이션이 [프라이빗 마이그레이션 모드: 시나리오 2](https://intl.cloud.tencent.com/document/product/213/44340)인 경우 이 단계를 건너뛰십시오.
 - 마이그레이션이 [프라이빗 마이그레이션 모드: 시나리오 3](https://intl.cloud.tencent.com/document/product/213/44340)인 경우 프록시 네트워크의 IP 주소와 포트를 구성합니다.
    - `client.json` 파일의 `Client.Net.Proxy.Ip`와 `Client.Net.Proxy.Port`를 네트워크 프록시의 IP 주소와 포트로 설정해야 합니다.
    - 네트워크 프록시 확인이 필요한 경우 `Client.Net.Proxy.User` 및 `Client.Net.Proxy.Password`에 네트워크 프록시의 사용자 이름과 비밀번호를 입력합니다.

5. 마이그레이션 소스를 가져옵니다.
 i. 예를 들어 64비트 Linux 소스 서버에서 root 사용자로 다음 명령을 순서대로 실행하여 도구를 실행합니다.
```shellsession
chmod +x go2tencentcloud_x64
```
```shellsession
sudo ./go2tencentcloud_x64
```
 ii.안내에 따라 [준비 사항](#prerequisites)에서 얻은 계정 API 액세스 키의 'SecretId'와 'SecretKey'를 입력하고 **Enter**를 누릅니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6e38d7e0487da4a2f6fd001e9953466a.png)
마이그레이션 툴 인터페이스에 다음 이미지와 같은 정보가 나타나면 마이그레이션 소스를 콘솔로 성공적으로 가져온 것이므로 콘솔로 이동하여 마이그레이션 소스를 볼 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9261d9c0ce1789c1b7afa1accd6bf884.png"/>
<a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">온라인 마이그레이션 콘솔</a>에 로그인하여 가져온 마이그레이션 소스가 ‘온라인’ 상태인 것을 볼 수 있습니다. 아래 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
Import source server successfully 메시지가 표시되지 않으면 마이그레이션 원본을 가져오지 못한 것이므로 문제 해결을 위해 로그(기본적으로 마이그레이션 도구 디렉터리에 있는 logs/log 파일)를 볼 수 있습니다. 그런 다음 마이그레이션 도구를 실행하여 마이그레이션 소스를 다시 가져옵니다.
<dx-alert infotype="notice" title="">
마이그레이션 소스를 성공적으로 가져온 후 마이그레이션 작업이 완료될 때까지 인스턴스에서 마이그레이션 툴을 닫지 마십시오. 그렇지 않으면 마이그레이션 소스가 오프라인되어 마이그레이션 작업을 완료할 수 없습니다.
</dx-alert>

6. 온라인 마이그레이션 콘솔로 이동하여 마이그레이션 작업을 생성합니다.
 i. [온라인 마이그레이션 콘솔](https://console.cloud.tencent.com/cvm/csm/online?rid=1)에 로그인하여 대상 마이그레이션 소스가 있는 행 우측의 **마이그레이션 작업 생성**을 클릭합니다.
 ii. ‘마이그레이션 작업 생성’ 팝업 창에서 [마이그레이션 작업 설정 설명](https://intl.cloud.tencent.com/document/product/213/44338)을 참고하여 설정합니다.
예를 들어 내부 네트워크를 사용하여 Linux 원본 호스트를 Tencent Cloud 상하이 리전으로 마이그레이션하고 대상 CVM 이미지를 생성하는 경우, 마이그레이션 작업 설정은 다음 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)

7. 마이그레이션 작업을 실행합니다.
<dx-alert infotype="explain" title="">
실행 예정 작업은 이 단계를 건너뛸 수 있으며, 예약된 실행 시간에 도달하면 자동으로 마이그레이션 작업이 시작됩니다.
</dx-alert>
마이그레이션 작업 생성 후 <b>마이그레이션 작업</b> 탭을 클릭하여 마이그레이션 작업을 볼 수 있습니다. 아래 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
마이그레이션 작업은 작업 행 오른쪽에 있는 <b>시작/재시도</b>를 클릭하고 팝업 확인 창에서 <b>확인</b>을 클릭하여 마이그레이션 작업을 시작합니다. 이 때 작업 상태가 ‘마이그레이션 중’으로 변경됩니다. 아래 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>

8. 마이그레이션 작업이 완료될 때까지 기다립니다.
마이그레이션 작업의 상태가 ‘성공’이면 마이그레이션이 성공적으로 완료되었음을 나타냅니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)
<dx-alert infotype="explain" title="">
데이터 전송 시간은 원본 데이터 크기, 네트워크 대역폭 등 요인의 영향을 받으므로 마이그레이션이 완료될 때까지 기다려 주십시오. 마이그레이션 툴은 데이터 전송의 체크포인트 재시작을 지원합니다.
</dx-alert>

### 마이그레이션 사후 점검

- **마이그레이션 실패**:
로그 파일(마이그레이션 툴 디렉터리 안의 log 파일로 기본 설정)의 오류 정보, 가이드 문서 또는 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 확인하여 문제를 해결하거나 복구하시기 바랍니다. 복구 후 마이그레이션 작업 열에서 **시작/재시도**를 클릭하여 마이그레이션 작업을 다시 시작합니다.
- **마이그레이션 성공**:
 - 마이그레이션 대상이 CVM인 경우, 정상 실행 여부, 데이터가 원본 호스트와 일치하는지, 네트워크 정상 여부 또는 다른 시스템 서비스의 정상 여부 등을 확인하시기 바랍니다.
 - 마이그레이션 타깃이 CVM 이미지인 경우 마이그레이션 작업이 있는 행의 ‘CVM 이미지 ID’를 클릭하여 [CVM 이미지 페이지](https://console.cloud.tencent.com/cvm/image/index)로 이동하여 이미지 정보를 볼 수 있으며, 이미지를 활용하여 CVM을 생성할 수 있습니다.

문의 사항이나 마이그레이션 오류 문제 등이 있다면 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 조회하거나 [문의하기](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 해결하실 수 있습니다.
