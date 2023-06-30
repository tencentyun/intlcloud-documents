## 작업 시나리오

Windows 운영 체제는 SID(보안 식별자)를 통해 컴퓨터와 사용자를 식별합니다. 동일한 이미지로 생성된 CVM 인스턴스는 동일한 SID를 가지며 도메인 로그인 문제가 발생할 수 있습니다. Windows 도메인 환경을 구축해야 하는 경우 SID를 수정해야 합니다.
본 문서는 Windows Server 2012 운영 체제의 CVM을 예시로 시스템의 sysprep 및 sidchg 툴을 사용하여 SID를 수정하는 방법을 설명합니다.

## 주의 사항

- 본 설명은 Windows Server 2008 R2,Windows Server 2012 및 Windows Server 2016에만 적용됩니다.
- SID를 일괄 수정하려면 사용자 지정 이미지를 만들 수 있습니다(‘이미지 생성을 위해 sysprep 실행’ 선택).
- SID를 수정하면 데이터 손실 또는 시스템 손상이 발생할 수 있습니다. 시스템 디스크 스냅샷 또는 이미지를 미리 생성하는 것이 좋습니다.

## 작업 방식

### sysprep를 사용하여 SID 수정



<dx-alert infotype="notice" title="">
- sysprep를 사용하여 SID를 수정한 후에는 IP 구성 정보를 포함하여 일부 시스템 매개변수를 수동으로 재설정해야 합니다.
- sysprep를 사용하여 SID를 수정하면 C:\Users\Administrator가 재설정되고 시스템 디스크의 일부 데이터가 지워집니다. 데이터를 백업하십시오.
</dx-alert>


1. [VNC를 사용하여 Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32496).
2. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"> > **실행**을 우클릭하고 **cmd**를 입력한 뒤, **Enter** 키를 눌러 관리자 명령 라인을 엽니다.
3. [](id:step_03)관리자 명령 라인에서 다음 명령을 실행하여 현재 네트워크 구성을 저장합니다.
```shellsession
ipconfig /all
```
4. 관리자 명령 라인에서 다음 명령을 실행하여 sysprep 툴을 엽니다.
```shellsession
C:\Windows\System32\Sysprep\sysprep.exe
```
5. ‘시스템 준비 툴 3.14’ 팝업 창에서 다음과 같이 구성합니다.
- **시스템 정리 작업**을 **시스템 OOBE(Out-of-Box Experience) 시작**으로 설정하고 ‘일반’을 선택합니다.
   - **종료 옵션**을 **재부팅**으로 설정합니다.
6. **확인**을 클릭하면 시스템이 자동으로 다시 시작됩니다.
7. 시작이 완료되면 마법사를 따라 구성을 완료합니다(언어 선택, 비밀번호 재설정 등).
8. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"> > **실행**을 우클릭하고 **cmd**를 입력한 뒤, **Enter** 키를 눌러 관리자 명령 라인을 엽니다.
9. 다음 명령을 실행하여 SID가 수정되었는지 확인합니다.
```shellsession
whoami /user
```
다음과 유사한 메시지가 반환되면 SID가 수정된 것입니다.
![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)

10. [3단계](#step_03)에서 저장한 네트워크 구성 정보를 기반으로 ENI 정보(예: IP 주소, 게이트웨이 주소, DNS 등)를 재설정합니다.


### sidchg를 사용하여 SID 수정

1. CVM에 로그인합니다.
2. IE 브라우저를 통해 sidchg 툴에 액세스하고 다운로드하십시오.
sidchg 툴 다운로드 주소: `http://www.stratesave.com/html/sidchg.html`
3. 아래와 같이 관리자 명령 라인을 사용하여 다음 명령을 실행하고 sidchg 툴을 엽니다.
예를 들어, sidchg 툴은 C: 드라이브에 저장되며 이름은 sidchg64-2.0p.exe입니다.
![](https://main.qcloudimg.com/raw/284926ae1eae88228fb009f247b82068.png)
`/R` 은 수정 후 자동 재시작을  나타내고,` /S` 는 수정 후 종료를 나타냅니다. 자세한 내용은 [SIDCHG 공식 설명](http://www.stratesave.com/html/sidchg.html)을 참고하십시오.
4. 페이지의 프롬프트에 따라 license key 또는  trial key입력하고 **Enter** 키를 누릅니다.
5. 페이지의 프롬프트에 따라 **Y**를 입력하고 아래와 같이 **Enter** 키를 누릅니다.
![](https://main.qcloudimg.com/raw/43c19634475517b183402d15fa32e962.png)
6. SID를 수정하라는 프롬프트 상자에서 **확인**을 클릭하여 아래와 같이 SID를 재설정합니다.
재설정하는 동안 시스템이 다시 시작됩니다.
![](https://main.qcloudimg.com/raw/b59ec21417cc0de1fd7d851fcd8a2a3b.png)
7. 시작이 완료되면 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;"> > **실행**을 우클릭하고, **cmd**를 입력한 뒤, **Enter** 키를 눌러 관리자 명령 라인을 엽니다.
8. 다음 명령을 실행하여 SID가 수정되었는지 확인합니다.
```shellsession
whoami /user
```
다음과 유사한 메시지가 반환되면 SID가 수정된 것입니다.
![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)


