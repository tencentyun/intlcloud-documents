Veja abaixo as descrições das portas de servidor comuns. Para obter mais informações sobre as portas de aplicativos de serviços para Windows, consulte o documento oficial da Microsoft ([Visão geral do serviço e requisitos de porta de rede para Windows](https://support.microsoft.com/zh-cn/help/832017/service-overview-and-network-port-requirements-for-windows?spm=5176.7740724.2.3.omd4DB%3Fspm%3D5176.7740724.2.3.omd4DB)).

| Número da porta | Serviço | Descrição |
|---------|---------|---------|
| 21 | FTP | Uma porta de servidor FTP aberta para upload e download. |
| 22 | SSH | A porta 22 é a porta SSH. É usada para conectar remotamente a servidores do Linux no modo CLI. |
| 25 | SMTP | Porta aberta do servidor SMTP para envio de e-mails. |
| 80 | HTTP | Esta porta é usada para serviços Web, como IIS, Apache e Nginx, para fornecer acesso externo. |
| 110 | POP3 | A porta 110 fica aberta para o serviço POP3 (protocolo de e-mail 3). |
| 137, 138, 139 | Protocolo NetBIOS | As portas 137 e 138 são portas UDP para transferência de arquivos pelos Meus locais de rede. <br>Porta 139: as conexões da porta 139 tentam acessar o serviço NetBIOS/SMB. Esse protocolo é usado para compartilhamento de arquivos e impressoras no Windows e SAMBA. |
| 143 | IMAP | A porta 143 é usada principalmente para o protocolo IMAP v2, um protocolo para receber e-mails semelhante ao POP3. |
| 443 | HTTPS | Uma porta de navegação na web. HTTPS é outro tipo de HTTP que fornece criptografia e transmissão por portas seguras. |
| 1433 | SQL Server | A porta 1433 é a padrão do SQL Server. O SQL Server usa duas portas: porta 1433 para TCP e porta 1434 para UDP. A porta 1433 é usada para o SQL Server para fornecer serviços externos, enquanto a porta 1434 é usada para responder ao solicitante em relação a qual porta TCP/IP está sendo usada pelo SQL Server. |
| 3306 | MySQL | A porta 3306 é a padrão para bancos de dados MySQL e é usada para fornecer serviços externos. |
| 3389 | Serviços de área de trabalho remota do Windows Server | A porta 3389 é a porta para serviço de área de trabalho remota do Windows 2000/2003 Server, por meio da qual você pode se conectar a um servidor remoto usando a ferramenta de conexão de área de trabalho remota. |
| 8080 | Porta proxy | Semelhante à porta 80, a porta 8080 é usada para o serviço de proxy WWW para navegação na web. A extensão do número de porta ":8080" costuma ser adicionada ao URL quando os usuários acessam um site ou usam um servidor proxy. Além disso, após a instalação do servidor Web Apache Tomcat, a porta de serviços padrão é a 8080. |
