## 작업 시나리오

CVM를 생성할 때 **사용자 정의 데이터**를 지정하여 인스턴스를 구성할 수 있습니다. CVM을 **처음 시작**할 경우 사용자 정의 데이터는 텍스트 모드로 CVM에 전달된 뒤 텍스트가 실행됩니다. 한 번에 여러 CVM를 구매할 경우 사용자 정의 데이터는 모든 CVM이 처음 시작할 때 해당 텍스트를 실행합니다.
본 문서는 Linux CVM를 처음 시작할 때 PowerShell 형식을 통해 전달되는 스크립트를 예시로 합니다.

## 주의사항
- 사용자 정의 데이터를 지원하는 Linux 운영 체제는 다음과 같습니다.
	- 64비트 운영 체제: CentOS 6.8 64비트 이상, Ubuntu Server 14.04.1 LTS 64비트 이상, suse42.3x86_64
	- 32비트 운영 체제: CentOS 6.8 32비트 이상
- CVM을 처음 시작할 경우에만 텍스트 전달을 통해 명령어를 실행하십시오.
- 전달된 텍스트는 Base64로 인코딩되어야 합니다. **Linux 환경에서 인코딩해야 형식이 호환되지 않는 상황을 피할 수 있습니다.**
- root 계정을 사용하여 사용자 데이터가 입력된 텍스트를 실행할 경우 스크립트에서 sudo 명령어를 사용할 수 없습니다. 생성한 모든 파일은 root가 소유하기 때문에, root가 아닌 사용자의 파일 액세스 권한이 필요할 경우 스크립트에서 권한을 수정하십시오.
- 시작할 때 사용자 정의 데이터에서 지정된 작업을 실행하면 서버 시작에 소요되는 시간이 증가합니다. 작업이 완료된 후, 작업이 성공적으로 실행되는지 테스트하길 권장합니다.
- 이 예시에서 Shell 스크립트는 ‘#!’ 문자 부호와 스크립트를 읽는 인터프리터의 경로(일반적으로 ‘/bin/bash’)로 시작해야 합니다.

## 작업 순서

### Shell 스크립트 작성
1. 아래의 명령어를 실행하여 "script_text.sh"라는 Shell 스크립트 파일을 생성하십시오.
```
vi script_text.sh
```
2. **i** 또는 **Insert**를 눌러 편집 모드로 전환한 뒤, 아래의 내용을 참조하여 "script_text.sh" 스크립트 파일을 작성하고 저장하십시오.
```
#!/bin/bash
echo "Hello Tencent Cloud."
```
> Shell 스크립트는 ‘#!’ 문장 부호와 스크립트를 읽는 인터프리터의 경로(일반적으로 ‘/bin/bash’)로 시작해야 합니다. Shell 스크립트와 관련된 더 자세한 내용은 Linux 문서화 프로젝트(tldp.org)의 [BASH 프로그래밍 방법](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)을 참조하십시오.

<span id="Base64Script"></span>
### Base64로 스크립트 파일 인코딩

1. 아래의 명령어를 실행하여 "script_text.sh" 스크립트 파일에서 Base64 인코딩 작업을 진행하십시오.
```
# 스크립트에 대한 Base64 인코딩 작업
base64 script_text.sh
```
다음의 정보가 리턴됩니다.
```
# 인코딩 후의 결과
IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
```
2. 아래의 명령어를 실행하여 Base64로 인코딩한 스크립트의 리턴 결과를 확인하십시오.
```
# Base64 인코딩을 진행해 리턴된 결과가 실행할 명령어가 맞는지 확인하십시오.
echo "IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==" | base64 -d
```

### 텍스트 전달

Tencent Cloud는 인스턴스를 시작하는 다양한 방법을 제공하며, 주로 다음 두 가지 경우로 나뉩니다. 사용자의 실제 필요에 따라 선택하십시오.
- [공식 웹 사이트 또는 콘솔을 통해 전달](#Consoletrans)
- [API를 통해 전달](#APItrans)

<span id="Consoletrans"></span>
#### 공식 웹 사이트 또는 콘솔을 통해 전달

1. [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참조하여 인스턴스를 구매하고 "4. 보안 그룹과 호스트 설정”에서 [고급 설정]을 클릭하십시오.
2. "고급 설정"의 "사용자 정의 데이터" 텍스트 상자에 [Base64로 스크립트 파일 인코딩](#Base64Script)의 인코딩 리턴 결과를 입력하십시오. 아래 이미지를 참조하십시오.
예를 들어 Base64로 script_text 스크립트 파일을 인코딩할 시 리턴 결과는 ‘IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==’입니다.
3. 인터페이스 정보 절차에 따라, CVM 생성을 완료하십시오.
> Tencent CVM는 오픈 소스 소프트웨어인 cloud-init를 통해 스크립트를 실행합니다. cloud-init와 관련된 더 자세한 내용은 [cloud-init 공식 웹 사이트](https://cloud-init.io/)를 참조하십시오.

<span id="APItrans"></span>
### API를 통해 전달

API를 통해 CVM를 생성할 경우 [Base64로 스크립트 파일 인코딩](#Base64Script)에 리턴된 인코딩 결과를 RunInstances 인터페이스의 UserData 파라미터에 할당하여 텍스트를 전달할 수 있습니다.
예를 들어 UserData 파라미터로 CVM에 대한 요청 파라미터를 생성하는 예는 다음과 같습니다.
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
  &<공유 요청 파라미터>
```
