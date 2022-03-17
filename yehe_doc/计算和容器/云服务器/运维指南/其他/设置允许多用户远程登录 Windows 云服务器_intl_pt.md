## Cenário
Este documento mostra como configurar um login remoto de vários usuários para o CVM do Windows, usando um CVM com Windows Server 2012 R2 como o sistema operacional de exemplo.

## Etapas
### Adição do serviço de área de trabalho remota
1. Faça login no CVM do Windows.
2. Na interface do sistema operacional, clique em <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> para abrir o **Server Manager (Gerenciador do servidor)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/66bb5237846f1dd79e3145bfd82d9257.png)
3. Clique em **Add roles and features (Adicionar funções e funcionalidades)** e a janela **Add Roles and Features Wizard (Assistente para adicionar funções e funcionalidades)** será exibida.
4. Na janela "Add Roles and Features Wizard (Assistente para adicionar funções e funcionalidades)", mantenha os parâmetros padrão para as primeiras três etapas.
5. Na página **Select server roles (Selecionar funções de servidor)**, marque **Remote Desktop Services (Serviços de área de trabalho remota)** e clique em **Next (Avançar)**, conforme mostrado abaixo: 
![](https://main.qcloudimg.com/raw/54d329c2667ac5c60ffdc2b74f1fc555.png)
6. Mantenha os parâmetros padrão e clique em **Next (Avançar)** duas vezes consecutivas.
7. Na interface **Select Role Service (Selecionar serviço de função)**, marque **Remote Desktop Session Host (Host de sessão da área de trabalho remota)**, conforme mostrado abaixo:
A caixa de prompt "Add features that are required for remote desktop session host? (Adicionar funcionalidades necessárias para o host de sessão da área de trabalho remota?)" será exibida.
![](https://main.qcloudimg.com/raw/8d24fd515bd363dc020257c2843c5562.png)
8. Na caixa de prompt "Add features required for remote desktop session host? (Adicionar funcionalidades necessárias para o host de sessão da área de trabalho remota?)", clique em **Add Features (Adicionar funcionalidades)**, conforme mostrado abaixo: 
![](https://main.qcloudimg.com/raw/2a33d896c16b1d98012536cdc3776248.png)
9. Na página **Select Role Service (Selecionar serviço de função)**, marque **Remote Desktop Licensing (Licenciamento da área de trabalho remota)**, conforme mostrado abaixo:
A caixa de prompt "Add features that required for Remote Desktop Licensing? (Adicionar funcionalidades necessárias para o licenciamento da área de trabalho remoto)" será exibida.
![](https://main.qcloudimg.com/raw/1c908dc77f50488387a2fdbfda08ba35.png)
10. Na caixa de prompt "Add features that required for Remote Desktop Licensing? (Adicionar funcionalidades necessárias para o licenciamento da área de trabalho remoto)", clique em **Add Features (Adicionar funcionalidades)**.
![](https://main.qcloudimg.com/raw/d7aa066366b168ac8a7475155d34ea19.png)
11. Clique em **Next (Avançar)**.
12. Marque **Restart the destination server automatically if required (Reinicie o servidor de destino automaticamente se necessário)** e clique em **Yes (Sim)** na caixa de prompt exibida, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/df280b0a66470be404f114bd17c47d21.png)
13. Clique em **Install (Instalar)** e aguarde a conclusão da instalação do serviço de área de trabalho remota.

### Configuração do login remoto de vários usuários na instância
1. Use o VNC para fazer login no CVM do Windows.
2. Na interface do sistema operacional, clique em <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> para abrir a janela Windows PowerShell.
3. Na janela Windows PowerShell, digite **gpedit.msc** e pressione **Enter** para abrir o **Local Group Policy Editor (Editor de política de grupo local)**.
4. Na árvore de navegação à esquerda, selecione **Computer Configuration (Configuração do computador)** > **Administrative Templates (Modelos administrativos)** > **Windows Components (Componentes do Windows)** > **Remote Desktop Services (Serviços de área de trabalho remota)** > **Remote Desktop Session Host (Host de sessão da área de trabalho remota)** > **Connections (Conexões)** e clique duas vezes em **Limit number of connections (Limitar a quantidade de conexões)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/e0420d2bb8ddd3e1524ee688173cb9d1.png)
5. Na janela **Limit number of connections (Limitar a quantidade de conexões)** exibida, selecione **Enabled (Ativado)** e insira a quantidade máxima de usuários remotos simultâneos em **RD Maximum Connections allowed (Conexões máximas de área de trabalho remota permitidas)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/066c9dfb06dc4c092424c4e1142f7471.png)
6. Clique em **OK**.
4. Na árvore de navegação à esquerda, selecione **Computer Configuration (Configuração do computador)** > **Administrative Templates (Modelos administrativos)** > **Windows Components (Componentes do Windows)** > **Remote Desktop Services (Serviços de área de trabalho remota)** > **Remote Desktop Session Host (Host de sessão da área de trabalho remota)** > **Connections (Conexões)** e clique duas vezes em **Restrict Remote Desktop Services users to a single Remote Desktop Services session (Restringir os usuários dos serviços de área de trabalho remota a uma única sessão de serviços de área de trabalho remota)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/1183e9f4c6c08b6f99746db42b0d183e.png)
8. Na janela "Restrict Remote Desktop Services users to a single Remote Desktop Services session (Restringir os usuários dos serviços de área de trabalho remota a uma única sessão de serviços de área de trabalho remota)" exibida, selecione **Disabled (Desativado)** e clique em **OK**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/56d910ea359024d34dc05de3a274c91a.png)
9. Feche o editor de política de grupo local.
10. Reinicie a instância.



