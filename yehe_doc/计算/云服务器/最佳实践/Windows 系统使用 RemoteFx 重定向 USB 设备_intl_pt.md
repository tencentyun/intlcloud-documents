## Cenário

O RemoteFx é uma versão atualizada do Windows Remote Desktop Protocol (RDP). A partir do RDP 8.0, o RemoteFx pode ser usado para redirecionar dispositivos USB locais para uma área de trabalho remota por meio do canal de dados RDP, garantindo que o CVM possa usar esses dispositivos USB.

Este documento usa as seguintes versões de ambiente como exemplos para descrever como habilitar o recurso de redirecionamento RemoteFx USB do RDP para redirecionar dispositivos USB para um CVM.
- Cliente: Windows 10
- Servidor: Windows Server 2016

## Limites de uso

Como o RDP 8.0 e versões posteriores oferecem suporte ao recurso de redirecionamento RemoteFx USB, o Windows 8, Windows 10, Windows Server 2016 e Windows Server 2019 oferecem suporte a esse recurso. Se o sistema operacional do seu PC local tiver uma dessas versões, você não precisa instalar o patch de atualização RDP 8.0. Se o seu PC local tiver Windows 7 ou Windows Vista, acesse [site oficial da Microsoft](https://support.microsoft.com/en-us) para obter e instalar o patch de atualização do RDP 8.0.


## Instruções

### Configuração do servidor

1. [Fazer login em uma instância do Windows usando o arquivo RDP (recomendado)](https://intl.cloud.tencent.com/document/product/213/5435).
2. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/ab9a3a22baf69f63a90a43476f12db94.png" style="margin: 0;"></img> e selecione **Server Manager (Gerenciador do servidor)** para abrir o Gerenciador do servidor.
3. Na janela "Server Manager (Gerenciador do servidor)", clique em **Add roles and features (Adicionar funções e recursos)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/4ee64b60cf2993013698c2f641ea8dc1.png)
4. Na janela pop-up "Add Roles and Features Wizard (Assistente para adicionar funções e recursos)", clique em **Next (Avançar)** para ir para a página "Select installation type (Selecionar tipo de instalação)".
5. Na página "Select installation type (Selecionar tipo de instalação)", selecione **Role-based or feature-based installation (Instalação baseada em funções ou recursos)** e clique em **Next (Avançar)**.
6. Na página "Select destination server (Selecionar servidor de destino)", mantenha as configurações padrão e clique em **Next (Avançar)**.
7. Na página "Select server roles (Selecionar funções de servidor)", selecione **Remote Desktop Services (Serviços de área de trabalho remota)** e clique em **Next (Avançar)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/76481a67eb8aa5b98e2e8a8de5895263.png)
8. Mantenha as configurações padrão e clique em **Next (Avançar)** por 2 vezes.
9. Na página "Select role services (Selecionar serviços de função)", selecione **Remote Desktop Session Host (Host de sessão de área de trabalho remota)**, **Remote Desktop Connection Broker (Agente de conexão de área de trabalho remota)** e **Remote Desktop Licensing (Licenciamento de área de trabalho remota)**. Na janela pop-up, clique em **Add Features (Adicionar recursos)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/38d46bf2c391f82684c5c82c439df3ec.png)
10. Clique em **Next (Avançar)**.
11. Clique em **Install (Instalar)**.
12. Após a instalação ser concluída, reinicie o CVM.
13. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, digite **gpedit.msc** e pressione Enter para abrir o "Local Group Polzhicy (Editor de política de grupo local)".
14. Na árvore de navegação à esquerda, escolha **Computer Configuration (Configuração do computador)** > **Administrative Templates (Modelos administrativos)** > **Windows Components (Componentes do Windows)** > **Remote Desktop Services (Serviços de área de trabalho remota)** > **Remote Desktop Session Host (Host de sessão de área de trabalho remota)** > **Device and Resource Redirection (Redirecionamento de dispositivo e recurso)** e clique duas vezes em **Do not allow supported Plug and Play device redirection (Não permitir redirecionamento de dispositivo Plug and Play compatível)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/9d62d199cb34482f6c80f3dddb47bb0e.png)
15. Na janela pop-up, selecione **Disabled (Desativado)** e clique em **OK**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/a76cf6ec239df644f6905eca7de3a2bd.png)
16. Reinicie o CVM.


### Configuração do cliente

1. No PC local, clique com o botão direito do mouse em <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> e selecione **Run (Executar)** para abrir a caixa de diálogo "Run (Executar)", conforme mostrado na figura a seguir:
2. Na caixa de diálogo "Run (Executar)", digite **gpedit.msc** e clique em **OK** para abrir o "Local Group Policy Editor (Editor de política de grupo local)".
3. Na árvore de navegação à esquerda, escolha **Computer Configuration (Configuração do computador)** > **Administrative Templates (Modelos administrativos)** > **Windows Components (Componentes do Windows)** > **Remote Desktop Services (Serviços de área de trabalho remota)** > **Remote Desktop Connection Client (Cliente de conexão de área de trabalho remota)** > **RemoteFX USB Redirection (Redirecionamento RemoteFx USB)** e clique duas vezes em **Allow RDP redirection of other supported RemoteFX USB devices (Permitir redirecionamento de RDP de outros dispositivos compatíveis com RemoteFx USB)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/e65d8e43fcf5531c701d08e257daa20f.png)
4. Na janela pop-up, selecione **Enabled (Ativado)** e defina a permissão de acesso de redirecionamento RemoteFx USB para **Administrators and Users (Administradores e usuários)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/8fc197ed25e82d2f85ad32144b197a06.png)
5. Clique em **OK**.
6. Reinicie o PC local.

### Verificação do resultado da configuração

1. Em seu PC local, insira um dispositivo USB, clique com o botão direito do mouse em <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> e escolha **Run (Executar)** para abrir a caixa de diálogo "Run (Executar)".
2. Na caixa de diálogo "Run (Executar)", digite **mstsc** e pressione Enter para abrir a caixa de diálogo de conexão de área de trabalho remota, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/5478a5d46f6825cdfe604600a1391f4d.png)
3. Digite o endereço IP público do servidor Windows em **Computer (Computador)** e clique em **Options (Opções)**.
4. Na página da guia **Local Resources (Recursos locais)**, clique em **More (Mais)** em "Local devices and resouces (Dispositivos e recursos locais)", conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/f9c676bba12a01e029d727d9771faa38.png)
5. Na janela pop-up, expanda **Other supported RemoteFx USB devices (Outros dispositivos compatíveis com RemoteFx USB)**, selecione o dispositivo USB inserido e clique em **OK**.
![](https://main.qcloudimg.com/raw/681b010102c112bd99309c2c325d53c2.png)
6. Clique em **Connect (Conectar)**.
7. Na janela pop-up **Windows Security (Segurança do Windows)**, insira a conta de administrador e a senha da instância, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/f87c5e1240ce07fe0ac28b48d88e61fd.png)
8. Clique em **OK** para fazer login na instância do Windows.
Se <img src="https://main.qcloudimg.com/raw/73fe2b3cfa740517e44e4596a222840a.png" style="margin: 0;"></img> aparecer na página de operação da instância do Windows, a configuração foi bem-sucedida.
![](https://main.qcloudimg.com/raw/af5b70150d4032a29e1ded2db75858b6.png)


## Operações relevantes

O RDP do Windows fornece conexão otimizada para dispositivos USB padrão. Dispositivos como drivers e câmeras podem ser mapeados diretamente sem habilitar o recurso RemoteFx. O recurso de redirecionamento RemoteFX USB é necessário para dispositivos USB menos usados. A tabela a seguir lista os métodos de redirecionamento para esses dispositivos USB.
![](https://main.qcloudimg.com/raw/715de06c08753eefe6e4ff5cc3bca270.png)

