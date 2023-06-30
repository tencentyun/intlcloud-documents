## 현상 설명
VNC로 CVM에 로그인할 때 시스템에 정상적으로 액세스되지 않고, 다음과 같이 'Cannot allocate memory' 오류 보고 정보가 나타납니다.
![](https://main.qcloudimg.com/raw/0a31fdd909701c27c9923b2fff24668a.png)

## 예상 원인[](id:PossibleCauses)
시스템 내 다수의 Hugepage 메모리가 원인인 것으로 보입니다. 하나의 Hugepage 메모리는 기본적으로 2048KB를 차지합니다. `/etc/sysctl.conf`의 Hugepage 개수 계산에 따르면, 아래 예시처럼 1,280개의 Hugepage 메모리는 2.5G에 해당합니다. 인스턴스 설정은 낮은데 Huge pages pool에 2.5G을 할당하게 되면 시스템에 사용 가능한 메모리가 없어 재시작 후 시스템에 액세스할 수 없습니다.
![](https://main.qcloudimg.com/raw/1978a0b2a85fc828674f720c108c48a3.png)


## 해결 방법
1. [처리 순서](#ProcessingSteps)를 참고하여 총 프로세스 처리 수 제한 여부를 확인합니다. 
2. Hugepage의 메모리 설정을 확인하고 적절하게 수정합니다.


## 처리 순서[](id:ProcessingSteps)
1. [로그 오류 보고 fork: Cannot allocate memory](https://intl.cloud.tencent.com/document/product/213/40502)를 참고하여 프로세스 수가 제한을 초과하는지 확인합니다. 초과하지 않는다면 다음 단계를 실행합니다.
2. 단일 사용자 모드로 CVM에 로그인합니다. 자세한 내용은 [Linux CVM 단일 사용자 모드 진입 설정](https://intl.cloud.tencent.com/document/product/213/34819)을 참고하십시오.
3. 다음 명령어를 실행합니다. [예상 원인](#PossibleCauses)을 참고하여 Hugepage 메모리 설정을 확인합니다.
```
cat /etc/sysctl.conf | grep hugepages
```
Hugepage 메모리가 여러 개인 경우 아래 순서에 따라 설정을 수정하십시오.
4. 다음 명령어를 실행하여 VIM 편집기로 `/etc/sysctl.conf` 구성 파일을 엽니다.
```
vim /etc/sysctl.conf
```
5. **i**를 눌러 편집 모드로 전환하고, 인스턴스의 실제 설정에 맞춰 `vm.nr_hugepages` 설정 항목을 적정값으로 낮춥니다.
6. **Esc**를 누르고 **:wq**를 입력한 다음, **Enter**를 눌러 저장하고 VIM 편집기를 종료합니다.
7. 아래의 명령어를 실행하여 설정을 즉시 적용합니다.
```
sysctl -p
```
8. 설정 완료 후 CVM을 재시작하면 정상적으로 로그인이 가능합니다.
