## 작업 시나리오

CVM을 생성할 때 **사용자 정의 데이터**를 지정하여 인스턴스를 구성할 수 있습니다. CVM을 **처음 시작**할 경우 사용자 정의 데이터는 텍스트 모드로 CVM에 전달된 뒤 텍스트가 실행됩니다. 한 번에 여러 CVM을 구매할 경우 사용자 정의 데이터는 모든 CVM이 처음 시작할 때 해당 텍스트를 실행합니다.

본 문서는 Linux CVM을 처음 시작할 때 Shell 형식을 통해 전달되는 스크립트를 예시로 사용합니다.

## 주의 사항
- 사용자 정의 데이터를 지원하는 Linux 운영 체제는 다음과 같습니다.
	- 64비트 운영 체제: CentOS 6.8 64비트 이상, Ubuntu Server 14.04.1 LTS 64비트 이상, suse42.3x86_64
	- 32비트 운영 체제: CentOS 6.8 32비트 이상
- CVM을 처음 시작할 경우에만 텍스트 전달을 통해 명령어를 실행하십시오.
- 전달된 텍스트는 Base64로 인코딩되어야 합니다. **Linux 환경에서 인코딩해야 형식이 호환되지 않는 상황을 피할 수 있습니다.**
- root 계정을 사용하여 사용자 데이터가 입력된 텍스트를 실행할 경우 스크립트에서 sudo 명령어를 사용할 수 없습니다. 생성한 모든 파일은 root가 소유하기 때문에, root가 아닌 사용자의 파일 액세스 권한이 필요할 경우 스크립트에서 권한을 수정하십시오.
- 시작할 때 사용자 정의 데이터에서 지정된 작업을 실행하면 서버 시작에 소요되는 시간이 증가합니다. 작업이 완료된 후, 작업이 성공적으로 실행되는지 테스트하길 권장합니다.
- 이 예시에서 Shell 스크립트는 ‘#!’ 문자 부호와 스크립트를 읽는 인터프리터의 경로(일반적으로 ‘/bin/bash’)로 시작해야 합니다.

## 작업 단계

### Shell 스크립트 작성
1. 아래의 명령어를 실행하여 "script_text.sh"라는 Shell 스크립트 파일을 생성하십시오.
```shellsession
vi script_text.sh
```
2. **i**를 눌러 편집 모드로 바꾸고, 다음의 내용을 참조하여 “script_text.sh”를 입력한 뒤 스크립트 파일을 저장합니다.
```bash
#!/bin/bash
echo "Hello Tencent Cloud."
```
<dx-alert infotype="notice" title="">
Shell 스크립트는 ‘#!’ 문자 및 스크립트를 읽을 인터프리터의 경로(일반적으로 ‘/bin/bash’)로 시작해야 합니다. Shell 스크립트에 대한 자세한 정보는 Linux 문서 항목(tldp.org)의 [BASH 프로그래밍](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)을 참조 바랍니다.
</dx-alert>




### Base64로 스크립트 인코딩[](id:Base64Script)

1. 아래의 명령어를 실행하여 "script_text.sh" 스크립트 파일에서 Base64 인코딩 작업을 진행하십시오.
```shellsession
# 스크립트에 대한 Base64 인코딩 작업
base64 script_text.sh
```
다음의 정보를 출력합니다.
```shellsession
# 인코딩 후의 결과
IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
```
2. 아래의 명령어를 실행하여 Base64로 인코딩한 스크립트의 리턴 결과를 확인하십시오.
```shellsession
# Base64 인코딩을 진행해 리턴된 결과가 실행할 명령어가 맞는지 확인하십시오.
echo "IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==" | base64 -d
```

### 텍스트 전달

Tencent Cloud는 인스턴스를 시작하는 다양한 방법을 제공하며, 주로 다음 두 가지 경우로 나뉩니다. 사용자의 실제 필요에 따라 선택하십시오.
<dx-tabs>
::: 공식 웹 사이트 또는 콘솔을 통해 전달[](id:Consoletrans)
1. [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하여 인스턴스를 구매하고 ‘2. 호스트 설정’ 단계에서 **고급 설정**을 클릭하십시오.
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. ‘고급 설정’에서 아래와 같이 ‘사용자 정의 데이터’ 텍스트 상자에 [Base64로 인코딩된 스크립트](#Base64Script)의 리턴 결과를 입력합니다.
예를 들어 Base64로 script_text 스크립트 파일을 인코딩할 시 리턴 결과는 ‘IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==’입니다.
![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3. 인터페이스의 작업 절차에 따라 CVM 생성을 완료합니다.
<dx-alert infotype="explain" title="">
Tencent CVM는 오픈 소스 소프트웨어인 cloud-init를 통해 스크립트를 실행합니다. cloud-init와 관련된 더 자세한 내용은 [cloud-init 공식 웹 사이트](https://cloud-init.io/)를 참고하십시오.
</dx-alert>


:::
::: API를 통해 전달[](id:APItrans)
API를 통해 CVM를 생성할 경우 [Base64로 스크립트 파일 인코딩](#Base64Script)에 리턴된 인코딩 결과를 RunInstances 인터페이스의 UserData 파라미터에 할당하여 텍스트를 전달할 수 있습니다.
예를 들어 UserData 파라미터로 CVM에 대한 요청 파라미터를 생성하는 예는 다음과 같습니다.
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
  &<공통 요청 매개변수>
```

:::
</dx-tabs>

### 실행 로그 보기
서버가 성공적으로 생성되면 다음 명령을 실행하여 스크립트 실행 로그를 볼 수 있습니다.
```shellsession
cat /var/log/cloud-init-output.log
```

