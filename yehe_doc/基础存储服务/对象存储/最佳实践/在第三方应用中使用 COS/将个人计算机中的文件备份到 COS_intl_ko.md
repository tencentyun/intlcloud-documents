## 서문

데이터의 가치가 무한하다는 데에는 누구도 이견이 없을 것입니다. 디지털 사진, 전자 문서, 업무 자료, 게임 아카이브 등 잃어버렸을 때 곤란하지 않을 데이터는 없습니다. 디스크 장애로 인한 파일 손실뿐 아니라 조작 오류, 컴퓨터 다운 또는 소프트웨어 크래쉬로 인한 파일 손실, '버전 롤백'이 필요할 때 저장된 이전 버전이 없다면 매우 당황스럽습니다. 그러니 백업의 중요성은 두말할 필요도 없지요.

백업이라고 하면 외장 하드 또는 LAN에 구축한 NAS 스토리지에 파일을 업로드하면 그만이라고 생각하는 사람이 많습니다. 정말 실제로도 이렇게 간단할까요?

백업은 사실 하나의 시스템 프로세스입니다. 파일을 백업 매체에 복사하는 것뿐만 아니라 백업 내용의 정확성도 검증해야 합니다. 복사와 검증은 파일 손실 시의 피해를 최소화할 수 있도록 정기적으로 실시해야 합니다. 또한 백업 매체도 점검이 필요하며, 손상된 디스크는 즉시 교체해야 합니다.

그렇다면 파일의 안전을 보장할 수 있는 간단한 방법은 없을까요? 답은 '있습니다'.

클라우드 서비스가 발전함에 따라 신뢰할 만한 기업급 클라우드 스토리지 서비스가 생겨났고, Tencent Cloud COS 객체 스토리지가 바로 이런 서비스입니다. 속도를 높이고 비용을 절감하고자 하는 정부의 노력에 부응하여 더욱 빠르고 저렴한 광대역이 등장함으로써 클라우드 파일 백업은 이미 상용화되었습니다. 이제는 컴퓨터의 파일과 클라우드 스토리지를 연결하여 파일을 정기적으로 클라우드에 자동 백업하고 백업 파일의 정확성을 검증하는 소프트웨어가 필요합니다.

## 소프트웨어 소개

[Arq® Backup](https://www.arqbackup.com/)은 Windows와 macOS 시스템을 지원하는 비즈니스 백업 소프트웨어입니다. 시스템 백그라운드에서 실행되며 설정에 따라 일정 시간마다 지정 디렉터리를 자동 백업하고, 매시간 파일을 백업해 두기 때문에 파일의 이전 버전을 쉽게 찾을 수 있습니다. 또한 시간마다 실행되는 백업은 변경 사항이 있는 파일만 백업하고 경로가 다른 중복 파일은 한 번만 백업함으로써 백업 용량을 최대한 작게, 백업 속도는 최대한 빠르게 합니다. 백업 파일을 네트워크로 전송하기 전, 소프트웨어는 네트워크 전송 과정 또는 클라우드 스토리지에서 도용되는 일이 없도록 사용자가 입력한 비밀번호를 바탕으로 백업 파일을 암호화하여 중요 데이터의 보안성을 보장합니다.

Arq® Backup 비즈니스 라이선스는 사용자 1명당 49.99USD입니다. 사용자는 구매 후 한 대의 컴퓨터에서 사용할 수 있습니다. 소프트웨어는 30일 무료 사용이 가능하므로 직접 사용해본 후 구매할 수도 있습니다.

> ?Arq® Backup 소프트웨어는 현재 중국어 간체 버전이 없습니다. 소프트웨어의 다운로드, 구매 및 관련 설명은 해당 소프트웨어의 [공식 홈페이지](https://www.arqbackup.com/)에서 확인할 수 있습니다.

## Tencent Cloud COS 준비

> ?현재 COS를 사용 중인 경우 1-2단계는 생략합니다.

1. [Tencent Cloud 계정 생성](https://intl.cloud.tencent.com/document/product/378/17985) 및 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)을 완료합니다. 실명 인증을 하지 않은 사용자는 중국 내 리소스를 구매할 수 없습니다.
2. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하여 지시에 따라 COS를 활성화합니다.
3. COS 콘솔에서 왼쪽 메뉴의 **버킷 리스트** 클릭 후 **버킷 생성**을 클릭하여 버킷 생성을 시작합니다.
	- 이름: 버킷 이름입니다(예: “backups”).
	- 소속 리전: 귀하의 소재지와 가까운 곳을 선택할 수 있으나 금융 클라우드 리전은 선택하지 마십시오. 현재 서남 리전에 가격 할인 혜택이 있으므로 '청두' 또는 '충칭'을 선택하면 가격 할인 혜택을 받을 수 있습니다.
    ![](https://main.qcloudimg.com/raw/d9caa38d7216c4270ff2a0fc096405fa.png)
  기타 설정 항목은 기본값을 유지합니다. **도메인 요청** 주소를 복사 및 저장한 후 **확인**을 클릭하여 생성을 완료합니다.
> ?자세한 버킷 생성 순서는 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)을 참조하십시오.
4. [API Keys 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인하여 키 정보 SecretId와 SecretKey를 생성 및 기록합니다.
   ![](https://main.qcloudimg.com/raw/5a78bab4cb211503b5c3ff54e5551eb3.png)

## Arq® Backup 설치 및 설정

> ?본 문서는 Windows의 Arq Backup 6.2.11 버전을 예시로 사용하였습니다.

1. [Arq® Backup 공식 홈페이지](https://www.arqbackup.com/)에서 소프트웨어를 다운로드합니다.
2. 지시에 따라 소프트웨어 설치를 완료하면 소프트웨어가 자동으로 실행됩니다. 최초 실행 시 로그인 알림이 뜹니다. 이때 이메일 주소를 입력하고 [Start Trial]을 클릭합니다.
   ![](https://main.qcloudimg.com/raw/b9ea1e5cebb30c96fe5894bb5adb7214.png)
3.**Backup** 인터페이스에서**Create a new backup plan** 을 클릭하고 백업 플랜을 추가합니다.
   ![](https://main.qcloudimg.com/raw/397c1b77f1a3871644ef9eec63ebda7e.png)
4. 리디렉션 인터페이스에서 백업할 디렉터리를 선택합니다. 전체 디스크 또는 지정 디렉터리를 선택할 수 있습니다.
   ![](https://main.qcloudimg.com/raw/410a0f1728cda892f375c89103b46531.png)
5.**Add storage location** 을 클릭하고 아래 이미지와 같이 백업 스토리지 위치를 추가합니다.
   ![](https://main.qcloudimg.com/raw/a8d33f582c5600eec6c67893f2ee3c46.png)
6.**S3-Compatible Server** 를 클릭합니다.
   ![](https://main.qcloudimg.com/raw/9d515b8ef332dc00a4f7a9277b70eef1.png)
7. 리디렉션 인터페이스에서 다음 설명에 따라 설정합니다. 설정 완료 후**Continue** 를 클릭합니다.
   - Server URL: 위에 기록된 도메인 요청 중 `cos`로 시작하면서 앞에 `https://`가 있는 주소를 입력합니다(예: `https://cos.ap-chengdu.myqcloud.com`). 버킷 이름은 포함되어 있지 않다는 것에 주의하십시오.
   - Access Key ID: 위에 기록된 키 정보 중 SecretId입니다.
   - Secret Access Key: 위에 기록된 키 정보 중 SecretKey입니다.
     ![](https://main.qcloudimg.com/raw/bfe1454b37d756068a61050d4585e451.png)
8. 다음 인터페이스에서**Use an existing bucket** 을 선택한 후 위에서 생성한 버킷(예: backups-1250000000)을 선택하고**Save** 를 클릭합니다.
   ![](https://main.qcloudimg.com/raw/bcb5223dad1ac34ce642c0ecdff184b1.png)
9. (옵션) 백업 데이터 암호화 여부를 선택합니다. **활성화** 버튼을 선택합니다.
   ![](https://main.qcloudimg.com/raw/8744311c148e6ebbc2a35c230de76002.png)
10. 팝업 창에서 암호화에 사용되는 비밀번호를 설정합니다. 백업 파일 암호화에 사용되는 비밀번호를 두 번 입력하고**OK** 를 클릭합니다. **주의: 백업 비밀번호를 기억하지 않으면 백업에서 파일을 복구할 수 없습니다!**
    ![](https://main.qcloudimg.com/raw/43213532f56da02450b1ea52321457c6.png)
11. (옵션) 백업 주기를 설정합니다.
    ![](https://main.qcloudimg.com/raw/92a00ca49471007336c34471bec8fa6d.png)
12.**Save** 를 클릭하여 설정을 저장한 후**Back Up Now** 를 클릭하여 백업을 시작합니다.
    ![](https://main.qcloudimg.com/raw/65093effc29b66385f8ee20f293cde01.png)


## 백업에서 파일 복구

1. 메인 인터페이스 왼쪽 **Backup** 리스트에서**Restore** 를 클릭합니다.
   ![](https://main.qcloudimg.com/raw/844349292e7fd2d89441fe37c789349e.png)
2. 위의 9단계에서 백업 데이터 암호화를 설정한 경우 비밀번호를 입력해야 합니다.
   ![](https://main.qcloudimg.com/raw/41360bd0dbaa4b131a42d56d43d1eae5.png)
3. 복구할 디렉터리 또는 파일 및 복구한 디렉터리 또는 파일의 저장 위치를 선택한 후 **Restore** 를 클릭하여 복구를 시작합니다.
   ![](https://main.qcloudimg.com/raw/513d4c1f317834a55d7ad1f1f93a3d80.png)
4. 복구 작업은 기본적으로 최신 백업에서 복구됩니다. 필요에 따라 스냅샷에서 이전 버전 백업을 찾아 이전 버전 백업에서 복구를 진행할 수도 있습니다.**Snapshots** 를 클릭하여 이전 스냅샷을 조회합니다.
   ![](https://main.qcloudimg.com/raw/6c37ee6a7450dbf8ad1a7198b43ec247.png)
5. 이전 스냅샷을 선택합니다.
   ![](https://main.qcloudimg.com/raw/b1e02efe3b3e018a8cadd1a1203a6efa.png)
6. 복구할 디렉터리 또는 파일 및 복구한 디렉터리 또는 파일의 저장 위치를 선택한 후 **Restore** 를 클릭하여 복구를 시작합니다. 
7. 복구가 완료되었다는 인터페이스 안내가 뜨면 조금 전 지정한 디렉터리에서 복구된 파일을 확인할 수 있습니다.


