
Este documento descreve as portas de servidor comuns. Para obter mais informações sobre as portas de aplicativos de serviços para Windows, consulte a [Visão geral do serviço e requisitos de porta de rede para Windows](https://support.microsoft.com/zh-cn/help/832017/service-overview-and-network-port-requirements-for-windows?spm=5176.7740724.2.3.omd4DB%3Fspm%3D5176.7740724.2.3.omd4DB).

| Porta | Serviço | Descrição |
|---------|---------|---------|
| 21 | FTP | Uma porta de servidor FTP aberta para upload e download. |
| 22 | SSH | Uma porta SSH para conexão remota a servidores do Linux no modo CLI. |
| 25 | SMTP | Uma porta de servidor SMTP aberta para envio de e-mails. |
| 80 | HTTP | Uma porta para serviços Web, como IIS, Apache e Nginx, para fornecer acesso externo. |
| 110 | POP3 | Uma porta para o serviço POP3 (protocolo de e-mail 3). |
| 137, 138, 139 | Protocolo NetBIOS | As portas 137 e 138 são portas UDP para transferência de arquivos pelos Meus locais de rede. <br>Porta 139: as conexões estabelecidas por meio da porta 139 tentam acessar o serviço NetBIOS/SMB. Esse protocolo é usado para compartilhamento de arquivos e impressoras no Windows e SAMBA. |
| 143 | IMAP | Uma porta para o protocolo Internet Message Access Protocol (IMAP) v2, que é um protocolo para receber e-mails como POP3. |
| 443 | HTTPS | Uma porta para navegação na web. HTTPS é uma variante do HTTP que fornece criptografia e transmissão por portas seguras. |
| 1433 | SQL Server | Porta padrão para o SQL Server. O serviço SQL Server usa duas portas: TCP-1433 e UDP-1434. A porta 1433 é usada para fornecer serviços externos e a porta 1434 é usada para retornar uma resposta ao solicitante para indicar a porta TCP/IP usada pelo SQL Server. |
| 3306 | MySQL | Porta padrão para bancos de dados MySQL, que é usada pelo MySQL para fornecer serviços externos. |
| 3389 | Serviços de área de trabalho remota do Windows Server | Porta de serviços para a área de trabalho remota do Windows Server, por meio da qual é possível se conectar a um servidor remoto usando a ferramenta de conexão "Área de trabalho remota". |
| 8080 | Porta proxy | Semelhante à porta 80, a porta 8080 é usada no serviço de proxy WWW para navegação na web. O número de porta ":8080" costuma ser adicionado ao URL quando você acessa um site ou usa um proxy. Além disso, após a instalação do servidor Web Apache Tomcat, sua porta de serviços padrão é a porta 8080. |
