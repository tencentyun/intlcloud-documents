## 작업 시나리오
도메인 입력 및 도메인 계정으로 Windows CVM에 로그인해야 하는 사용자는 사용자 정의 이미지를 생성하기 전에 Sysprep 작업을 통해 인스턴스에 도메인을 입력함으로써 SID의 고유성을 보장할 수 있습니다. 그러지 않을 경우, 사용자 정의 이미지를 통해 생성된 CVM 안에는 기존 인스턴스 관련 정보(동일한 SID 정보 등)가 포함되어 있기 때문에 도메인 연결에 실패할 수 있습니다. Windows CVM에 도메인 입력 등 작업이 필요하지 않다면 해당 작업을 건너뛸 수 있습니다.

본 문서는 Windows Server 2012 R2 64비트 운영 체제를 예로, Windows 운영 체제에서 Sysprep을 실행하여 Windows CVM에 도메인을 입력한 후 SID가 고유성을 갖도록 만드는 방법을 안내합니다.

더 자세한 Sysprep 정보는 `https://technet.microsoft.com/zh-cn/library/cc721940(v=ws.10).aspx`를 참조 바랍니다.


## 주의 사항

- Windows CVM은 반드시 정품 Windows 운영 체제여야 하며, 활성화되어 있어야 합니다.
- 사용자의 Windows CVM이 공용 이미지가 아닌 방식으로 생성되었다면, 해당 CVM은 원래 이미지에 기본으로 포함된 Sysprep 버전만 지원하며, 항상 `%WINDIR%\system32\sysprep` 디렉터리에서 실행해야 합니다.
-  반드시 잔여 Windows 초기화 횟수가 1 이상 남아 있어야 합니다. 그러지 않을 경우 Sysprep 캡슐화를 실행할 수 없습니다.
`slmgr.vbs /dlv` 명령어를 실행하여 잔여 Windows 초기화 횟수를 조회할 수 있습니다.
-  Windows CVM의 Cloudbase-Init 계정은 Cloudbase-Init 프록시 프로그램의 내장 계정으로, CVM 시작 시 메타데이터 획득 및 관련 설정 실행에 사용됩니다. 사용자가 해당 계정을 수정/삭제하거나 Cloudbase-Init 프록시 프로그램을 제거할 경우, 해당 CVM이 생성한 사용자 정의 이미지를 통해 생성한 CVM을 초기화할 때 사용자 정의 정보 입력에 실패할 수 있습니다. 따라서, Cloudbase-init 계정을 수정하거나 삭제하지 말 것을 권장합니다.  

## 전제 조건

- Administrator 계정으로 [Windows CVM에 로그인](https://intl.cloud.tencent.com/document/product/213/5435)한 상태.
- [Windows CVM에 Cloudbase-Init를 설치](https://intl.cloud.tencent.com/document/product/213/32364)한 상태.

## 작업 순서

1. 운영 체제 인터페이스에서 src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png"></img>를 클릭하여 “Windows PowerShell ” 창을 엽니다.
2. Windows PowerShell 창에서 다음의 명령어를 실행하여 Cloudbase-init 툴의 설치 경로에 액세스합니다.
> Cloudbase-init 툴을 `C:\Program Files\Cloudbase Solutions\` 디렉터리에 설치를 예로 듭니다.
>
```
cd 'C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf'
```
3. 다음 명령어를 실행하여 Windows 시스템에 대해 캡슐화를 진행합니다.
> 
> - 다음의 명령어를 실행할 때, 명령어에 반드시 `/unattend:Unattend.xml`가 포함되어야 합니다. 그러지 않을 경우 현재 CVM의 사용자 이름, 비밀번호 등 중요한 설정 정보가 초기화될 수 있습니다. 나중에 해당 이미지로 CVM을 생성할 때, 로그인 방식에 “이미지 설정 유지”를 선택하면 CVM 시작 후 해당 CVM의 사용자 이름과 비밀번호를 수동으로 설정해야 합니다.
> - 다음의 명령어를 실행하면 CVM이 자동 종료됩니다. 나중에 해당 이미지로 생성한 CVM의 SID가 고유성을 갖도록 보장하기 위해, 사용자 정의 이미지를 생성하기 전에 해당 CVM을 재시작하지 마시기를 바랍니다. 그렇지 않을 경우 해당 작업이 현재의 CVM에만 적용됩니다.  
> -Windows Server 2012 및 Windows Server 2012 R2의 운영 체제에서 다음의 명령어를 실행하면 해당 CVM의 계정(Administrator)과 비밀번호가 삭제됩니다. CVM을 재시작한 후 계정과 비밀번호를 재설정하고 보관에 유의하시기 바랍니다. 구체적인 작업 순서는 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조 바랍니다.
> 
```
C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /unattend:Unattend.xml
```
4. [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942)을 참조하여 Sysprep 작업을 진행할 CVM 인스턴스를 이미지로 만들고, 해당 이미지를 사용하여 CVM 인스턴스를 생성합니다.
새로 생성한 모든 CVM 인스턴스가 도메인에 연결한 후에는 고유한 SID를 가질 수 있습니다.
> `whoami /user` 명령어를 실행하여 CVM의 SID를 조회할 수 있습니다.
>


