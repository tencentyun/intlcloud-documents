## 작업 시나리오
Cloud Block Storage（CBS）는 클라우드에서 스토리지 장치 확장이 가능하고 사용자가 CBS를 생성한 후 수시로 용량을 확장할 수 있습니다. 또, 스토리지 용량을 확장할 때 CBS의 원본 데이터가 손실되지 않습니다.
[CBS 확장](https://intl.cloud.tencent.com/document/product/362/5747)완료 후, 확장된 부분의 용량을 기존 파티션 안으로 나누거나 확장된 부분의 용량을 독립된 새로운 파티션으로 포맷합니다.



## 전제 조건
>확장 파일 시스템 조작이 부적절한 경우 기존 데이터에 영향을 줄 수 있으므로 작업 전에 반드시 수동으로 [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755)에서 데이터 백업을 진행하기 권장합니다.
>
- 이미 [CBS 확장](https://intl.cloud.tencent.com/document/product/362/5747) 용량이 있습니다.
- 해당 CBS가 이미 Linux 클라우드 서버에 [마운트](https://cloud.tencent.com/document/product/362/32401)되었고 파일 시스템이 생성되었습니다.
- 확장 예정인 파티션 및 파일 시스템의 Linux 클라우드 서버에 [로그인](https://intl.cloud.tencent.com/document/product/213/5436)했습니다.

## 작업 순서
### 확장 방법 확인
<span id="fdisk"></span>
1. root 사용자는 다음 커맨드를 실행하여 CBS의 파티션 형식을 확인하십시오.
```
fdisk -l
```
 - 만약 결과 표시된 장치가 파티션으로 나누어 지지 않은 경우(예: /dev/vdb만 표시) [파일 시스템 확장](# ExpandTheFileSystem)을 참조하십시오.
 - 만약 결과가 다음 이미지처럼 (운영 체제에 따라 소폭 차이가 있음)표시된 경우 GPT 파티션 형식을 사용하고 있습니다.
![](https://main.qcloudimg.com/raw/5ff70adb58a223d32d334470c5b29e0e.png)
![](https://main.qcloudimg.com/raw/ce19715fc8494a9735b714d86f0cccfa.png)
 - 만약 결과가 다음 이미지처럼(운영 체제에 따라 소폭 차이가 있음) 표시된 경우 경MBR 파티션 형식을 사용하고 있습니다.
 > MBR 파티션 형식이 지원하는 디스크 최대 용량은 2TB입니다. 만약 사용자의 디스크 파티션이 MBR 형식이고 2TB 이상으로 확장해야 하는 경우, 데이터 디스크를 다시 작성하고 마운트합니다. 또, GPT 파티션 방식을 사용하여 데이터를 새로운 디스크에 복사합니다. Linux 운영 체제에 있어서 디스크 파티션 형식을 GPT를 사용하는 경우 fdisk 파티션 도구를 사용할 수 없으며 parted 도구를 사용해야 합니다.
 >
![](https://main.qcloudimg.com/raw/0e336cd3354c098cf5e70d0672e6f625.png)
2. [1단계] (#fdisk)에서 CBS 파티션 유형을 확인합니다. 해당하는 조작 안내를 선택하십시오.
<table>
     <tr>
         <th nowrap="nowrap">파티션 형식</th>  
         <th>조작 안내</th>  
         <th>설명</th>  
     </tr>
		 	 <tr>      
         <td>-</td>   
	     <td nowrap="nowrap"><a href="#ExpandTheFileSystem">파일 시스템 확장</a></td>
	     <td>파티션 생성이 되지 않았고 로우 디바이스에 직접 파일 시스템을 생성한 시나리오에 사용됩니다.</td>
     </tr>
	 <tr>      
         <td rowspan="2">GPT</td>   
	     <td nowrap="nowrap"><a href="#AddToTheExistingGPTPart">확장 부분의 용량을 기존 파티션(GPT)으로 나눕니다.</a></td>
	     <td>파티션되지 않은 직접 포맷된 시나리오에 동일하게 적용합니다.</td>
     </tr> 
	 <tr>
         <td><a href="#CreateANewGPTPart">확장 부분의 용량을 독립된 새로운 파티션(GPT)으로 포맷합니다.</a></td> 
	     <td>기존의 파티션이 변동하지 않고 유지할 수 있습니다.</td>
     </tr> 
	 <tr>
         <td rowspan="2">MBR</td>   
	     <td><a href="#AddToTheExistingMBRPart">확장 부분의 용량을 기존 파티션(MBR)으로 나눕니다.</a></td> 
	     <td>파티션되지 않은 직접 포맷된 시나리오에 동일하게 적용합니다.</td>
     </tr> 
	 <tr>
         <td><a href="#CreateANewMBRPart">확장 부분의 용량을 독립된 새로운 파티션(MBR)로 포맷합니다.</a></td> 
	     <td>기존의 파티션이 변동하지 않고 유지할 수 있습니다.</td>
     </tr> 
</table>

<span id="ExpandTheFileSystem"></span>
### 파일 시스템 확장

1. 파일 시스템의 유형에 따라 다른 커맨드를 실행하여 확장을 진행하십시오.
 - EXT 파일 시스템의 경우, `resize2fs` 커맨드를 실행하여 파일 시스템을 확장하십시오.
 - XFS 파일 시스템의 경우, `xfs_growfs` 커맨드를 실행하여 파일 시스템을 확장하십시오.

 예로 들면 `/dev/vdb`로 EXT 파일 시스템은 다음 커맨드를 실행합니다.
```
resize2fs /dev/vdb
```
예로 들면 `/dev/vdb`로 XFS 파일 시스템은 다음 커맨드를 실행합니다.
```
xfs_growfs /dev/vdb
```
2. 다음 커맨드를 실행하여 새로운 파티션을 확인하십시오.
```
df -h
```

<span id="AddToTheExistingGPTPart"></span>
### 확장 부분의 용량을 기존 파티션(GPT)으로 나누기
1. root 사용자는 다음 커맨드를 실행하여 CBS의 용량 변화를 확인하십시오.
 ```
parted <디스크 경로> print
```
이 문서의 디스크 경로는 예로 들면 `/dev/vdb`입니다. 다음을 참조하여 실행하십시오.
```
parted /dev/vdb print
```
만약 과정 중 아래와 같은 정보가 나타나면`Fix`를 입력하십시오.
![](//mccdn.qcloud.com/static/img/cf51cda9a12085f76949ab0d5dd0fbfc/image.png)
아래 이미지와 같이 확장 후의 CBS의 크기는 107GB이고 기존 파티션의 크기는 10.7GB가 됩니다.
![](//mccdn.qcloud.com/static/img/01a0a7a8fdfe6f05f2739f0326a74ef9/image.png)

2. 다음 커맨드를 실행하여 해당 CBS에 이미 마운트된 파티션이 있는지 여부를 확인하십시오.
```
mount | grep '<디스크 경로>' 
```
이 문서의 디스크 경로는 예로 들면 `/dev/vdb`입니다. 다음을 참조하여 실행하십시오.
```
mount | grep '/dev/vdb'
```
아래 이미지와 같이 CBS의 1개 파티션(vdb1)이 `/data`에 마운트됩니다.
![](//mccdn.qcloud.com/static/img/edc5bbd6834e1dd929ce0eb00acd53ca/image.png)
3. 다음 커맨드를 실행하여 데이터 디스크를 언마운트하십시오.
```
umount <마운트 포인트>
```
이 문서의 마운트 포인트는 예로 들면 `/data`입니다. 다음을 참조하여 실행하십시오.
```
umount /data
```
> CBS에서 모든 파티션의 파일 시스템을 언마운트하고 [4단계](#step4)작동을 실행하십시오. 다음 커맨드를 실행하여 해당 디스크의 모든 파티션 파일 시스템이 모두 언마운트 되었는지 확인하십시오.
```
mount | grep '/dev/vdb'
```
CBS의 모든 파티션 파일 시스템이 이미 언마운트되었습니다. 아래 이미지와 같이 나타납니다.
![](https://main.qcloudimg.com/raw/9242efdec1aab382ae74f975ca68d68a.png)

<span id="step4"></span>
4. 다음 커맨드를 실행하여 parted 파티션 도구로 진입합니다.
```
parted '<디스크 경로>'
```
이 문서의 디스크 경로는 예로 들면 `/dev/vdb`입니다. 다음을 참조하여 실행하십시오.
```
parted '/dev/vdb'
```
5. 다음 커맨드를 실행하여, 디스플레이와 조작 단위를 sector(기본 GB)로 변경하십시오.
```
unit s
```
6. `print`를 입력하여 파티션 정보를 조회하고 파티션이 있는 Start 값을 기록하십시오.
>파티션을 삭제하고 새로운 파티션을 생성한 후, Start 값을 반드시 그대로 유지해야 합니다. 그렇지 않으면 데이터가 손실됩니다.

 ![](//mccdn.qcloud.com/static/img/67ba54c1d9d63c307d4b8a157b70c722/image.png)
7. 다음 커맨드를 실행하여 기존 파티션을 삭제하십시오.
```
rm <파티션 Number>
```
예를 들어, 위의 이미지와으로부터 CBS에 1개의 파티션이 있는 것을 알 수 있으며 그 Number는 "1"입니다. 다음을 참조하여 실행하십시오.
```
 rm 1
```
에코 정보는 아래와 같습니다.
![](//mccdn.qcloud.com/static/img/3384eeada87ce75695e0e55125109eff/image.png)
5. 다음 커맨드를 실행하여 새로운 주요 파티션을 생성하십시오.
```
mkpart primary <기존 파티션 시작 섹터> 100%
```
그 중, 100%는 이 파티션이 디스크 맨 끝에 있음을 의미합니다.
예를 들어, 주요 파티션이 2048번째 섹터부터 시작되면 (반드시 삭제 전의 파티션과 일치해야 합니다. Start 값은 2048s) 실행하십시오.
```
mkpart primary 2048s 100%
```
만약 다음과 같은 상태가 나타나면, 'Ignore'를 입력하십시오.
![](//mccdn.qcloud.com/static/img/c45966e20dc856817c65fd6b81155e4a/image.png)
6. 다음 커맨드를 실행하여 새로운 파티션 작성이 성공했는지 확인하십시오.
```
print
```
반환된 결과는 아래 이미지와 같이 표시됩니다. 새로운 파티션 작성이 완료되었음을 나타냅니다.
![](//mccdn.qcloud.com/static/img/cb1af5adaf6c89d066077c43fd428a38/image.png)
7. 다음 커맨드를 실행하여 parted 도구를 종료하십시오.
```
quit
```
11. 다음 커맨드를 실행하여 확장 후의 파티션을 확인하십시오.
```
e2fsck -f <파티션 경로>
```
이 문서의 파티션 작성은 예로 들면 1(파티션 경로는`/dev/vdb1)입니다. 다음을 참조하여 실행하십시오.
```
e2fsck -f /dev/vdb1
```
아래 이미지와의 결과와 같이 반환됩니다.
![](//mccdn.qcloud.com/static/img/307f7a0c98eea05ca1d4560fe4e96f57/image.png)
12. 다음 커맨드를 실행하여 새로운 파티션의 EXT 파일 시스템에 확장을 진행하십시오.
```
resize2fs <파티션 경로>
```
이 문서의 파티션 경로는 예로 들면 `/dev/vdb1`입니다. 다음을 참조하여 실행하십시오.
```
resize2fs /dev/vdb1
```
확장이 완료되면 아래 이미지와 같이 나타납니다.
![](//mccdn.qcloud.com/static/img/57d66da9b5020324703498dbef0b12f9/image.png)
13. 다음 커맨드를 실행하여 새로운 파티션의 XFS 파일 시스템에 확장을 진행하십시오.
```
xfs_growfs <파티션 경로>
```
이 문서의 파티션 경로는 예로 들면 `/dev/vdb1`입니다. 다음을 참조하여 실행하십시오.
```
xfs_growfs /dev/vdb1
```
14. 다음 커맨드를 실행하여 새로운 파티션을 수동으로 마운트하십시오.
```
mount <파티션 경로> <마운트 포인트>
```
이 문서의 파티션 경로는`/dev/vdb1`이고 마운트 포인트는 예로 들면`/data`입니다 다음을 참조하여 실행하십시오.
```
mount /dev/vdb1 /data
```
15. 다음 커맨드를 실행하여 새로운 파티션을 확인하십시오.
```
df -h
```
아래 이미지와 정보와 같이 반환되면 마운트가 완료된 것입니다. 데이터 디스크를 확인할 수 있습니다.
![](//mccdn.qcloud.com/static/img/a2bd04c79e8383745689e19033a0daaa/image.png)

<span id="CreateANewGPTPart"></span>
### 확장 부분의 용량을 독립된 새로운 파티션(GPT)으로 포맷

1. 1. root 사용자는 다음 커맨드를 실행하여 CBS의 용량 변화를 확인하십시오.
 ```
parted <디스크 경로> print
```
이 문서의 디스크 경로는 예로 들면 `/dev/vdb`입니다. 다음을 참조하여 실행하십시오.
```
parted /dev/vdb print
```
만약 과정 중 아래와 같은 정보가 나타나면`Fix`를 입력하십시오.
![](//mccdn.qcloud.com/static/img/cf51cda9a12085f76949ab0d5dd0fbfc/image.png)
아래 이미지와 같이 확장 후의 CBS의 크기는 107GB이고 기존 파티션의 크기는 10.7GB가 됩니다.
![](//mccdn.qcloud.com/static/img/01a0a7a8fdfe6f05f2739f0326a74ef9/image.png)
2. 다음 커맨드를 실행하여 해당 CBS에 이미 마운트된 파티션이 있는지 여부를 확인하십시오.
```
mount | grep '<디스크 경로>' 
```
이 문서의 디스크 경로는 예로 들면 `/dev/vdb`입니다. 다음을 참조하여 실행하십시오.
```
mount | grep '/dev/vdb'
```
아래 이미지와 같이 CBS의 1개 파티션(vdb1)이 `/data`에 마운트됩니다.
![](//mccdn.qcloud.com/static/img/edc5bbd6834e1dd929ce0eb00acd53ca/image.png)
3. 다음 커맨드를 실행하여 데이터 디스크를 언마운트하십시오.
```
umount <마운트 포인트>
```
이 문서의 마운트 포인트는 예로 들면 `/data`입니다. 다음을 참조하여 실행하십시오.
```
umount /data
```
> CBS에서 모든 파티션의 파일 시스템을 언마운트하고 [4단계](#step4)작동을 실행하십시오. 다음 커맨드를 실행하여 해당 디스크의 모든 파티션 파일 시스템이 모두 언마운트 되었는지 확인하십시오.
```
mount | grep '/dev/vdb'
```
CBS의 모든 파티션 파일 시스템이 이미 언마운트되었습니다. 아래 이미지와 같이 나타납니다.
![](https://main.qcloudimg.com/raw/d1a9a33f0d4e3725aed677f2403c91ae.png)
<span id="Step4"></span>
4. 다음 커맨드를 실행하여 parted 파티션 도구로 진입합니다.
```
parted '<디스크 경로>'
```
이 문서의 디스크 경로는 예로 들면 `/dev/vdb`입니다. 다음을 참조하여 실행하십시오.
```
parted '/dev/vdb'
```
5. 다음 커맨드를 실행하여 파티션 정보를 확인하고 기존 파티션의 End 값을 기록하십시오.이 값은 다음 파티션의 시작 오프셋이 됩니다.
```
print
```
![](//mccdn.qcloud.com/static/img/788ce125bba952f204ed6ee36dfb644d/image.png)
6. 다음 커맨드를 실행하여 새로운 주요 파티션을 생성하십시오. 이 파티션은 기존 파티션의 끝부터 시작하여 디스크의 모든 새로운 공간을 덮어 씁니다.
```
mkpart primary start end
```
이 문서는 End 값을 10.7GB 예로 합니다. 다음 커맨드를 실행하십시오.
```
mkpart primary 10.7GB 100%
```
7. 다음 커맨드를 실행하여 새로운 파티션 생성에 성공했는지 확인하십시오.
```
print
```
![](//mccdn.qcloud.com/static/img/fc54fd4c05102ee91c648526d77d1b42/image.png)
8. 다음 커맨드를 실행하여 parted 도구를 종료합시오.
```
quit
```
9. 다음 커맨드를 실행하여 새로운 파티션을 포맷하십시오.
```
mkfs.<fstype> <파티션 경로> 
```
사용자는 파일 시스템의 형식(예: EXT2, EXT3 등)을 선택할 수 있습니다.
이 문서의 파일 시스템은 EXT3을 예로 합니다. 다음을 참조하여 실행하십시오. 
```
mkfs.ext3 /dev/vdb2
```

<span id="AddToTheExistingMBRPart"></span>
###확장 부분의 용량을 기존 파티션(MBR)으로  나누기
fdisk / e2fsck / resize2fs 자동 확장 도구는 Linux 운영 체제에서 사용하며, 새로 확장 된 CBS 공간을 기존 파일 시스템에 추가하는데 사용됩니다. 확장을 완료하려면 다음 4가지 조건을 반드시 충족해야 합니다.
- 파일 시스템이 EXT2/EXT3/EXT4/XFS이어야 합니다.
- 현재 파일 시스템에 오류가 없어야 합니다.
- 확장 후 디스크 크기가 2TB를 미만이어야 합니다.
- 현재 도구는 Python2 버전만 지원하며 Python3 버전은 지원되지 않습니다.


1. root 사용자는 다음 커맨드를 실행하여 파티션을 언마운트 하십시오.
```
umount <마운트 포인트>
```
이 문서의 마운트 포인트는 예로 들면 `/data`입니다. 다음을 참조하여 실행하십시오.
```
umount /data
```
![](//mccdn.qcloud.com/static/img/c0acc05057941681627a5fd34979d194/image.jpg)
2. 다음 커맨드를 실행하여 도구를 다운로드하십시오.
```
wget -O /tmp/devresize.py https://raw.githubusercontent.com/tencentyun/tencentcloud-cbs-tools/master/devresize/devresize.py
```
3. 다음 커맨드를 실행하여 확장 도구를 사용해 확장을 진행하십시오.
```
python /tmp/devresize.py <디스크 경로>
```
이 문서의 디스크 경로는`/dev/vdb`이며 파일 시스템은 vdb1를 예로 합니다. 다음을 참조하여 실행하십시오.
```
python /tmp/devresize.py /dev/vdb
```
![](//mccdn.qcloud.com/static/img/c7617b90578192d64d19f02325f00ffb/image.jpg)
 - 만약 “The filesystem on /dev/vdb1 is now XXXXX blocks long.” 메세지가 나타나면 확장이 완료된 것을 나타내며 [4단계](#step4MBR)을 실행하십시오.
 - 만약 "[ERROR]-e2fsck failed !!" 메세지가 나타나면 다음 단계를 수행하십시오.
   a. 다음 커맨드를 실행하여 파일 시스템이 위치한 파티션을 복구하십시오.
```
fsck -a <파티션 경로>
```
이 문서의 디스크 경로는`/dev/vdb`이며 파일 시스템은 vdb1를 예로 합니다. 다음을 참조하여 실행하십시오.
```
fsck -a /dev/vdb1
```
    b. 복구가 완료된 후, 다음 커맨드를 다시 실행하여 확장 도구를 사용해 확장을 진행하십시오.
```
python /tmp/devresize.py /dev/vdb
```
<span id="step4MBR"></span>
4. 다음 커맨드를 실행하여 확장 후의 파티션을 수동 마운트하십시오.
```
mount <파티션 경로> <마운트 포인트>
```
이 문서의 마운트 포인트는 예로 들면 `/data`입니다.
 - 만약 확장 전에 파티션이 이미 있고 파티션 경로를 예로 들면 `/dev/vdb1`입니다. 다음을 참조하여 실행하십시오.
```
mount /dev/vdb1 /data
```
 - 만약 확장 전에 파티션이 없었다면 다음을 참조하여 실행하십시오.
```
mount /dev/vdb /data
```
5. 다음 커맨드를 실행하여 확장 후의 파티션 용량을 확인하십시오.
```
df -h
```
만약 아래 이미지와 비슷한 유형의 정보가 반환되면 마운트가 완료된 것입니다. 데이터 디스크를 확인할 수 있습니다.
![](//mccdn.qcloud.com/static/img/2367f3e70cd0c3c1bef665cc47c1c3bc/image.jpg)
6. 다음 커맨드를 실행하여 확장 후 기존 파티션의 데이터 정보를 확인하고, 새로 추가된 저장 공간이 파일 시스템으로 확장되었는지를 확인하십시오.
```
ll /data
```

<span id="CreateANewMBRPart"></span>
### 확장 부분의 용량을 독립된 새로운 파티션(MBR)으로 포맷
1. root 사용자는 다음 커맨드를 실행하여 이미 마운트된 데이터 디스크 파티션 정보를 확인하십시오.
```
df -h
```
![](//mccdn.qcloud.com/static/img/0a450dfaa9cfc7b2c7fdc04861f0e754/image.png)
2. 다음 커맨드를 실행하여 데이터 디스크 확장 후 파티션 되지 않은 정보를 확인하십시오.
```
fdisk -l
```
![](//mccdn.qcloud.com/static/img/594671a1215dee3036b7940892438f62/image.png)
3. 다음 커맨드를 실행하여 모든 마운트된 파티션을 언마운트하십시오.
```
umount <마운트 포인트>
```
이 문서의 마운트 포인트는 예로 들면 `/data`입니다. 다음을 참조하여 실행하십시오.
```
umount /data
```
> CBS에서 모든 파티션을 언마운트하고 [4단계](#step4)를 실행하십시오.
<span id="Step4MBR"></span>
4. 다음 커맨드를 실행하여 새로운 파티션을 생성하십시오.
```
Fdisk <디스크 경로>
```
이 문서의 디스크 경로는 예로 들면`/dev/xvdc`입니다. 다음을 참조하여 실행하십시오.
```
fdisk /dev/xvdc
```
인터페이스의 표시에 따라 "p"(현재 파티션 정보 확인), "n"(파티션 생성), "p"(주요 파티션 생성), "2"(두 번째 주요 파티션 생성)을 입력하고, 엔터 2회를 누르고(기본 구성 사용), "w"(파티션 테이블 저장) 입력하여 파티션을 시작하십시오. 아래 이미지를 참고하십시오.
![](//mccdn.qcloud.com/static/img/8c35d6f4dfb367e74edc27ce6822c317/image.png)
>? 이 문서에서는 파티션 작성을 예로 합니다. 사용자의 실제 요구사항에 따라 여러 파티션을 작성할 수도 있습니다.
5. 다음 커맨드를 실행하여 새로운 파티션을 확인하십시오.
```
fdisk -l
```
아래 이미지는 새로운 파티션 xvdc2가 이미 생성되었음을 나타냅니다.
![](//mccdn.qcloud.com/static/img/e04e924d62317bc2c605c8abaac394f5/image.png)
6. 다음 커맨드를 실행하여, 새로운 파티션을 포맷하고 파일 시스템을 생성하십시오.
```
mkfs.<fstype> <파티션 경로> 
```
사용자는 파일 시스템의 형식(예: EXT2, EXT3 등)을 선택할 수 있습니다.
이 문서의 파일 시스템은 예로 들면 EXT3입니다. 다음을 참조하여 실행하십시오.
```
mkfs.ext3 /dev/xvdc2
```
![](//mccdn.qcloud.com/static/img/074e23eaa580495f96fb532b688d2d68/image.png)
7. 다음 커맨드를 실행하여 새로운 마운트 포인트를 생성하십시오.
```
mkdir <새로운 마운트 포인트>
```
이 문서의 마운트 포인트는`/data1`를 예로 합니다. 다음을 참조하여 실행하십시오.
```
mkdir /data1
```
8. 다음 커맨드를 실행하여 수동으로 새로운 파티션을 마운트하십시오.
```
mount <새로운 파티션 경로> <새로운 마운트 포인트>
```
이 문서의 새로운 파티션 경로는`/dev/xvdc2`이고 새로운 마운트 포인트는 예로 들면`/data1`입니다. 다음을 참조하여 실행하십시오.
```
mount /dev/xvdc2 /data1
```
9. 다음 커맨드를 실행하여 새로운 파티션 정보를 확인하십시오.
```
df -h
```
아래 이미지의 정보와 같이 반환되면 마운트가 완료된 것입니다. 즉, 데이터 디스크를 확인할 수 있습니다.
![](//mccdn.qcloud.com/static/img/7b749a4bb6e7c8267c9354e1590c35d4/image.png)

>만약 사용자가 클라우드 서버를 재시작하거나 시작할 때 자동으로 데이터 디스크에 마운트 되게하려면 [10단계](# AddNewPartINFOstep10) 와 [11단계](# AddNewPartINFOstep11)를 수행해야 합니다. 새로운 파티션 정보는 `/etc/fstab`에 추가하십시오.

<span id="AddNewPartINFOstep10"></span>
10. 다음 커맨드를 실행하여 정보를 추가하십시오.
```
echo '/dev/xvdc2 /data1 ext3 defaults 0 0' >> /etc/fstab
```
<span id="AddNewPartINFOstep11"></span>
11. 다음 커맨드를 실행하여 정보를 조회하십시오.
```
cat /etc/fstab
```
아래 이미지에 표시된 정보와 같이 반환되면 파티션 정보가 성공적으로 추가된 것입니다.
![](//mccdn.qcloud.com/static/img/f0b5c14bf08fd3629ddf6d9b1ae01ffc/image.png)

## 관련 작업
[파티션 및 파일 시스템(Windows) 확장](https://intl.cloud.tencent.com/document/product/362/6737)
