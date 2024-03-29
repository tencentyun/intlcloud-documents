
このドキュメントでは、サーバーでよく使うポートの説明です。Windowsにおけるより多くのサービスアプリケーションポートの詳細については、 Microsoft公式サイトのドキュメント（[Windowsのサービス概要及びネットワークポートの要件](https://support.microsoft.com/zh-cn/help/832017/service-overview-and-network-port-requirements-for-windows?spm=5176.7740724.2.3.omd4DB%3Fspm%3D5176.7740724.2.3.omd4DB)）をご参照ください。

| ポート | サービス | 説明 |
|---------|---------|---------|
| 21 | FTP | FTPサーバーでオーペンされているポート、アップロードとダウンロードに使われます。 |
| 22 | SSH | 22ポートはSSHポートであり、通常のCommand Line InterfaceモードによるLinuxシステムサーバーへのリモート接続に使われています。 |
| 25 | SMTP | SMTPサーバーでオーペンされているポート、メールの送信に使われています。 |
| 80 | HTTP | サイトサービスに使われています。例えば、IIS、Apache、Nginx等は外部アクセスを提供しています。|
| 110 | POP3 | 110ポートはPOP3（メールプロトコル 3）サービスのためにオーペンされています。 |
| 137、138、139 | NETBIOS プロトコル | ポート137および138は、マイネットワーク経由でファイルを転送するためのUDPポートです。<br>139ポート：このポート経由で確立された接続はNetBIOS/SMBサービスの取得を試します。このプロトコルは、WindowsおよびSAMBAでのファイルとプリンターの共有に使用されます。 |
| 143 | IMAP | 143ポートは主に「Internet Message Access Protocol」v2（Internetメッセージアクセスプロトコルであり、IMAPと略称する）に使われており、 POP3 と同じように、電子メールを受信するためのプロトコルです。 |
| 443 | HTTPS | Webブラウジング用のポートであり、暗号化とセキュリティポートを介した転送を提供できるもう1種のHTTPです。 |
| 1433 | SQL Server | 1433ポートはSQL Serverのデフォルトポートです。SQL ServerサービスはTCP-1433とUDP-1434の2つのポートを使っています。そのうち、ポート1433はSQL Serverが外部サービスを提供するために使用され、ポート1434はリクエスタに対してSQL ServerがどのTCP/IP ポートを使っているかを返信することに使われています。 |
| 3306 | MySQL | 3306ポートはMySQLデータベースのデフォルトポートであり、MySQLは外部サービスを提供するために使われています。|
| 3389 | Windows Server Remote Desktop Services（リモートデスクトップサービス）| 3389ポートはWindows  Server リモートデスクトップのサービスポートです。このポートを介して、「リモートデスクトップ」接続ツールでリモートサーバーに接続することができます。 |
| 8080 | プロキシポート | 8080ポートは80ポートと同様に、WWW プロキシサービスに使われています。特定のWebサイトにアクセスする場合、またはプロキシサーバーを使う場合、よくURLに「:8080」ポート番号を追加します。また、Apache Tomcat Webサーバーがインストールされた後のデフォルトのサービスポートはポート8080です。 |
