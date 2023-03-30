본문은 Tencent Cloud IM(Instant Messaging) Demo(Unreal Engine)를 빠르게 실행하는 방법을 소개합니다.

>?현재 Windows, macOS, iOS, Android를 지원합니다.

## 환경 요건
Unreal Engine 4.27.1 이상 버전 권장.
<table>
   <tr>
      <th width="0px" style="text-align:center">개발측</td>
      <th width="0px" style="text-align:center">환경</td>
   </tr>
   <tr>
      <td>Android</td>
      <td><li>Android Studio 4.0 이상 버전.</li><li>Visual Studio 2017 15.6 이상 버전. </li><li>기기 디버깅만 지원됩니다.                    </li></td>
   </tr>
   <tr>
      <td>iOS & macOS</td>
      <td><li>Xcode 11.0 이상 버전.                   </li><li>OSX 시스템 버전은 10.11 이상 버전이 필요합니다.       </li><li>프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.   </li></td>
   </tr>
   <tr>
      <td>Windows</td>
      <td><li>운영 체제: Windows 7 SP1 이상 버전(x86-64 기반 64비트 운영 체제).                    </li><li>디스크 공간: IDE 및 일부 툴 설치 외에 최소 1.64GB의 공간이 있어야 합니다.                            </li><li><a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Visual Studio 2019</a>를 설치합니다.        </li></td>
   </tr>
</table>

## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.

## 작업 단계
[](id:step1)
### 1단계: 신규 애플리케이션 생성
1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인합니다.
>?이미 애플리케이션이 있는 경우 SDKAppID를 기록하고 [키 정보 가져오기](#step2)를 합니다.
>동일한 Tencent Cloud 계정으로 최대 300개의 IM 애플리케이션을 만들 수 있습니다. 이미 300개의 애플리케이션이 있는 경우 신규 애플리케이션 생성 전에 사용하지 않는 애플리케이션을 [비활성화 및 삭제](https://intl.cloud.tencent.com/document/product/1047/34540)합니다. **애플리케이션 삭제 후에는 SDKAppID에 해당하는 모든 데이터 및 서비스를 복구할 수 없으므로 주의하시기 바랍니다.**
>
2. **애플리케이션 생성**을 클릭하고 **애플리케이션 생성** 대화 상자에 애플리케이션 이름을 입력하고 **확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. 애플리케이션 생성 후, 콘솔 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 생성 시간, 태그 및 만료 시간을 확인할 수 있습니다. SDKAppID 정보를 저장하십시오.
![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)

[](id:step2)

### 2단계: 키 정보 가져오기
1. 대상 애플리케이션 카드를 클릭하여 애플리케이션의 기본 구성 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)
2. **기본 정보** 섹션에서 **키 표시**를 클릭하고 키 정보를 복사 및 저장합니다.
>!키 정보가 유출되지 않도록 잘 보관하십시오.

[](id:step3)
### 3단계: Demo 프로그래밍 파일 설정
1. IM Demo 프로젝트 다운로드 특정 다운로드 주소는 [Demo 다운로드](https://github.com/tencentyun/IMUnrealEngine)를 참고하십시오(문의 사항은 QQ 그룹 번호: 764231117 추가 후 상담).
2. `/IM_Demo/Source/debug/include/DebugDefs.h` 파일을 찾아 엽니다.
3. `DebugDefs.h` 파일에서 관련 매개변수를 설정합니다.
<ul><li/>SDKAPPID: 기본값 0 , 실제 SDKAppID로 설정하십시오.
	<li/>SECRETKEY: 기본값 ‘ ’ , 실제 키 정보로 설정하십시오.</ul>


>?
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로만 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.

[](id:step4)
### 4단계: 컴파일 패키지 실행
1. 더블 클릭하여 `/IM_Demo/IM_Demo.uproject`를 엽니다.
2. 컴파일 실행 디버깅:
<dx-tabs>
::: macOS\s
**File** -> **Package Project** -> **Mac**
:::
::: Windows\s
**File**->**Package Project**->**Windows**->**Windows(64-bit)**
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s
프로젝트 패키지
**File** -> **Package Project** -> **iOS**
:::
:::  Android\s
1. 개발 디버깅: 자세한 내용은 [Android 시작하기](https://docs.unrealengine.com/4.27/en/SharingAndReleasing/Mobile/Android/GettingStarted/)를 참고하십시오.
2. 패키징 프로젝트: 자세한 내용은 [Android 프로젝트 패키징](https://docs.unrealengine.com/4.27/en/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/)을 참고하십시오.
:::
</dx-tabs>

## IM Unreal Engine API 문서
자세한 인터페이스 소개는 [API 개요](https://im.sdk.qcloud.com/doc/en/md_introduction_CPP%E6%A6%82%E8%A7%88.html)를 참고하십시오.

## FAQ

### Android ‘Attempt to construct staged filesystem reference from absolute path"’오류 보고
UE4 프로젝트를 비활성화하고 CMD를 열어 다음 명령을 실행합니다.

<dx-codeblock>
:::  cmd
adb shell

cd sdcard

ls (you should see the UE4Game directory listed)

rm -r UE4Game
:::
</dx-codeblock>

프로젝트를 다시 컴파일합니다.
