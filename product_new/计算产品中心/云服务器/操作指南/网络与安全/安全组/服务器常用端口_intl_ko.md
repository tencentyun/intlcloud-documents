
다음은 서버에서 자주 사용하는 포트에 대해 소개하며, Windows의 추가 서비스 애플리케이션 포트에 관해 설명합니다. Microsoft 공식 문서([Windows의 서비스 개요 및 네트워크 포트 요구 사항](https://support.microsoft.com/zh-cn/help/832017/service-overview-and-network-port-requirements-for-windows?spm=5176.7740724.2.3.omd4DB%3Fspm%3D5176.7740724.2.3.omd4DB))을 참조하십시오.

| 포트 | 서비스 | 설명 |
|---------|---------|---------|
| 21 | FTP | FTP 서버가 개방한 포트로써 업로드, 다운로드에 사용합니다. |
| 22 | SSH | 22 포트는 SSH 포트로써 커맨드 라인 모드를 통해 Linux 시스템 서버 원격 연결에 사용합니다. |
| 25 | SMTP | SMTP 서버가 개방한 포트로써 이메일 발송에 사용합니다. |
| 80 | HTTP | IIS, Apache, Nginx 등의 네트워크 서비스에 대한 외부 액세스 제공에 사용합니다. |
| 110 | POP3 | 110 포트는 POP3(이메일 프로토콜 3) 서비스를 위해 개방됩니다. |
| 137, 138, 139 | NETBIOS 프로토콜 | 137 및 138은 UDP 포트이며 네트워크 환경을 통해 파일을 전송할 때 사용합니다. <br> 139 포트: 이 포트를 통해 진입된 연결은 NetBIOS/SMB 서비스를 얻기 위한 시도를 합니다. 이 프로토콜은 Windows 파일과 프린터 공유와 SAMBA에 사용됩니다. |
| 143 | IMAP | 143 포트는 "Internet Message AccessProtocol"v2(Internet 정보 액세스 프로토콜，약칭 IMAP), POP3와 같은 이메일 수신을 위해 사용하는 프로토콜입니다. |
| 443 | HTTPS | 웹 브라우징 포트로써 암호화 기능 및 보안 포트를 통한 다른 HTTP 전송 기능을 제공합니다. |
| 1433 | SQL Server | 1433 포트는 SQL Server의 기본 포트로써 SQL Server 서비스는 TCP-1433, UDP-1434 두 개의 포트를 사용합니다. 1443은 SQL Server가 외부 서비스를 제공하는 데 사용하며, 1434는 SQL Server가 사용하는 TCP/IP 포트를 요청자에게 리턴하는 데 사용합니다. |
| 3306 | MySQL | 3306 포트는 MySQL 데이터베이스의 기본 포트로써 MySQL가 외부 서비스를 제공하는 데 사용합니다. |
| 3389 | Windows Server Remote Desktop Services(원격 데스크톱 서비스) | 3389 포트는 Windows  2000(2003) Server의 원격 데스크톱 서비스 포트로써 "원격 데스크톱" 연결 툴을 사용해 원격 서버에 연결합니다. |
| 8080 | 프록시 포트 | 8080 포트는 80 포트와 같이 WWW 프록시 서비스에 사용됩니다. 웹 브라우징을 구현하거나 웹 사이트에 액세스하거나 또는 프록시 서버를 사용할 경우, “:8080” 포트 번호가 추가됩니다. 이외에, Apache Tomcat web server 설치 후의 기본 서비스 포트도 8080입니다. |
