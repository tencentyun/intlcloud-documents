## 작업 시나리오
본문은 온라인 마이그레이션 툴에서 **내부 네트워크 마이그레이션** 모드를 사용하여 자체 구축 데이터 센터(IDC) 또는 클라우드 플랫폼과 같은 소스 환경에서 Tencent Cloud CVM으로 원본 서버의 시스템 및 애플리케이션을 마이그레이션 작업 단계를 소개합니다.

공용 네트워크 마이그레이션에 비해 내부 네트워크 마이그레이션은 전송 속도가 빨라 마이그레이션 효율성이 크게 향상되고 원본 시스템의 공용 네트워크 액세스 기능에 제한이 없으며 마이그레이션을 유연하게 구성할 수 있습니다.


## 준비 사항

- Tencent Cloud 계정과 대상 CVM이 있어야 합니다.
- 마이그레이션할 때, 현재 사용하고 있는 애플리케이션에 영향을 줄 수 있으므로, 원본 서버의 애플리케이션 사용을 잠시 중지할 것을 권장합니다. 
- [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 'SecretId' 및 'SecretKey'를 생성 및 획득합니다.
- 원본 호스트와 타깃 CVM이 마이그레이션 조건을 충족하는지 확인합니다. 예를 들어, 타깃 CVM의 CBS에는 반드시 원본 호스트 데이터를 저장할 충분한 스토리지 용량이 확보되어야 합니다.


## 작업 단계

### 데이터 백업
- 원본 CVM: 원본 서버 스냅샷 기능 등의 방식을 선택해 데이터를 백업할 수 있습니다.
- 타깃 CVM：[스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 데이터를 백업할 수 있습니다.


### 마이그레이션 툴 가져오기  
마이그레이션 툴 압축 패키지 [클릭하여 가져오기](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip).


### 인터넷 환경에 따라 마이그레이션 시나리오 확정
소스 서버와 타깃 CVM의 네트워크 환경에 따라 적합한 이전 모델을 결정하십시오.
현재 마이그레이션 툴은 공용 네트워크 마이그레이션 모드와 내부 네트워크 마이그레이션 모드를 지원합니다. 내부 마이그레이션 모드는 3가지 시나리오로 나뉘며, 마이그레이션 모드/시나리오에 따라 소스 서버와 타깃 CMV에 대한 네트워크 요구 조건이 다릅니다. 소스 서버와 타깃 CVM이 모두 공용 네트워크로 액세스할 수 있는 경우 직접 기본 모드를 사용해 마이그레이션할 수 있으며, 소스 서버와 타깃 CVM 중 하나라도 공용 네트워크로 직접 액세스할 수 없는 경우 먼저 [VPC 피어링 연결](https://intl.cloud.tencent.com/zh/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) 또는 [Direct Connect](https://intl.cloud.tencent.com/zh/document/product/216) 등의 방법으로 연결 터널을 구축한 후 내부 네트워크 모드로 마이그레이션합니다.

### 마이그레이션 사전 점검

마이그레이션하기 전에 원본 호스트와 대상 CVM을 확인해야 합니다. 다음 표를 확인하십시오.


<table>
  <tr>
	<th style="width: 15%;">대상 CVM</th>
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
내부 네트워크 마이그레이션 모드의 시나리오별 작업 단계는 다음과 같습니다.

<dx-tabs>

::: 시나리오1

1. 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다.
[VPC 피어링 연결](https://intl.cloud.tencent.com/zh/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) 등의 방법으로 원본 호스트와 타깃 CVM의 연결 터널을 생성합니다.
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
3. `user.json` 파일에 타깃 CVM을 설정합니다.
[user.json 파일 매개변수 설명](https://intl.cloud.tencent.com/document/product/213/44340)에 따라 필수 항목과 필수 항목의 값을 설정하십시오.
4. `client.json` 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
`client.json` 파일의 `Client.Net.Mode` 항목을 `1`, 즉 [내부 네트워크 마이그레이션 모드: 시나리오1](https://intl.cloud.tencent.com/document/product/213/44340)의 마이그레이션으로 설정합니다. 또한, 다른 항목을 설정하려면 [client.json 파일 매개변수 설명](https://intl.cloud.tencent.com/document/product/213/44340)에 따라 설정하십시오.
5. (옵션)원본 호스트에서 마이그레이션하지 않을 파일 또는 디렉터리를 제외합니다.
Linux 원본 호스트에 마이그레이션할 필요가 없는 파일 또는 디렉터리가 있는 경우 [rsync_excludes_linux.txt 파일](https://intl.cloud.tencent.com/document/product /213/44340)에 추가합니다.
6. [](id:Scenario1_step05)게이트웨이같이 공용 네트워크에 액세스할 수 있는 호스트에서 툴을 실행합니다.
예를 들어, 공용 네트워크에 액세스할 수 있는 CVM에서 다음 명령어로 툴을 실행하여, 1단계 마이그레이션을 진행합니다.
```sh
chmod +x go2tencentcloud_x64
sudo ./go2tencentcloud_x64
```
`Stage 1 is finished and please run next stage at source machine.`라는 문구가 출력되면, 1단계 마이그레이션이 완료되었다는 의미입니다. 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)
7. [](id:Scenario1_step06)마이그레이션 대기 중인 원본 호스트에서 툴을 실행합니다.
[과정5](#Scenario1_step05)(1단계)가 완료되면, 1단계의 모든 툴 목록을 마이그레이션할 소스 CVM에 복사한 뒤, 다시 툴을 실행하여 2단계 마이그레이션을 진행합니다.
예를 들어, 다음 명령어로 툴을 실행하여 2단계 마이그레이션을 진행합니다.
```sh
sudo ./go2tencentcloud_x64
```
`Stage 2 is finished and please run next stage at gateway machine.`라는 문구가 제시되면, 2단계 마이그레이션이 완료되었다는 의미입니다. 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
8. 게이트웨이같이 공용 네트워크에 액세스할 수 있는 호스트에서 툴을 실행합니다.
[과정6](#Scenario1_step06)(2단계)가 완료되면, 2단계의 모든 툴 목록을 1단계의 CVM에 복사한 뒤, 다시 툴을 실행하여 3단계 마이그레이션을 진행합니다.
예를 들어, 다음 명령어로 툴을 실행하여 3단계 마이그레이션을 진행합니다.
```sh
sudo ./go2tencentcloud_x64
```
`Migrate successfully.`라는 문구가 출력되면, 모든 마이그레이션 작업이 완료되었다는 의미입니다. 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)

:::
::: 시나리오2

1. 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다.
[VPC 피어링 연결](https://intl.cloud.tencent.com/zh/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) 등의 방법으로 원본 호스트와 타깃 CVM의 연결 터널을 생성합니다.
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
3. `user.json` 파일에 타깃 CVM을 설정합니다.
 [user.json 파일 매개변수 설명](https://intl.cloud.tencent.com/document/product/213/44340)에 따라 필수 항목과 필수 항목의 값을 설정하십시오.
4. `client.json` 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
 `client.json` 파일의 `Client.Net.Mode` 항목을 `2`, 즉 [내부 네트워크 마이그레이션 모드: 시나리오2](https://intl.cloud.tencent.com/document/product/213/44340)의 마이그레이션으로 설정합니다. 또한, 다른 항목을 설정하려면 [client.json 파일 매개변수 설명](https://intl.cloud.tencent.com/document/product/213/44340)에 따라 설정하십시오.
5. (옵션)원본 호스트에서에서 마이그레이션하지 않을 파일 또는 디렉터리를 제외합니다.
Linux 원본 호스트에 마이그레이션할 필요가 없는 파일 또는 디렉터리가 있는 경우 [rsync_excludes_linux.txt 파일](https://intl.cloud.tencent.com/document/product /213/44340)에 추가합니다.
6. 툴을 실행합니다.
예를 들어, 64비트 Linux 소스 서버에서는 root 권한으로 다음 명령어를 실행하여 툴을 실행합니다.
```sh
sudo ./go2tencentcloud_x64
```
툴을 실행한 후, 마이그레이션 과정이 완료될 때까지 기다려 주시기 바랍니다.
마이그레이션 성공 시 콘솔에 출력되는 정보는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)



:::

::: 시나리오3

1. 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다.
[VPC 피어링 연결](https://intl.cloud.tencent.com/zh/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) 등의 방법으로 원본 호스트와 타깃 CVM의 연결 터널을 생성합니다.
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
3. `user.json` 파일에 타깃 CVM을 설정합니다.
    [user.json 파일 매개변수 설명](https://intl.cloud.tencent.com/document/product/213/44340)에 따라 필수 항목과 필수 항목의 값을 설정하십시오.
4. `client.json` 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
    `client.json` 파일의 `Client.Net.Mode` 항목을 `3`, 즉 [내부 네트워크 마이그레이션 모드: 시나리오3](https://intl.cloud.tencent.com/document/product/213/44340)의 마이그레이션으로 설정합니다.
    2. `client.json` 파일 안의 `Client.Net.Proxy.Ip`와 `Client.Net.Proxy.Port` 항목을 네트워크 프록시의 IP 주소 및 포트로 설정합니다.
        네트워크 프록시에 대한 인증이 필요하다면 `Client.Net.Proxy.User`와 `Client.Net.Proxy.Password` 항목에 네트워크 프록시의 사용자 이름과 비밀번호를 입력해야 합니다. 인증이 필요하지 않다면 입력하지 않아도 됩니다. 이외에 다른 항목을 설정해야 한다면 [client.json 파일 매개변수 설명](https://intl.cloud.tencent.com/document/product/213/44340)에 따라 설정하시기 바랍니다.
5. (옵션)원본 호스트에서 마이그레이션하지 않을 파일 또는 디렉터리를 제외합니다.
Linux 원본 호스트에 마이그레이션할 필요가 없는 파일 또는 디렉터리가 있는 경우 [rsync_excludes_linux.txt 파일](https://intl.cloud.tencent.com/document/product /213/44340)에 추가합니다.
6. 툴을 실행합니다.
예를 들어, 64비트 Linux 소스 서버에서는 root 권한으로 다음 명령어를 실행하여 툴을 실행합니다.
```sh
sudo ./go2tencentcloud_x64
```
툴을 실행한 후, 마이그레이션 과정이 완료될 때까지 기다려 주시기 바랍니다.
마이그레이션 성공 시 콘솔에 출력되는 내용은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)

:::

</dx-tabs>



### 마이그레이션 사후 점검

- 마이그레이션 결과가 실패인 경우, 로그 파일(마이그레이션 툴 디렉터리 안의 log 파일로 기본 설정)의 오류 정보 출력, 가이드 문서 또는 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)을 확인하여 문제를 해결하거나 복구하시기 바랍니다.
- 마이그레이션 성공 시, 대상 CVM이 정상적으로 실행되는지, 대상 CVM의 데이터가 소스 CVM과 일치하는지, 네트워크가 정상적인지 또는 다른 시스템 서비스가 정상적인지 등을 확인하시기 바랍니다.

문의 사항이나 마이그레이션 오류 문제 등이 있다면 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 조회하거나 [문의하기](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 해결하실 수 있습니다.











