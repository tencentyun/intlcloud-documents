## 작업 시나리오
본 문서에서는 CentOS 8.2 OS를 적용한 Tencent Cloud Cloud Virtual Machine(CVM)을 예로 들어 SCP를 통해 Linux CVM으로 파일을 업로드 또는 다운로드 하는 방법에 대해 소개합니다.


## 전제 조건
구매한 Linux CVM이 있어야 합니다.

## 작업 순서
### 공용 IP 획득
[CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 후, 인스턴스 리스트 페이지에서 파일을 업로드할 CVM의 공용 IP를 다음 이미지와 같이 기록합니다.
![](https://main.qcloudimg.com/raw/4ffafbd2f6ab65d55e56fe59b669363a.png)


### 파일 업로드
1. 다음 명령어를 실행하여 Linux CVM에 파일을 업로드합니다.
```
scp 로컬 파일 주소 CVM 계정@CVM 공용 IP/도메인: CVM 파일 주소
```
예를 들어, 로컬 파일 `/home/lnmp0.4.tar.gz`를 IP 주소가 '129.20.0.2`인 CVM 디렉터리에 업로드해야 할 경우, 다음과 같은 명령어를 실행합니다.
```
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
<dx-alert infotype="explain" title="">
'-r' 매개변수를 추가하여 파일을 업로드할 수 있습니다. 더 많은 scp 명령 기능을 보려면 `man scp`를 실행하여 더 많은 정보를 확인하십시오.
</dx-alert>
2. **yes**를 입력한 뒤 **Enter**를 눌러 업로드 여부를 확인하고 로그인 비밀번호를 입력하면 업로드가 완료됩니다.
 - 시스템 기본 설정 비밀번호로 인스턴스에 로그인할 경우 [내부 메시지](https://console.cloud.tencent.com/message)에 접속하여 획득 바랍니다.
 - 비밀번호를 잊으신 경우, [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)하시기 바랍니다.

### 파일 다운로드
1. 다음 명령어를 실행하여 Linux CVM의 파일을 로컬에 다운로드합니다.
```
scp CVM 계정@CVM 인스턴스 공용 IP/도메인: CVM 파일 주소 로컬 파일 주소 
```
예를 들어, IP 주소가 `129.20.0.2`인 CVM 파일 `/home/lnmp0.4.tar.gz`을 해당 로컬 디렉터리로 다운로드하는 경우, 다음과 같은 명령어를 실행합니다.
```
scp root@129.20.0.2:/home/Inmp0.4.tar.gz /home/Inmp0.4.tar.gz
```

