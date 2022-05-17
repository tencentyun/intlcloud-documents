## Visão geral
Este documento apresenta como construir o Microsoft SharePoint 2016 em uma instância CVM.

## Versões de software
Este documento usa a instância CVM com a seguinte especificação de hardware como exemplo:
- vCPU: 4 núcleos
- Memória: 8 GB

Este documento usa as seguintes versões de software como exemplo:
- Sistema operacional: Windows Server 2012 R2 Datacenter 64 bits (Inglês)
- Base de dados: SQL Server 2014

## Pré-requisitos
Aquisição de uma instância do CVM Windows. Se você ainda não o fez, consulte [Personalização das configurações do CVM Windows](https://intl.cloud.tencent.com/document/product/213/10516).

## Instruções

### Etapa 1: fazer login em uma instância Windows
Você pode [fazer login em uma instância do Windows usando o arquivo RDP (recomendado)](https://intl.cloud.tencent.com/document/product/213/5435) ou [fazer login em uma instância do Windows através da área de trabalho remota](https://intl.cloud.tencent.com/document/product/213/32498).

<span id="AddAD_DHCP_DNS_IIS"></span>
### Etapa 2: adicionar serviços AD, DHCP, DNS e IIS
1. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> para abrir o **Server Manager (Gerenciador do servidor)**.
2. Selecione **Local Server (Servidor Local)** na barra lateral esquerda e localize **IE Enhanced Security Configuration (Configuração de segurança do IE aprimorada)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/c2b0791555bbc910cea70732c75daa0f.png)
3. Desative a **IE Enhanced Security Configuration (Configuração de segurança do IE aprimorada)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/6acbf171bc703100401e48e362539b21.png)
4. Selecione **Dashboard (Painel)** na barra lateral esquerda e clique em **Add roles and features (Adicionar funções e recursos)**.
5. Na janela "Add Roles and Features Wizard (Assistente para adicionar funções e recursos)", mantenha as configurações padrão e clique em **Next (Avançar)** 3 vezes.
6. Na página **Server Roles (Funções do servidor)**, selecione **Active Directory Domain Services (Serviços de domínio do diretório ativo)**, **DHCP Server (Servidor DHCP)**, **DNS Server (Servidor DNS)**, **Web Server (IIS) (Servidor web (IIS))** e clique em **Add Features (Adicionar recursos)** na janela pop-up, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/a2bb1c86c9277ca870c629ecf5b0d3f5.png)
7. Clique em **Next (Avançar)**.
8. Na página **Features (Recursos)**, selecione **.NET Framework 3.5 Features (Recursos do .NET Framework 3.5)** para adicionar recursos, conforme mostrado abaixo:.
![](https://main.qcloudimg.com/raw/bf47abbb95ad42b9d6c720c3bb2c846b.png)
9. Mantenha as configurações padrão e clique em **Next (Avançar)** até que a página **Confirmation (Confirmação)** apareça.
10. Confirme a instalação e clique em **Install (Instalar)**.
11. Após a conclusão da instalação, reinicie o CVM
12. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> para abrir o **Server Manager (Gerenciador do servidor)**.
13. Clique em <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> e selecione **Promote this server to a domain controller (Promover este servidor a um controlador de domínio)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/1e6aa1d75044898357709909bb969c6f.png)
14. <span id="step14"></span>Na janela **Active Directory Domain Services Configuration Wizard (Assistente de configuração dos serviços de domínio Active Directory)**, selecione **Add a new forest (Adicionar nova floresta)**, insira um nome de domínio no campo **Root domain name (Nome do domínio raiz)** e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/017acc0e5939632f3808698f36320fd2.png)
15. <span id="step15"></span>Em **Type Directory Services Restore Mode (DSRM) password (Digitar senha do modo de restauração dos serviços de diretório (DSRM))**, defina a senha e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/078672b95294790e4985108bd58d8504.png)
16. Mantenha as configurações padrão e clique em **Next (Avançar)** até que a configuração seja concluída.
17. Clique em **Install (Instalar)**.
18. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> para abrir o **Server Manager (Gerenciador do servidor)**.
19. Clique em <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin: 0;"></img> e selecione **Complete DHCP configuration (Configuração DHCP completa)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/4c65a7990acc647866d73c1b5ba20a6c.png)
20. Na janela **DHCP Post-Install configuration wizard (Assistente de configuração pós-instalação DHCP)**, clique em **Next (Avançar)**.
21. Mantenha as configurações padrão e clique em **Commit (Confirmar)** para concluir a instalação.
![](https://main.qcloudimg.com/raw/4162a8fbde1b7af1d8fadacaa61965cf.png)
22. Clique em **Close (Fechar)**.

### Etapa 3: instalar o banco de dados SQL Server 2014

1. Abra o navegador no CVM e baixe o pacote de instalação do site oficial do SQL Server 2014.
> Você também pode obter o pacote de instalação do SQL Server 2014 em um site de terceiros ou outros canais válidos.
>
2. Clique duas vezes no arquivo "Setup.exe" para iniciar o assistente de instalação, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/f2cc33aef5ec2662238ffeca56d08a7d.png)
3. Selecione **New SQL Server stand-alone installation or add features to an existing installation (Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente)**.
4. Na página **Product Key (Chave do produto)**, insira a chave do produto e clique em **Next (Avançar)**.
5. Selecione **I accept the license terms (Aceito os termos da licença)** e clique em **Next (Avançar)**.
6. Mantenha as configurações padrão e clique em **Next (Avançar)**.
7. Depois que a verificação da instalação for concluída, clique em **Next (Avançar)**.
8. Mantenha as configurações padrão e clique em **Next (Avançar)**.
9. Na página **Feature Selection (Seleção de recursos)**, clique em **Select All (Selecionar tudo)** para selecionar todos os recursos e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/92eac7b681dae5937bafa484874ae122.png)
10. Na página **Instance Configuration (Configuração da instância)**, selecione **Default instance (Instância padrão)** e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/2bf1682b927b66224c574435ee35e7af.png)
11. Na página **Server Configuration -> Service Accounts (Configuração do servidor -> Contas de serviço)**, configure a conta e a senha do SQL Server Database Engine e do SQL Server Analysis Services e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/1310d9db077772be6dad6f58a698273e.png)
 - Defina o nome da conta de **SQL Server Database Engine** como "NT AUTHORITY\NETWORK SERVICE".
 - Defina o nome da conta e a senha do **SQL Server Analysis Services** para o nome de domínio e a senha configurados em [14](#step14) para [15](#step15) na [Etapa 2: adicionar AD, DHCP, DNS e serviços IIS](#AddAD_DHCP_DNS_IIS).
12. Na página **Database Engine Configuration -> Server Configuration (Configuração do Database Engine -> Configuração do servidor)**, selecione **Add Current User (Adicionar usuário atual)** para usar a conta atual como a conta de administrador do SQL Server e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/90ac80988b45a6b08650d97fd0d08c09.png)
13. Na página **Analysis Services Configuration -> Account Provisioning (Configuração dos serviços de análise -> Provisionamento de conta)**, selecione **Add Current User (Adicionar usuário atual)** para conceder à conta atual permissões de administrador para Serviços de análise e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/5fda4e9b2ac31d8394ab0dfa14847d73.png)
14. Mantenha as configurações padrão e clique em **Next (Avançar)**.
15. Na página **Distributed Replay Controller (Controlador de reprodução distribuído)**, clique em **Add Current User (Adicionar usuário atual)** para conceder à conta atual permissões de acesso para o serviço do Controlador de reprodução distribuído.
![](https://main.qcloudimg.com/raw/2b67cc38051c51cb88ba7bbb740027b3.png)
16. Mantenha as configurações padrão e clique em **Next (Avançar)**.
17. Confirme as configurações do SQL Server e clique em **Install (Instalar)**.
18. Após a conclusão da instalação, clique em **Close (Fechar)**.


### Etapa 4: instalar o SharePoint 2016

1. Abra o navegador no CVM e faça download do pacote de instalação do site oficial do Microsoft SharePoint 2016.
2. Abra o arquivo de imagem "Microsoft SharePoint 2016", clique duas vezes no arquivo executável `prerequisiteinstaller.exe` da ferramenta de preparação para instalar a Preparation Tool (Ferramenta de preparação) do Microsoft SharePoint 2016, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/1c6c2e0970ea456bbabd4a77ef454a5e.png)
3. Abra o assistente de instalação da Preparation Tool (Ferramenta de preparação) do Microsoft SharePoint 2016 e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/4b42cde60ca558a7c905c6f8031e3a50.png)
4. Selecione **I accept the terms of the License Agreement(s) (Aceito os termos do(s) contrato(s) de licença)** e clique em **Next (Avançar)**.
5. Depois que a ferramenta de preparação for instalada, clique em **Finish (Concluir)** para reiniciar o CVM.
![](https://main.qcloudimg.com/raw/a8c14625c359decb9941511e267ea2a6.png)
6. Abra o arquivo de imagem "Microsoft SharePoint 2016", clique duas vezes no arquivo de instalação `setup.exe` para instalar o Microsoft SharePoint 2016.
![](https://main.qcloudimg.com/raw/2614739955551657148d9c3a72e566df.png)
7. Insira a chave do produto e clique em **Continue (Continuar)**.
8. Selecione **I accept the terms of this agreement (Aceito os termos deste contrato)** e clique em **Continue (Continuar)**.
9. Selecione o diretório de instalação (este exemplo mantém a configuração padrão, mas você pode especificar um diretório conforme necessário) e clique em **Install Now (Instalar agora)**.
![](https://main.qcloudimg.com/raw/3ea703e1632ec78b3f8f4b961c189208.png)
10. Quando a instalação for concluída, selecione **Run the SharePoint Products Configuration Wizard now (Executar o assistente de configuração de produtos do SharePoint agora)** e clique em **Close (Fechar)**.
![](https://main.qcloudimg.com/raw/368fa9a4cdb3b47a77c554db855737e0.png)

### Etapa 5: configurar o SharePoint 2016

1. Na janela **SharePoint Products Configuration Wizard (Assistente de configuração de produtos do SharePoint)**, clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/73aa25130b0e24e6784760a28d6d8fe2.png)
2. Clique em **Yes (Sim)** na caixa de diálogo pop-up para permitir a reinicialização do serviço durante a configuração.
3. Selecione **Create a new server farm (Criar um novo farm de servidor)** e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/b66da626c4883f2f2fb1b75bce6042f6.png)
4. Na página **Specify Configuration Database Settings (Especificar definições do banco de dados de configuração)**, defina o banco de dados de configuração e a conta de acesso.
O banco de dados do SharePoint está no host local, portanto, você precisa inserir o banco de dados local e a conta. Em seguida, clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/d1ccac780ddb9fb308b071fe385ad3f6.png)
5. Digite a senha do farm de servidor e clique em **Next (Avançar)**.
6. Selecione **Front-end** para "Multiple-Server Farm (Farm de vários servidores)" e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/c23051f73ae543002bc9c15d3d2b3387.png)
7. Especifique o número da porta do SharePoint Central Administration Web Application (este exemplo usa "10000", mas você pode configurar o número conforme necessário) e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/c7622761e6eb45b1935fccc851379b29.png)
8. Confirme as configurações do SharePoint e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/8d97c6aff42bb8b27fb3e108fa3d16d8.png)
9. Depois que a configuração for concluída, clique em **Finish (Concluir)**.

