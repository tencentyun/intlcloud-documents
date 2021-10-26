## 작업 시나리오
Cloud Block Storage(CBS)는 클라우드에서 확장 가능한 스토리지 디바이스이며 사용자는 CBS를 생성한 후 수시로 그 크기를 확장하여 스토리지 용량을 증가할 수 있습니다. 또한 CBS의 기존 데이터는 손실되지 않습니다.
CBS를 확장한 후에는 [파티션 및 파일 시스템(Windows) 확장](https://intl.cloud.tencent.com/document/product/362/31601) 또는 [파티션 및 파일 시스템(Linux) 확장](https://intl.cloud.tencent.com/document/product/362/31602)으로 확장된 부분의 용량을 기존 파티션 안으로 나누거나 확장된 부분의 용량을 독립된 새로운 파티션으로 포맷해야 합니다.
>! MBR 형식 파티션이 지원하는 디스크의 최대 용량은 2TB입니다. 사용자의 디스크 파티션이 MBR 형식이고 2TB 이상으로 확장해야 하는 경우, 데이터 디스크를 다시 생성해서 마운트 하고 GPT 파티션 방식을 사용하여 데이터를 새로운 디스크에 복사할 것을 권장합니다.

## 데이터 디스크 확장
데이터 디스크 유형의 CBS 확장 시, 다음과 같은 세 가지 방식으로 확장이 가능합니다.
>!CVM에 다수의 용량과 유형이 같은 CBS가 마운트되어 있는 경우에는 [데이터 디스크 구분](#distinguish) 작업을 참조하여 구분할 수 있습니다. 확장할 데이터 디스크를 선택한 뒤, 다음과 같은 방식으로 확장합니다.
>

<dx-tabs>
::: CVM 콘솔을 사용하여 확장. (권장함) [](id:useCVMConsole)
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 타깃 CVM이 있는 행에서 [더 보기]>[리소스 변경]>[CBS 확장]을 선택합니다.
3. ‘CBS 확장’ 팝업창에서 확장할 데이터 디스크를 선택하고 [다음 단계]를 클릭합니다.
4. ‘용량 변경’ 단계에서 타깃 용량(반드시 현재 용량 이상이어야 함)을 설정하고 [다음 단계]를 클릭합니다.
5. ‘파티션 및 파일 시스템 확장’ 단계에서 주의사항을 확인한 뒤 [변경 시작]을 클릭합니다. 다음 이미지를 참고하십시오. 
![](https://main.qcloudimg.com/raw/dad3bd1f80569718a74a70df1579c4de.png)
6. 타깃 클라우드 서비스의 운영 체제 유형에 따라 사용자는 [파티션 및 파일 시스템 (Windows) 확장](https://intl.cloud.tencent.com/document/product/362/31601) 또는 [파티션 및 파일 시스템 (Linux) 확장](https://intl.cloud.tencent.com/document/product/362/31602)으로 확장된 부분의 용량을 기존 파티션 안으로 나누거나 확장된 부분의 용량을 독립된 새로운 파티션으로 포맷해야 합니다.
:::
::: CBS 콘솔을 사용하여 확장[](id:useCBSConsole)
1. [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에 로그인합니다.
2. 타깃 CBS의 [더 보기]>[확장]을 선택합니다.
3. 필요한 새로운 용량 크기(반드시 현재 크기보다 크거나 같아야 함)를 선택합니다.
4. 결제를 완료합니다.
5. 타깃 클라우드 서비스의 운영 체제 유형에 따라 사용자는 [파티션 및 파일 시스템 (Windows) 확장](https://cloud.tencent.com/document/product/362/31601) 또는 [파티션 및 파일 시스템(Linux) 확장](https://cloud.tencent.com/document/product/362/31602)을 실행하여 확장된 부분의 용량을 기존 파티션 안으로 나누거나 확장된 부분의 용량을 독립된 새로운 파티션으로 포맷해야 합니다.
:::
::: \sAPI\s를 사용하여 확장[](id:useAPI)
ResizeDisk 인터페이스를 사용하여 지정된 엘라스틱 CBS의 용량을 확장할 수 있습니다. 자세한 작업 내용은 [CBS 용량 확장](https://intl.cloud.tencent.com/document/product/362/16310)을 참조하십시오.
:::
</dx-tabs>



## 시스템 디스크 확장[](id:useCVMconsole)
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 뒤 타깃 CVM이 있는 행에서 [더 보기]>[리소스 변경]>[CBS 확장]을 선택합니다.
2. ‘CBS 확장’ 팝업창에서 확장할 시스템 디스크를 선택하고 [다음 단계]를 클릭합니다.
3. ‘용량 변경’ 단계에서 타깃 용량(반드시 현재 용량 이상이어야 함)을 설정하고 [다음 단계]를 클릭합니다.
4. ‘파티션 및 파일 시스템 확장’ 단계에서 주의사항을 확인하고 ‘강제 종료 동의’를 선택한 뒤 [변경 시작]을 클릭합니다. 다음 이미지를 참고하십시오. 
![](https://main.qcloudimg.com/raw/b3702c6323dfd650665a1293db56b295.png)
5. 콘솔의 확장 작업을 완료한 뒤, 해당 CVM 실제 운영 체제의 [Linux 인스턴스 cloudinit 설정 조회](#confirmLinuxConfig) 또는 [Windows 인스턴스 cloudinit 설정 조회](#confirmwindowsConfig) 결과에 따라 필요한 경우, 파티션 및 파일 시스템 확장 작업을 진행해 주십시오.



## 관련 작업
### 데이터 디스크 구분[](id:distinguish)
실제 사용하는 CVM 운영 체제에 따라 조회 방식을 선택할 수 있습니다.
<dx-tabs>
::: Linux
1. [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)합니다.
2. 다음 명령어를 실행하여 CBS와 디바이스 이름 간의 대응 관계를 확인합니다.
```
ls -l /dev/disk/by-id
```
반환 결과는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
이미지에서 `disk-xxxx`는 CBS ID로, [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에서 조회할 수 있습니다.
:::
::: Windows

1. [Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5435)합니다.
2. 마우스 오른쪽 버튼으로 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-6px 0px">를 클릭하고 [실행]을 선택합니다.
3. ‘실행’ 창에 `cmd`를 입력하고 **Enter**를 누릅니다.
4. 다음 명령어를 실행하여 CBS와 디바이스 이름 간의 대응 관계를 확인합니다.
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
::: 조회\sLinux\s인스턴스\scloudinit\s설정[](id:confirmLinuxConfig)
확장 완료 후 [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)하여 `/etc/cloud/cloud.cfg`에 growpart와 resizefs 설정 항목이 포함되어 있는지 확인하십시오.
 - 포함되어 있는 경우, 추가 작업을 진행하지 않아도 됩니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
    - **growpart**: 파티션 크기를 디스크 크기와 동일하게 확장합니다.
    - **resizefs**: `/`파티션 조정 파일 시스템을 파티션 크기와 동일하게 확장합니다.
 - 포함되어 있지 않은 경우, 타깃 클라우드 서비스의 운영 체제 유형에 따라 수동으로 파일 시스템과 파티션을 확장해야 합니다. [파티션 및 파일 시스템(Linux) 확장](https://intl.cloud.tencent.com/document/product/362/31602)을 실행하여 확장된 부분의 용량을 기존 파티션 안으로 나누거나 독립된 새 파티션으로 포맷합니다.
:::
::: 조회\sWindows\s인스턴스\scloudinit\s설정[](id:confirmwindowsConfig)
확장 완료 후 [Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5435)하여 `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\cloudbase-init.conf`의 plugin에 ExtendVolumesPlugin 설정 항목이 포함되어 있는지 확인하십시오.
 - 포함되어 있는 경우, 추가 작업을 진행하지 않아도 됩니다.
 - 포함되어 있지 않은 경우, 타깃 클라우드 서비스의 운영 체제 유형에 따라 수동으로 파일 시스템과 파티션을 확장해야 합니다. [파티션 및 파일 시스템(Windows) 확장](https://intl.cloud.tencent.com/document/product/362/31601)을 실행하여 확장된 부분의 용량을 기존 파티션 안으로 나누거나 독립된 새 파티션으로 포맷합니다.
:::
</dx-tabs>
