## 작업 시나리오
클라우드 디스크는 클라우드에서 확장 가능한 스토리지 장치입니다. 클라우드 디스크가 생성된 후에는 언제든지 용량을 확장하여 데이터 손실 없이 스토리지 용량을 늘릴 수 있습니다.
클라우드 디스크의 볼륨 확장이 완료되면 파티션과 파일 시스템을 확장해야 합니다. 확장된 용량을 기존 파티션에 할당하거나 독립된 새 파티션으로 포맷해야 합니다.


<dx-alert infotype="notice" title="">
MBR 포맷 파티션이 지원하는 디스크의 최대 용량은 2TB입니다. MBR 파티션을 2TB 이상으로 확장하려면 새 데이터 디스크를 생성 및 탑재하고 GPT 파티션 형식을 사용하여 데이터를 복사하는 것이 좋습니다.
</dx-alert>


## 데이터 디스크 확장
클라우드 디스크가 데이터 디스크인 경우 다음 세 가지 방법으로 확장할 수 있습니다.


<dx-alert infotype="notice" title="">
CVM에 동일한 용량과 종류의 클라우드 디스크가 여러 개 탑재되어 있는 경우, [데이터 디스크 구분](#distinguish) 작업에 따라 구분할 수 있습니다. 확장할 데이터 디스크를 선택한 후 다음과 같은 방법으로 용량을 확장합니다.
</dx-alert>



<dx-tabs>
::: CVM 콘솔을 통한 데이터 디스크 확장(권장)[](id:useCVMConsole)
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 데이터 디스크를 확장할 CVM을 찾고 작업 열에서 **더보기** > **리소스 변경** > **클라우드 디스크 확장**을 선택합니다.
3. 팝업 창에서 확장할 데이터 디스크를 선택하고 **다음 단계**를 클릭합니다.
4. 새 용량을 선택하고(현재 용량보다 크거나 같아야 함) **다음 단계**를 클릭합니다.
5. ‘파티션 및 파일 시스템 확장’ 단계에서 주의사항을 확인한 뒤 **변경 시작**을 클릭합니다. 다음 이미지 참고:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rcu7553_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421164941.png)
6. 타깃 클라우드 서비스의 운영 체제 유형에 따라 사용자는 [파티션 및 파일 시스템(Windows) 확장](https://intl.cloud.tencent.com/document/product/362/31601) 또는 [파티션 및 파일 시스템(Linux) 확장](https://intl.cloud.tencent.com/document/product/362/39995)으로 확장된 부분의 용량을 기존 파티션 안으로 나누거나 확장된 부분의 용량을 독립된 새로운 파티션으로 포맷해야 합니다.
:::
::: CBS 콘솔을 통한 데이터 디스크 확장[](id:useCBSConsole)
1. [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에 로그인합니다.
2. 확장할 클라우드 디스크를 찾고 작업 열에서 **더보기** > **확장**을 선택합니다.
3. 필요한 새로운 용량 크기(반드시 현재 크기보다 크거나 같아야 함)를 선택합니다.
4. 결제를 완료합니다.
5. 타깃 클라우드 서비스의 운영 체제 유형에 따라 사용자는 [파티션 및 파일 시스템(Windows) 확장](https://intl.cloud.tencent.com/document/product/362/31601) 또는 [파티션 및 파일 시스템(Linux) 확장](https://intl.cloud.tencent.com/document/product/362/39995)을 실행하여 확장된 부분의 용량을 기존 파티션 안으로 나누거나 확장된 부분의 용량을 독립된 새로운 파티션으로 포맷해야 합니다.
:::
::: API를 통한 데이터 디스크 확장[](id:useAPI)
ResizeDisk API를 사용하여 지정된 클라우드 디스크를 확장할 수 있습니다. 자세한 작업 내용은 [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310)를 참고하십시오.

:::
</dx-tabs>



## 시스템 디스크 확장[](id:useCVMconsole)
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 뒤 확장할 CVM이 있는 행에서 **더보기** > **리소스 변경** > **클라우드 디스크 확장**을 선택합니다.
2. **클라우드 디스크 확장** 팝업 창에서 확장할 시스템 디스크를 선택하고 **다음 단계**를 클릭합니다.
3. **용량 변경** 단계에서 새 용량을 선택하고(현재 용량보다 크거나 같아야 함) **다음 단계**를 클릭합니다.
4. 다음 확장 방법을 통해 확장 작업을 완료합니다.
<dx-tabs>
::: CVM 콘솔을 통한 데이터 디스크 확장
<dx-alert infotype="explain" title="">
CVM은 클라우드 디스크를 시스템 디스크로 온라인 확장, 즉 무정지 확장을 지원합니다.
</dx-alert>
 1. **파티션 및 파일 시스템 확장** 단계에서 주의사항을 확인한 뒤 **변경 시작**을 클릭합니다. 다음 이미지 참고:
 <img style="width:600px; max-width: inherit;" src="https://staticintl.cloudcachetci.com/yehe/backend-news/rcu7553_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421164941.png" />
 2. 콘솔 확장 작업이 완료되면 인스턴스에 로그인하여 파일 시스템이 자동으로 확장되었는지 확인합니다. 확장하지 않은 경우 [Extending System Disk Partitions and File Systems Online](https://intl.cloud.tencent.com/document/product/362/50063)을 참고하여 파티션 및 파일 시스템을 확장하십시오.
:::
::: CBS 콘솔을 통한 데이터 디스크 확장[](id:useCBSConsole)
1. [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에 로그인합니다.
2. 확장할 클라우드 디스크를 찾고 작업 열에서 **더보기** > **확장**을 선택합니다.
3. 필요한 새로운 용량 크기(반드시 현재 크기보다 크거나 같아야 함)를 선택합니다.
4. 결제를 완료합니다.
5. 타깃 클라우드 서비스의 운영 체제 유형에 따라 사용자는 [파티션 및 파일 시스템(Windows) 확장](https://intl.cloud.tencent.com/document/product/362/31601) 또는 [파티션 및 파일 시스템(Linux) 확장](https://intl.cloud.tencent.com/document/product/362/39995)을 실행하여 확장된 부분의 용량을 기존 파티션 안으로 나누거나 확장된 부분의 용량을 독립된 새로운 파티션으로 포맷해야 합니다.
:::
::: API를 통한 데이터 디스크 확장[](id:useAPI)
ResizeInstanceDisks API를 사용하여 지정된 비탄성 클라우드 디스크를 확장할 수 있습니다. 자세한 작업은 [ResizeInstanceDisks](https://intl.cloud.tencent.com/document/product/213/33238)를 참고하십시오.

:::
</dx-tabs>


## 관련 작업
### 데이터 디스크 구분[](id:distinguish)
실제 사용하는 CVM 운영 체제에 따라 조회 방식을 선택할 수 있습니다.
<dx-tabs>
::: Linux
1. [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)합니다.
2. 다음 명령어를 실행하여 클라우드 디스크와 디바이스 이름 간의 대응 관계를 확인합니다.
```
ls -l /dev/disk/by-id
```
반환 결과는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
이미지에서 `disk-xxxx`는 CBS ID로, [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에서 조회할 수 있습니다.
:::
::: Windows
1. [Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5435)합니다.
2. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-6px 0px">을(를) 우클릭하고 **실행**을 선택합니다.
3. ‘실행’ 창에 `cmd`를 입력하고 **Enter**를 누릅니다.
4. 다음 명령어를 실행하여 클라우드 디스크와 디바이스 이름 간의 대응 관계를 확인합니다.
```
wmic diskdrive get caption,deviceid,serialnumber
```
또는 다음 명령어를 실행하십시오.

```
wmic path win32_physicalmedia get SerialNumber,Tag
```
반환 결과는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)
이미지에서 `disk-xxxx`는 CBS ID로, [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에서 조회할 수 있습니다.
:::
</dx-tabs>

### 인스턴스 cloudinit 설정 조회
실제 사용하는 CVM 운영 체제에 따라 조회 방식을 선택할 수 있습니다.
<dx-tabs>
::: Linux 인스턴스 cloudinit 구성 조회[](id:confirmLinuxConfig)
확장 완료 후 [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)하여 `/etc/cloud/cloud.cfg`에 growpart와 resizefs 설정 항목이 포함되어 있는지 확인하십시오.
 - 포함되어 있는 경우, 추가 작업을 진행하지 않아도 됩니다. 다음 이미지 참고:
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
    - **growpart**: 파티션 크기를 디스크 크기와 동일하게 확장합니다.
    - **resizefs**: `/` 파티션 파일 시스템을 파티션 크기와 동일하게 확장합니다.
 - 포함되어 있지 않은 경우, 대상 클라우드 서비스의 운영 체제 종류에 따라 파일 시스템 및 파티션을 수동으로 확장해야 합니다. [파티션 및 파일 시스템(Linux) 확장](https://intl.cloud.tencent.com/document/product/362/39995)을 실행하여 확장된 부분의 용량을 기존 파티션 안으로 나누거나 독립된 새 파티션으로 포맷합니다.
:::
::: Windows 인스턴스 cloudinit 구성 조회[](id:confirmwindowsConfig)
확장 완료 후 [Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5435)하여 `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\cloudbase-init.conf`의 plugin에 ExtendVolumesPlugin 구성 항목이 포함되어 있는지 확인하십시오.
 - 포함되어 있는 경우, `cloudbase-init` 구성 파일 `cloudbase-init.conf`에 ExtendVolumesPlugin 구성 항목이 포함된 경우 `cloudbase-init`를 다시 시작해야 자동으로 볼륨을 확장하고 C 파티션 뒤에 빈 공간을 C 파티션에 추가할 수 있습니다. 또한, C 파티션과 빈 공간 사이에 다른 파티션의 간섭이 없어야 합니다. C 파티션과 빈 공간 사이에 다른 파티션이 없고 재시작을 원하지 않거나, 타사 보안 소프트웨어가 `cloudbase-init`를 막아 extend volume을 완료할 수 없는 경우, 다음과 같이 수동으로 powershell을 실행해야 합니다.
 ```plantext
$DiskOps="@
select disk 0
select volume c
extend
exit
@"
$DiskOps | diskpart.exe | Out-Null
 ```
 - 포함되어 있지 않은 경우, 대상 클라우드 서비스의 운영 체제 종류에 따라 파일 시스템 및 파티션을 수동으로 확장해야 합니다. [파티션 및 파일 시스템(Windows) 확장](https://intl.cloud.tencent.com/document/product/362/31601)을 실행하여 확장된 부분의 용량을 기존 파티션 안으로 나누거나 독립된 새 파티션으로 포맷합니다.
:::
</dx-tabs>

