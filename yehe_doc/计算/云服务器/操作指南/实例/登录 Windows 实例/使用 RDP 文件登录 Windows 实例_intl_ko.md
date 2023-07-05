<dx-alert infotype="notice" title="">
현재 기본 Windows 인스턴스 로그인 방식은 **표준 로그인 방식(WebRDP)**이며, 로컬 로그인 클라이언트를 다운로드하지 않고 콘솔을 통해 Windows 인스턴스에 원클릭 로그인할 수 있습니다. 로그인 방법은 [표준 방식을 사용하여 Windows 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/41018)을 참고하십시오.
</dx-alert>



## 작업 시나리오
RDP는 Remote Desktop Protocol의 약자로, Microsoft에서 개발한 사용자의 로컬 컴퓨터와 원격 컴퓨터의 연결 시 사용되는 멀티 터널 프로토콜입니다. Tencent Cloud는 사용자가 RDP로 Windows CVM에 로그인하는 것을 권장합니다. 본 문서에서는 RDP 파일을 사용하여 Windows 인스턴스에 로그인하는 방법에 대해 알아볼 수 있습니다.

## 지원 운영 체제
Windows, Linux 및 Mac OS 모두 RDP 방식을 사용하여 CVM에 로그인할 수 있습니다.

## 전제 조건

- Windows 인스턴스 원격 로그인을 위해 필요한 인스턴스의 관리자 계정 및 비밀번호를 획득한 상태여야 합니다.
  - 인스턴스 생성 시 시스템에서 비밀번호 랜덤 생성을 선택했다면 [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 비밀번호를 받으시기 바랍니다.
  - 로그인 비밀번호가 설정되어 있는 경우 해당 비밀번호를 사용하여 로그인하시기 바랍니다. 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하시기 바랍니다.
- CVM 인스턴스에서 공용 IP를 구매하였고, WebRDP 프록시 IP가 소스인 원격 로그인 포트(기본값: 3389)가 인스턴스와 연결된 보안 그룹에서 개방되어있어야 합니다.
  - 빠른 구성을 통해 CVM을 구매하시면 기본적으로 이미 활성화되어 있습니다.
  - 사용자 정의 구성을 통해 CVM을 구매한 경우 [RDP를 통한 Windows CVM 원격 연결 허용](https://intl.cloud.tencent.com/document/product/213/32369)을 참고하여 수동으로 개방하십시오.
- 인스턴스의 공용 네트워크 대역폭이 5Mbit/s 이상인지 확인하십시오. 그렇지 않다면 원격 데스크톱에 랙이 발생됩니다. 네트워크 대역폭 조정은 [네트워크 구성 변경](https://intl.cloud.tencent.com/document/product/213/15517)을 참고하십시오.


## 작업 단계
<dx-tabs>
::: \sRDP\s로 Windows\s 시스템 로그인[](id:windowsRDP)
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 사용된 실제 뷰 모드에 따라 작업합니다.
 - **리스트 모드**: 아래 이미지와 같이 로그인하려는 Windows CVM 우측의 **로그인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)
 - **탭 모드**: 아래 이미지와 같이 로그인하려는 Windows CVM 탭을 선택하고 **로그인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)
3. ‘표준 로그인 | Windows 인스턴스’ 창에서 **RDP 파일 다운로드**를 선택하여 RDP 파일을 로컬에 다운로드합니다.
<dx-alert infotype="explain" title="">
원격 로그인 포트를 수정했다면 RDP 파일을 수정하고 IP 주소 뒤에 `:포트`를 추가해야 합니다.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png"/>
4. 로컬에 다운로드한 RDP 파일을 더블 클릭하여 비밀번호를 입력하고 **확인**을 클릭하면 바로 Windows CVM과 원격으로 연결됩니다.
  - 시스템 기본 설정 비밀번호로 인스턴스에 로그인할 경우 [내부 메시지](https://console.cloud.tencent.com/message)에 접속하여 획득 바랍니다.
  - 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하시기 바랍니다.

:::
::: \sRDP\s로 Linux\s 시스템 로그인[](id:LinuxRDP)


<dx-alert infotype="explain" title="">
해당 원격 데스크탑을 설치하여 프로그램에 연결해야 하며, rdesktop 사용을 권장합니다. 자세한 내용은 [rdesktop 공식 안내](http://www.rdesktop.org/)를 참고 바랍니다.
</dx-alert>


1. 다음 명령어를 실행하여 시스템에 rdesktop이 설치되어 있는지 확인합니다.
```
rdesktop
```
   - rdesktop이 이미 설치되어 있다면 [4단계](#step04)를 실행합니다.
   - command not found라는 메시지가 표시된다면 rdesktop이 설치되어 있지 않다는 의미이므로 [2단계](#step02)를 실행합니다.
2. [](id:step02) 단말기에서 다음 명령어를 실행하여 rdesktop 설치 패키지를 다운로드합니다. 이 단계에서는 rdesktop 1.8.3 버전을 예시로 사용합니다.
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
최신 설치 패키지가 필요한 경우 [GitHub rdesktop 페이지](https://github.com/rdesktop/rdesktop/releases)에서 최신 설치 패키지를 검색하고 명령어 라인에서 최신 설치 경로로 바꿔줍니다.
3. rdesktop 설치 대기 리스트에서 명령어를 순서대로 실행하여 rdesktop을 압축 해제 및 설치합니다.
```
tar xvzf rdesktop-<x.x.x>.tar.gz ## x.x.x를 다운로드된 버전 번호로 변경 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. [](id:step04)다음 명령어를 실행하여 원격 Windows 인스턴스에 연결합니다.
<dx-alert infotype="explain" title="">
예시의 매개변수를 사용자 본인의 매개변수로 수정하십시오.
</dx-alert>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
   - `Administrator`는 전제 조건에서 획득한 관리자 계정입니다.
   - `<your-password>`는 사용자가 설정한 로그인 비밀번호입니다.
      시스템 기본 설정 비밀번호로 인스턴스에 로그인할 경우 [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득 바랍니다. 비밀번호를 잊으신 경우 [인스턴스 비밀번호를 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하시기 바랍니다.
   - `<hostname or IP address>`는 Windows 인스턴스의 공용 IP 또는 사용자 정의 도메인입니다. 인스턴스 공용 IP 주소 가져오기는 [공용망IP주소 읽어오기](https://intl.cloud.tencent.com/document/product/213/17940)를 참고하십시오.

:::
::: \sRDP\s로 MacOS\s 시스템 로그인[](id:MacRDP)


<dx-alert infotype="explain" title="">
- 이하의 작업은 Microsoft Remote Desktop for Mac 기준 예시입니다. Microsoft는 2017년에 Remote Desktop 클라이언트의 다운로드 링크 제공을 중단하였고, 자회사인 HockeyApp에서 Beta 버전을 배포하고 있습니다. [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac)에서 Beta 버전을 다운로드 받으실 수 있습니다.
- 다음의 작업은 Windows Server 2012 R2 운영 체제의 CVM을 예시로 사용합니다.
</dx-alert>


1. Microsoft Remote Desktop for Mac을 다운로드하여 로컬에 설치합니다.
2. 아래 이미지와 같이 MRD를 실행하고 **Add Desktop**을 클릭합니다.
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. 아래 이미지와 같이 팝업된 ‘Add Desktop’ 창에서 다음의 순서를 따라 연결을 생성합니다.
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
     1. ‘PC name’에 CVM의 공용 IP를 입력합니다. 획득 방법은 [공용망IP 주소 읽어오기](https://intl.cloud.tencent.com/document/product/213/17940)를 참고하십시오.
     2. **Add**를 클릭하여 생성을 확인합니다.
     3. 나머지 옵션은 기본 설정을 유지하고 연결 생성을 완료합니다.
    생성된 연결은 아래 이미지와 같이 창에서 바로 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. 신규 생성한 연결을 더블 클릭하여 열고, 팝업 창의 메시지를 따라 CVM 계정 및 비밀번호를 입력한 후 **Continue**를 클릭합니다.
5. 시스템 기본 설정 비밀번호로 인스턴스에 로그인할 경우 [내부 메시지](https://console.cloud.tencent.com/message)에 접속하여 획득 바랍니다.
6. 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하시기 바랍니다.
7. 아래 이미지와 같이 팝업 창에서 **Continue**를 클릭하여 연결을 확인합니다.
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
연결 성공 후 아래 이미지와 같이 Windows CVM 인터페이스가 열립니다.
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
:::
</dx-tabs>

## RDP 대역폭 제한 설명[](id:illustrate)
가용 네트워크 대역폭은 RDP를 통해 CVM에 로그인하고 사용하는 경험에 직접적인 영향을 미칩니다. 애플리케이션 및 디스플레이 해상도에 따라 네트워크 구성이 다릅니다. Microsoft는 다양한 응용 시나리오에서 RDP를 사용할 때 인스턴스에 대한 최소 대역폭 요구 사항을 제시했습니다. 다음 표를 참고하여 인스턴스의 네트워크 구성이 비즈니스 요구 사항을 충족할 수 있는지 확인하십시오. 그렇지 않으면 랙 등의 문제가 발생할 수 있습니다.


<dx-alert infotype="explain" title="">
인스턴스 대역폭을 조정해야 하는 경우 [네트워크 구성 변경](https://intl.cloud.tencent.com/document/product/213/15517)을 참고하십시오.
</dx-alert>


다음 데이터는 1920 × 1080 해상도에 적용되며, 기본 그래픽 모드 및 H.264/AVC 444 그래픽 모드의 단일 모니터 설정을 사용합니다.

<table>
<tr>
<th width="15%">솔루션</th>
<th width="19%">기본 모드</th>
<th width="19%">H.264/AVC 444 모드</th>
<th width="47%">시나리오 설명</th>
</tr>
<tr>
<td>유휴</td>
<td>0.3Kbps	</td>
<td>0.3Kbps</td>
<td>사용자 작업 일시 중지, 화면 업데이트 미발생.</td>
</tr>
<tr>
<td>Microsoft Word</td>
<td>100 - 150 Kbps</td>
<td>200 - 300 Kbps</td>
<td>사용자 Microsoft Word, 타이핑, 그래픽 붙여넣기 활용. 문서 간 전환.</td>
</tr>
<tr>
<td>Microsoft Excel</td>
<td>150 - 200Kbps</td>
<td>400 - 500Kbps</td>
<td>사용자의 Microsoft Excel 활용. 여러 수식과 차트가 포함된 셀 동시 업데이트.</td>
</tr>
<tr>
<td>Microsoft PowerPoint</td>
<td>4 - 4.5Mbps</td>
<td>1.6 - 1.8Mbps</td>
<td>사용자의 Microsoft PowerPoint, 타이핑, 붙여넣기 활용. 다양한 그래픽 수정 및 슬라이드 쇼 애니메이션 효과 사용.</td>
</tr>
<tr>
<td>Web 브라우징</td>
<td>6 - 6.5Mbps</td>
<td>0.9 - 1Mbps</td>
<td>사용자의 여러 정적/동적 이미지가 포함된 그래픽이 풍부한 웹 사이트(가로 및 세로 스크롤 페이지) 브라우징.</td>
</tr>
<tr>
<td>갤러리</td>
<td>3.3 - 3.6Mbps	</td>
<td>0.7 - 0.8Mbps</td>
<td>사용자의 갤러리 애플리케이션 사용. 이미지 조회, 확대/축소, 크기 조정 및 회전.</td>
</tr>
<tr>
<td>비디오 재생</td>
<td>8.5 - 9.5Mbps</td>
<td>2.5 - 2.8Mbps</td>
<td>사용자의 화면의 절반을 차지하는 30FPS 비디오 시청.</td>
</tr>
<tr>
<td>비디오 전체 화면 재생</td>
<td>7.5 - 8.5Mbps</td>
<td>2.5 - 3.1Mbps</td>
<td>사용자의 전체 화면으로 최대화된 30FPS 비디오 시청.</td>
</tr>
</table>

```

```