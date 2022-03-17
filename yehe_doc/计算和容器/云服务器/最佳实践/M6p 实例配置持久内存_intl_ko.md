## 작업 시나리오
본문은 M6p 인스턴스에서 영구 메모리를 설정하는 방법을 설명합니다.


## 인스턴스 설정
본문은 다음과 같이 설정된 CVM 인스턴스를 예시로 들고 있습니다. 적용 시 실제 조건을 기준으로 하십시오.
 - **인스턴스 사양**: 메모리형 M6p 인스턴스 M6p.LARGE16(4코어 16GB). 기타 사양 및 설정은 [메모리형 M6p](https://intl.cloud.tencent.com/document/product/213/11518)를 참고하십시오.
 - **운영 체제**: TencentOS Server 3.1(TK4).
<dx-alert infotype="explain" title="">
인스턴스에서 다음 운영 체제를 사용할 것을 권장합니다.
 - TencentOS Server 3.1
 - CentOS 7.6CentOS 7.6 이상 버전
 - Ubuntu 18.10 이상 버전
</dx-alert>

## 전제 조건
[M6p 인스턴스](https://intl.cloud.tencent.com/document/product/213/11518) 생성 및 로그인이 완료되어있어야 합니다.
- 인스턴스 생성 방법은 [구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오.
- 인스턴스 로그인 방법은 [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.


## Intel® Optane™ DC BPS 하드웨어(PMEM) 모드 소개

### Memory 모드
Memory 모드에서는 기존 DRAM이 가장 자주 액세스되는 데이터의 캐시 역할을 하는 반면, 영구 메모리는 백업 메모리로 사용되며, 캐시 관리 작업은 메모리 컨트롤러에서 자동으로 처리됩니다.

### AD 모드
M6p 모델은 이 모드를 채택하고 있습니다. M6p 모델에서 플랫폼 측은 BPS 하드웨어를 AD 모드로 설정하고, CVM에 전송하여 사용하도록 합니다. AD 모드에서 애플리케이션은 PMEM 장치를 메모리 또는 로컬 SSD 디스크로 사용할 수 있습니다.


## 작업 단계

### PMEM 초기화
인스턴스를 처음 사용하는 경우 다음 명령어를 순서대로 실행하여 PMEM 장치를 초기화합니다. 이미 PMEM 초기화한 경우 이 단계를 건너뛰십시오.
```
yum install -y ndctl
```
```
ndctl destroy-namespace all --force
```
<dx-alert infotype="explain" title="">
가장 큰 인스턴스에는 두 개의 region이 있습니다. 다음 명령어를 실행한 후 region0을 region1로 바꾸고 명령어를 다시 실행하십시오.
</dx-alert>
```
ndctl disable-region region0
```
```
ndctl init-labels all
```
```
ndctl enable-region region0
```

### AD 모드에서 PMEM 설정

실제 필요에 따라 영구 메모리를 메모리 또는 로컬 SSD 디스크로 사용할 수 있습니다.

<dx-tabs>
::: 메모리로 사용
PMEM은 문자 장치로서 상위 애플리케이션 레이어(예시 redis)에 제공되어 영구 메모리 할당을 진행할 수 있습니다. memkind와 같은 PMDK 프레임워크를 통해 사용할 수 있습니다. 설정 방법은 다음과 같습니다. 
1. 다음 명령어를 실행하여 문자 장치를 생성합니다.
```
ndctl create-namespace -r region0 -m devdax
```
반환 결과가 아래 이미지와 같으면 'dax0.0' 문자 장치가 생성된 것입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e25e7a26c05b4d09507f571105d5e7c2.png)
가장 큰 인스턴스에는 두 개의 region이 있으므로 가장 큰 인스턴스를 사용하는 경우 다음 명령어를 동시에 실행하십시오.
```
ndctl create-namespace -r region1 -m devdax -f
```
설정이 완료되면 `/dev` 디렉터리에 `dax0.0`의 문자 장치가 생성되며, 이는 영구 메모리에 매핑될 수 있습니다.
2. 다음 명령어를 실행하여 영구 메모리 크기를 확인합니다.
```
ndctl list -R
```
반환 결과는 다음 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b454a36bf3baf0361fe6154639b6c4da.png)


#### 확장 기능(옵션)
이 단계를 통해 기능을 확장할 수 있습니다. 다음 명령어를 순서대로 실행하고 PMEM을 사용하여 CVM의 메모리를 확장합니다.
1. 상위 버전의 커널(5.1 이상 및 TencentOS Server 3.1 커널과 같은 KMEM DAX 드라이버 사용) 지원을 통해 devdax 모드의 PMEM을 kmemdax로 추가 설정할 수 있으며 PMEM을 사용하여 CVM의 메모리를 확장할 수 있습니다.
```
yum install -y daxctl
```
```
daxctl migrate-device-model
```
```
reboot
```
```
daxctl reconfigure-device --mode=system-ram --no-online dax0.0
```
반환 결과는 다음 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6cc731b4e6e08be343c284683ac75721.png)
2. 다음 명령어를 실행하여 시스템 메모리 확장을 확인합니다.
```
numactl -H
```
반환 결과는 다음 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6cbeee0aeb1bf7d4527297d5eaa747bc.png)
:::
::: 로컬 SSD 디스크로 사용
AD 모드의 PMEM을 고속 블록 장치로 설정할 수도 있으며, 일반 블록 장치로 파일 시스템 생성, 베어 디스크 읽기/쓰기 등 작업을 할 수 있습니다. 설정 방법은 다음과 같습니다.
1. 다음 명령어를 실행하여 `/dev` 디렉터리에 pmem0 블록 장치를 생성합니다.
```
ndctl create-namespace -r region0 -m fsdax
```
반환 결과는 다음 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/010dbd1f35b3dfdff08d39546f0ce06e.png)
가장 큰 인스턴스에는 두 개의 region이 있으므로 가장 큰 인스턴스를 사용하는 경우 다음 명령어를 동시에 실행하십시오.
```
ndctl create-namespace -r region1 -m fsdax -f
```
2. 다음 명령어를 순서대로 실행하여 파일 시스템을 생성하거나 마운트하여 사용할 수 있습니다.
    1. 파일 시스템을 생성합니다.
```
mkfs.ext4 /dev/pmem0
```
반환 결과가 아래 이미지와 같으면 파일 시스템이 성공적으로 생성된 것입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e1c39d0122b4d6bff535d22dd9af0c18.png)
    2. `/mnt/`에 마운트합니다.
```
mount -o dax,noatime /dev/pmem0 /mnt/
```


:::
</dx-tabs>






## 참고 자료
- [Intel® Optane™ DC Persistent Memory](https://www.intel.com/content/dam/support/us/en/documents/memory-and-storage/data-center-persistent-mem/Intel-Optane-DC-Persistent-Memory-Quick-Start-Guide.pdf)
- [Linux Provisioning for Intel® Optane™ Persistent Memory](https://www.intel.com/content/www/us/en/developer/articles/technical/qsg-part2-linux-provisioning-with-optane-pmem.html)
