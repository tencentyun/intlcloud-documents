## RAID 소개
RAID는 여러 디스크를 조합하고 하나의 디스크 어레이 그룹을 구성하여 데이터 읽기 및 쓰기 성능과 신뢰성을 향상시킬 수 있습니다.운영 체제는 디스크 어레이 그룹을 하드 디스크로 사용합니다. 현재 RAID에는 다양한 레벨이 있으며 선택한 버전에 따라  다릅니다. 디스크 어레이 그룹은 대용량 디스크에 비해 데이터 통합 강화, 내고장성 기능 강화, 처리량 및 용량 강화 등 장점을 갖고 있습니다.
>
>- 엘라스틱 Cloud Block Storage（CBS） 만료로 인해 시스템이 강제로 격리되어 RAID에 영향을 주지 않도록 [연장](https://intl.cloud.tencent.com/document/product/362/6739) 작업을 수행하십시오.
>- RAID 1, RAID 01 및 RAID 10을 생성할 경우 동일한 크기의 파티션을 사용하여 디스크 용량 낭비를 줄일 것을 권장합니다.

 RAID 0, RAID 1, RAID 01 및 RAID 10 사이의 같은 점 및 다른 점은 다음 표에서 참조하십시오.
<table>
     <tr>
         <th nowrap="nowrap">RAID 레벨</th>  
         <th>소개</th>  
		 <th>장단점</th>
		 <th>사용 시나리오(권장)</th>
     </tr>
	 <tr>
         <td>RAID 0</td>
				 <td>스토리지 모드: 데이터 세그먼트를 다양한 디스크에 저장합니다.<br /></br>가상 디스크 크기: 어레이의 모든 디스크 용량의 합입니다.</td>
		 <td>
		 <ul><li><b>장점</b>: 읽기 및 쓰기를 병행할 수 있습니다.</br>이론적으로 읽기 및 쓰기 속도는 단일 디스크의 최대 N 배(N은 RAID 0을 구성하는 디스크 수) 에 달할 수 있지만 실제로 파일 크기 및 파일 시스템 크기 등 다양한 요소에 의해 제한됩니다.</li>
		 <li><b>단점</b>: 데이터 이중화가 없고 단일 디스크만 손상되어도 가장 심각한 경우 모든 데이터의 손실을 초래할 수 있습니다.</li></ul></td>
		 <td>I/O 성능에 대한 요구가 높고 이미 다른 방식을 통해 데이터를 백업하였거나 데이터 백업이 필요하지 않는 시나리오입니다.</td>
     </tr> 
	 <tr>
         <td>RAID 1</td>
         <td>스토리지 모드: 데이터가 미러 이미지에 의해 여러 디스크에 저장됩니다.<br /></br> 가상 디스크 크기: 어레이에서 가장 작은 디스크의 용량입니다.</td>
		 <td>
		 <ul><li><b>장점</b>:<ul>
		 <li>읽기 속도가 빠릅니다.</li>
		 <li>데이터 신뢰성이 높아 단일 디스크가 손상되어도 복구할 수 있습니다.</li>
		 </ul>
		 <li><b>단점</b>:<ul>
		 <li>디스크 이용률이 가장 낮습니다.</li>
		 <li>쓰기 속도는 단일 디스크의 쓰기 속도에 의해 제한됩니다.</li>
		 </ul></ul>
		 </td>
		 <td>읽기 성능에 대한 요구가 높고, 쓰기 데이터의 백업 처리가 필요한 시나리오입니다.</td>
     </tr>
	 <tr>
         <td>RAID 01</td>
         <td>먼저 여러 개의 디스크로 RAID 0을 구축한 후 다시 여러 개의 RAID 0으로 RAID 1을 구축합니다.</td>
		 <td><ul><li><b>장점</b>: RAID 0 및 RAID 1의 장점을 모두 갖추고 있습니다.</li>
		 <li><b>단점</b>：<ul><li>비용이 상대적으로 높고 최소 4개의 디스크가 필요합니다.</li><li>단일 디스크가 손상되면 동일 그룹의 디스크를 사용할 수 없습니다.</li></td>
		 <td   rowspan="2">RAID 10 사용을 권장합니다.</td>
     </tr>
	 <tr>
         <td>RAID 10</td>
         <td>먼저 여러 개의 디스크로 RAID 1을 구축한 후 다시 여러 개의 RAID 1으로 RAID 0을 구축합니다.</td>
		 <td><ul><li><b>장점</b>: RAID 0 및 RAID 1의 장점을 모두 갖추고 있습니다.</li>
		 <li><b>단점</b>: 비용이 상대적으로 높고 최소 4개의 디스크가 필요합니다.</li></td>
     </tr>
</table>



##  RAID 구축
>본 문서는 CentOS Cloud Virtual Machine에서 4개의 엘라스틱 CBS를 사용하여 RAID 0을 구축하는 것을 예로 들었습니다. 다양한 운영 체제 및 RAID 레벨에 따라 작업도 다를 수 있습니다. 본 문서는 참조용이므로 구체적인 작업 절차 및 차이점은 대응하는 작업 시스템의 제품 설명서 및 RAID 관련 문서를 참조하십시오.

Linux 커널은 RAID 장치 관리를 위한 md 모듈을 제공하며, 직접 mdadm 툴을 사용하여 md 모듈 호출 및 RAID 0을 생성할 수 있습니다.
![](https://main.qcloudimg.com/raw/a7e717737b22456319cde4ec4bc0c8e1.png)

1. root 사용자는 [클라우드 서버에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 진행하십시오.
2. 다음 커맨드를 실행하여 mdadm을 설치하십시오.
```
yum install mdadm -y
```
설치 성공 결과는 다음 이미지와 같이 표시됩니다.
![](https://main.qcloudimg.com/raw/9ae334a316638ebc8e8b95a587c6e8b5.png)
3. 다음 커맨드를 실행하여 mdadm을 사용하고 RAID 0을 생성하십시오.
```
mdadm --create /dev/md0 --level=0 --raid-devices=4 /dev/vd[cdef]1
```
생성 성공 결과는 다음 이미지와 같이 표시됩니다.
![](https://main.qcloudimg.com/raw/7c2d92dc0cf8225d56c6696127e1a6ce.png)
4. 다음 커맨드를 실행하여 mkfs를 사용해 파일 시스템을 생성하십시오(예: EXT3 파일 시스템 사용).
```
mkfs.ext3 /dev/md0
```
생성 성공 결과는 다음 이미지와 같이 표시됩니다.
![](https://main.qcloudimg.com/raw/ed6291597a03923a46914ff39005c90e.png)
5. 다음 커맨드를 순서대로 실행하여 파일 시스템을 마운트하십시오.
```
mkdir md0/
mount /dev/md0 md0/
tree md0
```
마운트 성공 결과는 다음 이미지와 같이 표시됩니다.
![](https://main.qcloudimg.com/raw/c77863517336227b6dc5dc0180935e46.png)
6. 다음 커맨드를 실행하여 파일 시스템 세부 사항을 확인하고 UUID를 기록하십시오(예시:`c5d8a204: c28853ba: 3882e9f8: 62d078de`). 아래 이미지를 참고하십시오.
```
mdadm --detail --scan
```
![](https://main.qcloudimg.com/raw/bd258e727fc5ca5ee67ffe7ffeddea2a.png)
7. 다음 커맨드를 실행하여 mdadm 구성 파일을 편집하십시오.
```
vi /etc/mdadm.conf
```
8. 편집 모드에서 관련 콘텐츠를 입력하십시오.
엘라스틱 CBS에 다음 구성을 입력할 것을 권장합니다.
```
DEVICE /dev/disk/by-id/virtio-엘라스틱 CBS1ID-part1 
DEVICE /dev/disk/by-id/virtio-엘라스틱 CBS2ID-part1 
DEVICE /dev/disk/by-id/virtio-엘라스틱 CBS3ID-part1 
DEVICE /dev/disk/by-id/virtio-엘라스틱 CBS4ID-part1 
ARRAY 논리 장치 경로 metadata= UUID=
```
논리 장치 경로는 /dev/md0이고 metadata가 1.2를 예로 합니다. 다음을 참조하여 입력하십시오.
```
DEVICE /dev/disk/by-id/virtio-엘라스틱 CBS1ID-part1 
DEVICE /dev/disk/by-id/virtio-엘라스틱 CBS2ID-part1 
DEVICE /dev/disk/by-id/virtio-엘라스틱 CBS3ID-part1 
DEVICE /dev/disk/by-id/virtio-엘라스틱 CBS4ID-part1 
ARRAY /dev/md0 metadata=1.2 UUID=3c2adec2:14cf1fa7:999c29c5:7d739349
```
9. Esc를 누르고 `: wq`를 입력한 후 저장 및 종료하십시오.
