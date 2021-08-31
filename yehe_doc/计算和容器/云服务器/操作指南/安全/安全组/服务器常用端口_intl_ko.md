
다음은 서버에서 자주 사용하는 포트에 대해 소개하며, Windows와 관련된 더 많은 서비스 애플리케이션 포트는 Microsoft 공식 문서([Windows의 서비스 개요 및 네트워크 포트 요구 사항](https://support.microsoft.com/zh-cn/help/832017/service-overview-and-network-port-requirements-for-windows?spm=5176.7740724.2.3.omd4DB%3Fspm%3D5176.7740724.2.3.omd4DB))을 참조 바랍니다.

| 포트 | 서비스 | 설명 |
|---------|---------|---------|
| 21 | FTP | FTP 서버에서 개방한 포트로 업로드 및 다운로드에 사용됩니다. |
| 22 | SSH | 22 포트는 SSH 포트로 커맨드 라인 모드를 통한 Linux 시스템 서버 원격 연결에 사용됩니다. |
| 25 | SMTP | SMTP 서버에서 개방한 포트로 이메일 발송에 사용됩니다. |
| 80 | HTTP | IIS, Apache, Nginx 등 웹 사이트 서비스의 외부 액세스 제공에 사용됩니다. |
| 110 | POP3 | 110 포트는 POP3(이메일 프로토콜 3) 서비스를 위해 개방됩니다. |
| 137, 138, 139 | NETBIOS 프로토콜 | 그중 137, 138은 UDP 포트로 네트워크 환경을 통해 파일을 전송할 때 사용됩니다. <br> 139 포트: 이 포트를 통해 접속한 연결은 NetBIOS/SMB 서비스를 얻도록 시도합니다. 이 프로토콜은 Windows 파일, 프린터 공유와 SAMBA에 사용됩니다. |
| 143 | IMAP | 143 포트는 "Internet Message Access Protocol"v2(Internet 정보 액세스 프로토콜, 약칭 IMAP)에 주로 사용하며, POP3 같은 이메일 수신에 사용하는 프로토콜입니다. |
| 443 | HTTPS | 웹 브라우징 포트로써 암호화 기능을 제공하고, 보안 포트를 통해 전송하는 또 하나의 HTTP 입니다. |
| 1433 | SQL Server | 1433 포트는 SQL Server의 기본 포트로, SQL Server 서비스는 TCP-1433, UDP-1434 두 개의 포트를 사용됩니다. 그중 1433은 SQL Server가 외부 서비스를 제공하는 데 사용하며, 1434는 SQL Server가 사용하는 TCP/IP 포트를 요청자에게 리턴하는 데 사용됩니다. |
| 3306 | MySQL | 3306 포트는 MySQL 데이터베이스의 기본 포트로 MySQL이 외부 서비스를 제공하는 데 사용됩니다. |
| 3389 | Windows Server Remote Desktop Services(원격 데스크톱 서비스) | 3389 포트는 Windows Server의 원격 데스크톱 서비스 포트로, 이 포트를 통해 "원격 데스크톱" 연결 툴을 사용하여 원격 서버에 연결할 수 있습니다. |
| 8080 | 프록시 포트 | 8080 포트는 80 포트와 같이 WWW 프록시 서비스에 사용됩니다. 웹 브라우징을 구현할 수 있고, 웹 사이트에 액세스하거나 프록시 서버를 사용할 경우 ":8080" 포트 번호가 추가됩니다. 이외에, Apache Tomcat web server 설치 후의 기본 서비스 포트도 8080입니다. |
