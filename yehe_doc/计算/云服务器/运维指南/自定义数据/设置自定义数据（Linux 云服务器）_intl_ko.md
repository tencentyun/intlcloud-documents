## 작업 시나리오

CVM을 생성할 때 **사용자 정의 데이터**를 지정하여 인스턴스를 구성할 수 있습니다. CVM을 **처음 시작**할 경우 사용자 정의 데이터가 텍스트 형식으로 CVM에 전달된 뒤 해당 텍스트가 실행됩니다. 한 번에 여러 CVM을 구매할 경우 모든 CVM을 처음 시작하는 순간에 사용자 정의 데이터가 해당 텍스트를 실행합니다.
본 문서는 Linux CVM을 처음 시작할 때 Shell 형식을 통해 전달되는 스크립트를 예시로 사용합니다.

## 주의 사항
- 사용자 정의 데이터를 지원하는 Linux 운영 체제는 다음과 같습니다.
	- 64비트 운영 체제: CentOS 6.8 64비트 이상, Ubuntu Server 14.04.1 LTS 64비트 이상, suse42.3x86_64
	- 32비트 운영 체제: CentOS 6.8 32비트 이상
- CVM을 처음 시작할 때에만 텍스트 전달을 통해 명령어를 실행합니다.
- 전달한 텍스트는 Base64로 인코딩되어야 합니다. **Linux 환경에서 인코딩해야 형식이 호환됩니다.**.
- root 계정을 사용하여 사용자 데이터에 입력한 텍스트를 실행하며, 스크립트에서 sudo 명령어를 사용하지 않습니다. 생성한 모든 파일은 root에 귀속되므로, 다른 사용자에게 파일 액세스 권한이 필요하다면 스크립트에서 권한을 수정하시기 바랍니다.
- 시작 시 사용자 정의 데이터에 지정된 작업을 실행하면 서버 시작에 소요되는 시간이 길어질 수 있습니다. 작업이 완료될 때까지 기다렸다가 성공적으로 실행되는지 테스트하시길 권장합니다.
- 본 예시에서 Shell 스크립트는 ‘#!’ 문자 및 스크립트를 읽을 인터프리터의 경로(일반적으로 ‘/bin/bash’)로 시작해야 합니다.

## 작업 순서

### Shell 스크립트 작성
1. 다음 명령어를 실행하여 "script_text.sh"라는 이름의 Shell 스크립트 파일을 생성합니다.
```
vi script_text.sh
```
2. **i**를 눌러 편집 모드로 바꾸고, 다음의 내용을 참조하여 “script_text.sh”를 입력한 뒤 스크립트 파일을 저장합니다.
```
#!/bin/bash
echo "Hello Tencent Cloud."
```
- Shell 스크립트는 ‘#!’ 문자 및 스크립트를 읽을 인터프리터의 경로(일반적으로 ‘/bin/bash’)로 시작해야 합니다. Shell 스크립트에 대한 자세한 정보는 Linux 문서 항목(tldp.org)의 [BASH 프로그래밍](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)을 참조 바랍니다.

<span id="Base64Script"></span>
### Base64로 스크립트 파일 인코딩

1. 다음 명령어를 실행하여 "script_text.sh" 스크립트 파일에 대한 Base64 인코딩 작업을 진행합니다.
```
# 스크립트에 대한 Base64 인코딩 작업
base64 script_text.sh
```
다음의 정보를 출력합니다.
```
# 인코딩 후의 결과
IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
```
2. 다음 명령어를 실행하여 Base64 인코딩을 진행한 스크립트의 출력 결과를 확인합니다.
```
# 출력된 결과에 대해 Base64 인코딩을 진행하여 실행할 명령어가 맞는지 확인합니다.
echo "IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==" | base64 -d
```

### 텍스트 전달

Tencent Cloud는 인스턴스를 시작하는 다양한 방법을 제공하며, 그중 주요 방법은 다음 두 가지가 있습니다. 실제 필요에 따라 적합한 방법을 선택하시기 바랍니다.
- [공식 웹 사이트나 콘솔을 통해 전달](#Consoletrans)
- [API를 통해 전달](#APItrans)

<span id="Consoletrans"></span>
#### 공식 웹 사이트나 콘솔을 통해 전달

1. 다음 이미지와 같이, [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참조하여 인스턴스를 구매한 뒤, "4. 보안 그룹 및 호스트 설정"에서 [고급 설정]을 클릭합니다.
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. 다음 이미지와 같이, "고급 설정"의 "사용자 정의 데이터" 텍스트 상자에 [Base64로 스크립트 파일 인코딩](#Base64Script)해 출력된 인코딩 결과를 입력합니다.
예시, script_text 스크립트 파일을 Base64로 인코딩해 출력된 결과는'IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg=='입니다.
![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3. 인터페이스의 작업 절차에 따라 CVM 생성을 완료합니다.
> Tencent CVM은 오픈 소스 소프트웨어인 cloud-init을 통해 스크립트를 실행합니다. cloud-init에 대한 자세한 내용은 [cloud-init 공식 홈페이지](https://cloud-init.io/)를 참조 바랍니다.

<span id="APItrans"></span>
#### API를 통해 전달

API를 통해 CVM을 생성할 경우 [Base64로 스크립트 파일을 인코딩](#Base64Script)해 출력된 인코딩 결과를 RunInstances 인터페이스의 UserData 매개변수에 대입하여 텍스트를 전달할 수 있습니다.
예시, UserData 매개변수를 포함한 CVM의 요청 매개변수를 다음과 같이 생성합니다.
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
  &<공통 요청 매개변수>
```
