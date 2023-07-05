Este documento descreve como resolver o problema de **autenticação em nível de rede** ao se conectar a uma instância do Windows usando a Área de Trabalho Remota.

## Problema
A Área de Trabalho Remota do Windows não consegue se conectar à sua instância do Windows com a mensagem de erro **The remote computer requires Network Level Authentication, which your computer does not support. For assistance, contact your system administrator or technical support. (O computador remoto exige a Autenticação no Nível de Rede, que não é suportada pelo seu computador. Para obter assistência, entre em contato com o administrador do sistema ou o suporte técnico.)**
![](https://main.qcloudimg.com/raw/409b3259fa13220e8cde0790aa87488b.jpg)

## Solução de problemas

> Nas etapas a seguir, usamos o Windows Server 2016 como exemplo.
>

### Login no CVM usando o VNC
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, localize a instância do CVM desejada. Clique em **Log In (Fazer login)**, conforme mostrado na figura abaixo:
![CVM index page](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Na janela **Log in to Windows instance (Fazer login na instância do Windows)** exibida, selecione **Alternative login methods (VNC) (Métodos alternativos de login (VNC))**. Clique em **Log In Now (Fazer login agora)** para fazer login no CVM.
4. Na janela de login exibida, selecione **Send Remote Command (Enviar comando remoto)** no canto superior esquerdo. Clique em **Ctrl-Alt-Delete** para acessar a interface de login do sistema, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Modificação do registro do Windows

1. Na interface do sistema operacional, clique em <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>. Digite **regedit** e pressione **Enter** para abrir o Editor do Registro.
2. Usando a árvore de navegação no lado esquerdo, navegue para **Computer (Computador)** > **HKEY_LOCAL_MACHINE** > **SYSTEM (SISTEMA)** > **CurrentControlSet** > **Control (Controle)** > **Lsa**. No painel do lado direito, selecione **Security Packages (Pacotes de segurança)**, conforme mostrado na figura abaixo:
![Security Packages](https://main.qcloudimg.com/raw/db037b5131ff44af72b560fbac4931e1.png)
3. Clique duas vezes em **Security Packages (Pacotes de segurança)** para abrir a caixa de diálogo **Edit Multi-String (Editar Cadeia de Caracteres Múltipla)**.
4. Nessa caixa de diálogo, adicione **tspkg** em **Value Data (Dados de Valor)** e clique em **OK**, conforme mostrado na figura abaixo.
![](https://main.qcloudimg.com/raw/cca2bce345b48569d45fd391ee65bc51.png)
5. Usando a árvore de navegação no lado esquerdo, navegue para **Computer (Computador)** > **HKEY_LOCAL_MACHINE** > **SYSTEM (SISTEMA)** > **CurrentControlSet** > **Control (Controle)** > **SecurityProviders**. No painel do lado direito, selecione **SecurityProviders**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/14e84c77ae1d1d3c5bc2ab091543a957.png)
6. Clique duas vezes em **SecurityProviders** para abrir a caixa de diálogo **Edit Multi-String (Editar Cadeia de Caracteres Múltipla)**.
7. Acrescente `,credssp.dll` ao final do campo **Value Data (Dados de Valor)** na caixa de diálogo **Edit Multi-String (Editar Cadeia de Caracteres Múltipla)**. Clique em **OK** conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/34b98c226c359b070e2f03c2ff1c6e42.png)
8. Feche o editor de registro e reinicie a instância. Agora, você pode fazer login remotamente.

