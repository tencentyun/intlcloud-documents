## 제한과 설명
### 제한 조건

- CFS가 지원하는 파일 시스템 프로토콜: NFS v3.0/v4.0, CIFS/SMB.
- 단일 파일 시스템 용량 한도: 160 TB(그 중 금융 전용 지역 단일 파일 시스템 용량 한도는 40 TB).
- 단일 파일 시스템은 200개 이하의 컴퓨팅 노드 탑재를 지원합니다.
- 사용자당 지역별 사용 가능 파일 시스템 한도는 10개입니다.


### 관련 설명
#### UID와 GID 설명

- NFS v3.0 프로토콜을 사용할 때, 로컬 계정에 파일의 UID 또는 GID가 존재하지 않으면 UID와 GID가 바로 표시됩니다. Linux 로컬 계정에 파일의 UID 또는 GID가 존재하면 로컬 UID와 GID 매핑 관계에 따라 해당하는 사용자 이름과 그룹 이름을 표시합니다.
- NFS v4.0 프로토콜을 사용할 때, Linux 커널 버전이 3.0보다 높으면 UID와 GID 규칙은 NFS v3.0 프로토콜과 동일합니다. 로컬 커널 버전이 3.0보다 낮으면 모든 파일의 UID와 GID는 nobody로 표시됩니다.
- 주의: Linux 커널 버전이 3.0보다 낮은 경우 NFS v4.0 프로토콜을 사용하여 파일 시스템을 탑재하면, 해당 파일 또는 디렉터리의 UID와 GID가 nobody로 변경될 수 있으니 파일 또는 디렉터리에 change owner 또는 change group 작업을 진행하지 않길 권장합니다.


#### 지원되는 CIFS/SMB 프로토콜
- 지원되는 프로토콜 버전: CIFS, SMB 1.0 이상의 SMB 프로토콜 버전을 지원합니다. 단, SMB 1.0 프로토콜을 통한 탑재는 권장하지 않습니다. SMB 1.0은 SMB 2.0 및 그 이후 버전과 프로토콜 디자인상 큰 차이가 있어 성능과 기능면에서 심각하게 뒤떨어지며 SMB1.0 또는 이전 버전 포로토콜의 Windows 제품은 Microsoft에서 더 이상 지원을 받을 수 없기 때문입니다.
- 사용자가 NFS와 SMB를 사용하여 동일 파일 시스템에 접근하는 것을 지원하지 않고, WAN을 통해 SMB 파일 시스템에 접근하는 것도 지원하지 않습니다.
- 파일 시스템 레벨의 읽기/쓰기 권한 제어만 제공하며, 파일/디렉터리 레벨의 ACL 권한 제어는 제공하지 않습니다.
- 희소 파일, 파일 압축, ENI 상태 조회, 재분석 지점 등 IOCTL/FSCTL 작업을 지원하지 않습니다.
- ADS(Alternate Data Streams)를 지원하지 않습니다.
- SMB Direct, SMB Multichannel, SMB Directory Leasing, Persistent File Handle 등 SMB 3.0 및 그 이상 버전의 일부 프로토콜 기능을 지원하지 않습니다. 

 <!--
 * NFS v4.0이 지원하지 않는 특성은 FATTR4_MIMETYPE, FATTR4_QUOTA_AVAIL_HARD, FATTR4_QUOTA_AVAIL_SOFT, FATTR4_QUOTA_USED, FATTR4_TIME_BACKUP, FATTR4_TIME_CREATE을 포함하며 클라이언트는 NFS4ERR_ATTRNOTSUPP 오류를 표시합니다.
 * NFS v4.0이 지원하지 않는 OP는 OP_DELEGPURGE, OP_DELEGRETURN, NFS4_OP_OPENATTR을 포함하며 클라이언트는 NFS4ERR_NOTSUPP 오류를 표시합니다.
 * NFSv4는 Lock과 Delegation 기능을 지원하지 않습니다.
 -->

