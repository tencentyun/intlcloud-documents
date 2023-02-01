## 개요

CVM을 생성할 때 **사용자 지정 데이터**를 지정하여 인스턴스를 구성할 수 있습니다. CVM을 **처음 시작**할 경우 사용자 지정 데이터는 텍스트 형식으로 CVM에 전달되어 실행됩니다. 한 번에 여러 CVM을 구매하는 경우 사용자 지정 데이터 텍스트는 처음 실행하는 동안 모든 CVM에서 실행됩니다.

본문은 Windows CVM을 처음 실행하는 동안 PowerShell 스크립트가 전달되는 예를 설명합니다.

## 주의 사항

- 사용자 지정 데이터를 지원하는 Windows 운영 체제는 다음과 같습니다.
 - Windows Server 2019 IDC 64비트 영어 버전
 - Windows Server 2016 IDC 64비트 영어 버전
 - Windows Server 2012 R2 IDC 64비트 영어 버전
- CVM이 처음 실행될 때만 텍스트를 전달하여 명령을 실행할 수 있습니다.
- Base64 인코딩 이전에는 사용자 지정 데이터는 16KB를 초과할 수 없습니다.
- 사용자 지정 데이터는 Base64로 인코딩된 다음 전달됩니다. Base64가 아닌 스크립트 파일을 직접 복사하는 경우 ‘항목은 Base64로 인코딩된 텍스트입니다’를 선택하지 마십시오.
- 시작하는 동안 사용자 지정 데이터에서 지정된 작업을 실행하면 CVM을 시작하는 데 소요되는 시간이 늘어납니다. 몇 분 동안 기다린 후 작업이 완료되면 작업이 성공적으로 실행되었는지 테스트하는 것이 좋습니다.
- 이 예시에서는 PowerShell 레이블(예: &lt;powershell&gt;&lt;/powershell&gt; 레이블)을 사용하여 Windows PowerShell 스크립트를 지정합니다.

## 작업 단계

### 텍스트 준비

실제 요구 사항에 따라 텍스트를 준비합니다.


#### PowerShell 스크립트[](id:PowerShellScript)
PowerShell 레이블을 사용하여 PowerShell 스크립트를 준비합니다.
예를 들어 C 드라이브(C:)에 ‘Hello Tencent Cloud.’라는 내용으로 "tencentcloud.txt" 파일을 생성해야 하는 경우 PowerShell 레이블을 사용하여 다음 내용을 준비합니다.
```shell
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```


#### Base64 인코딩 스크립트[](id:Base64Script)

1. 아래의 명령어를 실행하여 ‘script_text.psl’이라는 PowerShell 스크립트 파일을 생성합니다.
```shell
vi script_text.ps1
```
2. **i**를 눌러 편집 모드로 바꾸고, 다음의 내용을 참고하여 ‘script_text.ps1’을 입력한 뒤 스크립트 파일을 저장합니다.
```shell
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```
3. 아래의 명령어를 실행하여 ‘script_text.psl’ 스크립트 파일에 Base64 인코딩 작업을 진행합니다.
```shell
base64 script_text.ps1
```
다음의 정보를 출력합니다.
```shell
PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAgQzpcdGVuY2VudGNsb3VkLnR4dAo8L3Bvd2Vyc2hlbGw+Cg==
```

### 텍스트 전달

Tencent Cloud는 인스턴스를 시작하는 다양한 방법을 제공하며, 여기서는 그 중 두 가지를 소개합니다. 요구 사항에 따라 방법을 선택하십시오.

<dx-tabs>
::: 공식 웹 사이트 또는 콘솔을 통해 전달[](id:Consoletrans)
1. [구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하여 인스턴스를 구매하고 **2. 네트워크 및 호스트 설정**의 **기타 설정**에서 **고급 설정**을 클릭합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TKin326_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221208114658.png)
2. ‘고급 설정’에서 실제 요구에 따라 ‘사용자 정의 데이터’의 텍스트 박스에 준비한 텍스트 콘텐츠를 입력합니다.
 - PowerShell 스크립트: [PowerShell 스크립트](#PowerShellScript)를 입력합니다.
 - Base64 인코딩 스크립트: 먼저 ‘상기 입력은 base64로 인코딩됨’을 선택하고 [Base64 인코딩 스크립트](#Base64Script)를 입력합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QkmS577_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221208114852.png)
3. 인터페이스의 작업 절차에 따라 CVM 생성을 완료합니다.
:::
::: API를 통해 전달[](id:APItrans)
API를 사용하여 CVM을 생성할 때 [Base64 인코딩 스크립트](#Base64Script)에서 반환된 인코딩 결과 값을 RunInstances API의 UserData 매개변수에 할당하여 텍스트를 전달할 수 있습니다.
다음은 UserData를 사용한 샘플 CVM 생성 요청입니다.
```shell
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Version=2017-03-12
&Placement.Zone=ap-guangzhou-2
&ImageId=img-pmqg1cw7
&UserData=PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAuXHRlbmNlbnRjbG91ZC50go=
&<공통 요청 매개변수>
```
:::
</dx-tabs>



### 사용자 정의 데이터 구성 검증

1. CVM에 로그인합니다.
2. 운영 체제 인터페이스에서 C 드라이브(C:\)를 열고 `tencentcloud.txt` 텍스트 파일이 있는지 확인합니다.
`tencentcloud.txt` 텍스트 파일이 있을 경우 아래 이미지와 같이 성공적으로 구성된 것입니다.
![](https://main.qcloudimg.com/raw/9f94ec922111734a489b9730d66168c3.png)


### 실행 로그 보기
스크립트 실행 로그는 `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\cloudbase-init.log` 파일에서 확인할 수 있습니다.

