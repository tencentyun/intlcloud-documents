## 현상 설명
Linux CVM 인스턴스에 메모리 문제로 장애가 발생했습니다(예시: 시스템 내부 서비스 응답 속도 감소, 서버 로그인 불가, 시스템 OOM 트리거 등).

## 예상 원인
지나치게 높은 인스턴스 메모리 사용률이 원인인 것으로 보입니다. 보통 인스턴스 메모리 사용률이 지속적으로 90%를 넘을 경우 사용률이 지나치게 높다고 판단합니다.


## 문제 진단
1. [처리 순서](#ProcessingSteps)를 참조하여 인스턴스 메모리 사용률이 지나치게 높아서 생긴 문제인지 판단합니다.
2. [기타 메모리 문제의 전형적인 사례 분석](#OtherProcessingSteps)을 참조하여 문제 원인을 파악합니다.

## 처리 순서[](id:ProcessingSteps)
1. [관련 작업](#RelatedOperations)을 참조하여 메모리 사용률이 지나치게 높지는 않은지 확인합니다.
 - 메모리 사용률이 지나치게 높다면 다음 단계를 실행합니다.
 - 메모리 사용률이 정상인 경우 [기타 메모리 문제의 전형적인 사례 분석](#OtherProcessingSteps)을 참조하여 자세한 문제 원인을 파악합니다.
2. 시스템 내부에서 `top` 명령어를 실행한 후 **M**을 눌러 'RES'나 'SHR' 열에 메모리 점유율이 지나치게 높은 프로세스가 있는지 확인합니다.
  - 없는 경우 다음 단계를 실행합니다.
  - 있는 경우 프로세스 유형에 맞춰 작업을 진행합니다. 자세한 내용은 [프로세스 분석](https://intl.cloud.tencent.com/document/product/213/32387)을 참조하십시오.
3. 다음 명령어를 실행하여 공유 메모리 점유율이 지나치게 높지는 않은지 확인합니다.
```
cat /proc/meminfo | grep -i shmem
```
반환 결과는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/269ca888f6f0232a63705b6f9fd578a8.png)
4. 다음 명령어를 실행하여 회수할 수 없는 slab 메모리의 점유율이 지나치게 높지는 않은지 확인합니다.
```
cat /proc/meminfo | grep -i SUnreclaim
```
반환 결과는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/9e6c84eb5bfb0be315fc39d1b768d168.png)
5. 다음 명령어를 실행하여 Hugepage 메모리가 있는지 확인합니다.
```
cat /proc/meminfo | grep -iE "HugePages_Total|Hugepagesize"
```
반환 결과는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/aae7ce06f7034c123c26ef92265b82ea.png)
 - `HugePages_Total`의 출력값이 0인 경우 [기타 메모리 문제의 전형적인 사례 분석](#OtherProcessingSteps)을 참조하여 자세한 문제 원인을 파악합니다.
 - `HugePages_Total`의 출력값이 0이 아닌 경우 Hugepage 메모리가 설정되어 있다는 의미입니다. Hugepage 메모리의 크기는 `HugePages_Total*Hugepagesize`이며, Hugepage가 다른 악성 프로그램을 위해 설정된 것은 아닌지 확인해야 합니다. Hugepage 메모리가 필요하지 않다면 `/etc/sysctl.conf` 파일의 `vm.nr_hugepage` 설정 항목에 주석을 달고 `sysctl -p` 명령어를 실행하여 Hugepage 메모리 설정을 해제합니다.

## 관련 작업[](id:RelatedOperations)
### 메모리 사용률 조회
Linux 릴리스 버전마다 `free` 명령어 출력의 의미가 다를 수 있기 때문에 `free` 명령어 출력 정보만으로 메모리 사용률을 계산할 수는 없습니다. 그러므로 다음 절차를 따라 Tencent Cloud 모니터링을 통해 메모리 사용률을 확인하시기 바랍니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하여 인스턴스 관리 페이지를 클릭합니다.
2. 인스턴스 ID를 선택하고 해당 인스턴스 상세 페이지로 이동하여 [모니터링] 탭을 선택합니다.
3. '메모리 모니터링'에서 다음과 같이 해당 인스턴스의 메모리 사용률을 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/4f9f423e6d9d460d1413ff0ead6c7e96.png)

### 컴퓨팅 메모리 사용률
메모리 모니터링에서 메모리 사용률은 총 메모리 중 사용한 메모리의 비율로 계산합니다. 버퍼와 시스템 캐시가 점유하는 콘텐츠는 포함되지 않습니다. 계산 프로세스는 다음과 같습니다.
= `(Total - available)100% / Total`
= `(Total - (Free + Buffers + Cached + SReclaimable - Shmem))100% /Total`
= `(Total - Free - Buffers - Cached - SReclaimable + Shmem）* 100% / Total`

계산 프로세스에서 사용하는 `Total`, `Free`, `Buffer`, `Cached`, `SReclaimable`, `Shmem` 매개변수는 `/proc/meminfo`에서 획득할 수 있습니다. 다음은 `/proc/meminfo` 예시입니다.
```plaintext
1. [root@VM_0_113_centos test]# cat /proc/meminfo 
2. MemTotal: 16265592 kB
3. MemFree: 1880084 kB
4. ......
5. Buffers: 194384 kB
6. Cached: 13647556 kB
7. ......
8. Shmem: 7727752 kB
9. Slab: 328864 kB
10. SReclaimable: 306500 kB
11. SUnreclaim: 22364 kB
12. ......
13. HugePages_Total: 0
14. Hugepagesize: 2048 kB
```
다음은 매개변수에 대한 설명입니다.
<table>
<tr>
<th>매개변수</th>
<th>설명</th>
</tr>
<tr>
<td><code>MemTotal</code></td>
<td>시스템 총 메모리입니다.</td>
</tr>
<tr>
<td><code>MemFree</code></td>
<td>시스템 잔여 메모리입니다.</td>
</tr>
<tr>
<td><code>Buffers</code></td>
<td> 블록 디바이스가 점유하는 캐시 페이지입니다. 직접 읽기/쓰기 블록 디바이스와 파일 시스템 메타데이터가 여기에 포함됩니다(예: SuperBlock이 사용하는 캐시 페이지).</td>
</tr>
<tr>
<td><code>Cached</code></td>
<td>page cache입니다. tmpfs의 파일 <code>POSIX/SysV shared memory</code> 및 <code>shared anonymous mmap</code>이 포함됩니다.
</td>
</tr>
<tr>
<td><code>Shmem</code></td>
<td>tmpfs 등 공유 메모리를 포함합니다.
</td>
</tr>
<tr>
<td><code>Slab</code></td>
<td>커널 slab 할당자가 할당한 메모리는 <code>slabtop</code>로 조회할 수 있습니다.
</td>
</tr>
<tr>
<td><code>SReclaimable</code></td>
<td>회수할 수 있는 slab입니다.</td>
</tr>
<tr>
<td><code>SUnreclaim</code></td>
<td>회수할 수 없는 slab입니다.</td>
</tr>
<tr>
<td><code>HugePages_Total</code></td>
<td>Hugepage 메모리의 총 수량입니다.</td>
</tr>
<tr>
<td><code>Hugepagesize</code></td>
<td>Hugepage 메모리 1페이지의 크기입니다.</td>
</tr>
</table>

### 기타 메모리 문제의 전형적인 사례 분석[](id:OtherProcessingSteps)
위 절차를 따랐음에도 문제가 처리되지 않거나, CVM 사용 시 아래 유형의 오류 정보가 나타난다면 다음 솔루션을 참조하십시오.
- [로그 오류 보고 fork: Cannot allocate memory](https://intl.cloud.tencent.com/document/product/213/40502)
- [VNC 로그인 오류 보고 Cannot allocate memory](https://intl.cloud.tencent.com/document/product/213/40503)
- [인스턴스 메모리 사용량이 남은 상황에서 Out Of Memory 트리거](https://intl.cloud.tencent.com/document/product/213/40504) 
