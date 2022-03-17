## Introdução
Descrição sobre como usar o IIS para construir um site FTP em uma instância do Tencent Cloud Virtual Machine (CVM) que executa o Windows.

## Requisitos de software
Os seguintes softwares são necessários para construir o serviço FTP:
 - OS: Windows Server 2012 
 - Servidor da web: IIS 8.5

## Instruções
### Etapa 1: fazer login no CVM
- [Faça login em um CVM Windows usando um arquivo RDP (recomendado)](http://intl.cloud.tencent.com/document/product/213/5435).
- [Faça login em um CVM Windows usando uma área de trabalho remota](https://intl.cloud.tencent.com/document/product/213/32498).

### Etapa 2: instalar o serviço FTP no IIS
1. Clique em <img src="https://main.qcloudimg.com/raw/446c1e8cb7da2ce280d710c6a46b693d.png" style="margin:-3px 0px"> para abrir o gerenciador do servidor. A janela **Server Manager (Gerenciador do servidor)** é exibida.
2. Clique em **Add Roles and Features (Adicionar funções e recursos)**, conforme mostrado na figura abaixo. A janela **Guide to Adding Roles and Features (Guia para adicionar funções e recursos)** é exibida.
![](https://main.qcloudimg.com/raw/1d941b3c877a420513e494971a834f37.png)
3. Clique em **Next (Avançar)**. A página **Choose Installation Type (Selecionar tipo de instalação)** é exibida.
4. Selecione **Role-based or Feature-based Installation (Instalação baseada em funções ou recursos)** e clique em **Next (Avançar)**. A página **Choose Target Server (Selecionar servidor de destino)** é exibida.
5. Mantenha as configurações padrão e clique em **Next (Avançar)**, conforme mostrado na figura abaixo. A página **Choose Server Role (Selecionar função do servidor)** é exibida.
![](https://main.qcloudimg.com/raw/41f775ccbcd8e984b72bc096efa668d4.png)
6. Selecione **Web Server (IIS) (Servidor web (IIS))** e clique em **Add Feature (Adicionar recurso)** na janela exibida, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/f23fe1b8415c0f75c54309b652781aa4.png)
7. Clique em **Next (Avançar)** três vezes. A página **Choose Role Service (Selecionar serviço de função)** é exibida.
8. Selecione **FTP Service (Serviço FTP)** e **FTP Extension (Extensão FTP)** e clique em **Next (Avançar)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/1fa84c69d96c16f2ea0f10e51b0607bb.png)
9. Clique em **Install (Instalar)** para iniciar a instalação do serviço FTP.
10. Após a conclusão da instalação, clique em **Close (Fechar)**.
<span id="user"></span>
### Etapa 3: criar um nome de usuário e senha de FTP
> As etapas a seguir criam uma conta FTP com autenticação de senha. Se você planeja usar apenas acesso anônimo, pule esta seção.
>
1. Na janela "Server Manager (Gerenciador do servidor)", selecione **Tools (Ferramentas)** -> **My Computer (Meu computador)** na barra de navegação no canto superior direito. A janela **My Computer (Meu computador)** é exibida.
2. Selecione **System Tools (Ferramentas do sistema)** -> **Local Users and Groups (Usuários e grupos locais)** -> **Users (Usuários)** na barra lateral à esquerda.
3. No lado direito da interface de **Users (Usuários)**, clique com o botão direito do mouse em um local vazio e selecione **New User (Novo usuário)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/60bad9ff725b8fe4386c2eed9c5ff63a.png)
4. Na interface "New User (Novo usuário)", defina o nome de usuário e a senha de acordo com as instruções a seguir. Clique em **Create (Criar)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/1bc9cb2c2000361f6699c155e25d7630.png)
Os principais parâmetros são os seguintes:
  - User name (Nome do usuário): nome do usuário. Neste caso, `ftpuser`.
  - Password and Confirm password (Senha e confirmar senha): a senha deve conter letras maiúsculas, minúsculas e números. Neste caso, `tf7295TFY`.
  - Desmarque **User must change password in next login (O usuário deve alterar a senha no próximo login)** e selecione **Password never expires (A senha nunca expira)**.
  Selecione as opções conforme achar adequado. Para este artigo, selecionamos **Password never expires (A senha nunca expira)**.
5. Clique em **Close (Fechar)** para fechar a janela "New User (Novo usuário)". É possível ver o usuário recém-criado `ftpuser` na lista.
	
### Etapa 4: definir permissões de pasta compartilhada
> Neste artigo, usamos `C:\test` como a pasta compartilhada. Ele contém um arquivo chamado `test.txt`. Crie uma pasta chamada `test` em `C:\` e um arquivo chamado `test.txt` em `C:\test`. Você também pode usar qualquer outra pasta e arquivo.
>
1. Clique em <img src="https://main.qcloudimg.com/raw/863967bab67b6cd83ce5f0924e1b19c8.png" style="margin:-3px 0px"> para abrir **This Computer (Este computador)**.
2. Expanda os diretórios na unidade C. Selecione e clique com o botão direito do mouse em `test`. Selecione **Properties (Propriedades)**.
3. Na janela **Properties (Propriedades)**, selecione a guia **Security (Segurança)**.
4. Selecione `Everyone` (Todos) e clique em **Edit (Editar)**, conforme mostrado na figura abaixo:
Se "Group or User Name (Nome do grupo ou do usuário)" não contiver `Everyone` (Todos), consulte [Adicionar todos](#add) para adicionar o usuário.
![](https://main.qcloudimg.com/raw/aec3d0557deef26ca3ff8005da86603f.png)
5. <span id="step5"></span>Na interface **Permissions (Permissões)**, defina as permissões para `Everyone` (Todos) e clique em **OK**, conforme mostrado na figura abaixo:
Neste artigo, concedemos a `Everyone` (Todos) todas as permissões.
![](https://main.qcloudimg.com/raw/ccdfda072d8a476a08773b7fcf979ec7.png)
6. Na janela **Properties (Propriedades)**, clique em **OK** para concluir as configurações.


### Etapa 5: adicionar um site FTP
1. Na janela "Server Manager (Gerenciador do servidor)", selecione **Tools (Ferramentas)** -> **Internet Information Services (IIS) Manager (Gerenciador de Serviços de Informações da Internet (IIS))** na barra de navegação no canto superior direito.
2. Na janela **Internet Information Services (IIS) Manager (Gerenciador de Serviços de Informações da Internet (IIS))**, expanda seu servidor na barra lateral esquerda, clique com o botão direito do mouse em **Website** e selecione **Add FTP Site (Adicionar site FTP)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/3d2c1a2708939cd5a8d7bf3bdf9aa1ff.png)
3. Na interface "Site Information (Informações do site)", insira as seguintes informações. Clique em **Next (Avançar)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/76761e667657b80bfdd2d2403d64ba3c.png)
    - **FTP site name (Nome do site FTP)**: nome do seu site FTP. Neste artigo, é usado `ftp`.
    - **Physical path (Caminho físico)**: caminho da pasta compartilhada. Certifique-se de definir as permissões apropriadas. Neste artigo, é usado `C:\test`.
4. Na interface **Binding and SSL Settings (Configurações de vinculação e SSL)**, insira as seguintes informações. Clique em **Next (Avançar)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/355c3de0e19d7e1c161c51156bf0965f.png) 
A seguir está uma lista de parâmetros:
     - **Binding (Vinculação)**: a opção padrão para endereços IP é **None assigned (Nenhum atribuído)**; e a porta padrão é a porta 21, o número da porta FTP padrão. É possível escolher seu próprio número de porta.
     - **SSL**: selecione uma opção. Neste artigo, **No SSL (Nenhum SSL)** é selecionado.
       - **No SSL (Nenhum SSL)**: não oferece suporte a conexões SSL.
       - **Allow SSL (Permitir SSL)**: permite que o servidor FTP se conecte a clientes com ou sem SSL.
      - **Require SSL (Requer SSL)**: A criptografia SSL é necessária para a comunicação entre o servidor FTP e os clientes.
   Se você escolher **Allow SSL (Permitir SSL)** ou **Require SSL (Requer SSL)**, pode selecionar um certificado SSL existente em "SSL Certificates (Certificados SSL)" ou consultar [criar um certificado de servidor](#ssl) para criar um certificado SSL.
5. Na interface "Identity Authentication and Authorization Information (Autenticação de identidade e informações de autorização)", insira as seguintes informações. Clique em **Next (Avançar)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/0f3be2c7ba449240cdac3f3c767e668c.png)
 - **Identity authentication (Autenticação de identidade)**: selecione um método de autenticação de identidade. Neste artigo, é usado **Basic (Básico)**.
    - *Anonymous (Anônimo)**: permite que os usuários acessem o conteúdo sem autenticação.
	 -. **Basic (Básico)**: exige que os usuários forneçam nomes de usuário e senhas válidos antes de permitir o acesso ao conteúdo. Nesse modo, as senhas são transferidas sem criptografia. Portanto, selecione este modo de autenticação apenas quando souber que a conexão entre os clientes e o servidor FTP é segura (por exemplo, usando SSL).
 - **Authorize (Autorizar)**: escolha uma opção na lista suspensa de permissões de acesso. Neste artigo, é usada `ftpuser`.
	    - **All users (Todos os usuários)**: todos os usuários, anônimos ou identificados, podem acessar o conteúdo.
	    - **Anonymous users (Usuários anônimos)**: usuários anônimos podem acessar o conteúdo.
	    - **Specified role or user group (Função ou grupo de usuários especificado)**: apenas as funções ou membros especificados dos grupos especificados podem acessar o conteúdo. Se você escolher esta opção, precisará especificar as funções ou grupos de usuários.
	    - **Specified user (Usuário especificado)**: apenas o usuário especificado pode acessar o conteúdo. Se você escolher esta opção, precisará especificar o nome de usuário.
 - **Permissions (Permissões)**: permissões para o conteúdo compartilhado. Neste artigo, **Read (Ler)** e **Write (Gravar)** são selecionados.
    - **Read (Ler)**: permite que usuários autorizados leiam o conteúdo compartilhado.
    - **Write (Gravar)**: permite que usuários autorizados gravem no diretório.
7. Clique em **Complete (Concluir)**.

### Etapa 6: configurar grupo de segurança e firewall
1. Depois que o site FTP for criado, adicione uma regra de entrada que permita o tráfego para a porta FTP, que é a 21 para os fins deste artigo. Para obter mais informações, consulte [Adicionar regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).
Se você selecionou outras portas, também precisa adicionar uma regra de entrada para cada porta selecionada.
2. (Opcional) Consulte a [documentação oficial da Microsoft](https://docs.microsoft.com/en-us/previous-versions/orphan-topics/ws.11/hh831655(v=ws.11)) sobre como configurar o firewall para que o servidor FTP seja capaz de aceitar conexões passivas do firewall.

### Etapa 7: testar o site FTP
É possível usar um cliente FTP, navegador ou gerenciador de arquivos para se conectar ao servidor FTP. Para os fins deste artigo, é utilizado o gerenciador de arquivos.
1. Configure o Internet Explorer
 - Se você adicionou as regras de firewall apropriadas, abra uma janela do Internet Explorer e selecione **Tools (Ferramentas)** -> **Internet Options (Opções da Internet)** -> **Advanced (Avançado)**. Desmarque **Use Passive FTP (used for compatibility between the firewall and DSL modem) (Usar FTP passivo (usado para compatibilidade entre o firewall e o modem DSL))** e clique em **OK**.
 - Se você não adicionou as regras de firewall adequadas:
    1. Abra uma janela do Internet Explorer no **the FTP server (servidor FTP)** e selecione **Tools (Ferramentas)** -> **Internet Options (Opções da Internet)** -> **Advanced (Avançado)**.  Desmarque **Use Passive FTP (used for compatibility between the firewall and DSL modem) (Usar FTP passivo (usado para compatibilidade entre o firewall e o modem DSL))** e clique em **OK**.
    2. Abra uma janela do Internet Explorer no **client (cliente)** e selecione **Tools (Ferramentas)** -> **Internet Options (Opções da Internet)** -> **Advanced (Avançado)**. Desmarque **Use Passive FTP (used for compatibility between the firewall and DSL modem) (Usar FTP passivo (usado para compatibilidade entre o firewall e o modem DSL))** e clique em **OK**.
2. Abra o gerenciador de arquivos em seu PC, digite o seguinte endereço na caixa de endereço do navegador e pressione **Enter**, conforme mostrado na figura a seguir.
```
ftp://CVM_public_IP_address:21
```
![](https://main.qcloudimg.com/raw/d3d5a93170bb990f47ecd9f24c3e89ab.png)
3. A caixa de diálogo **Login Identity (Identidade de login)** é exibida. Digite o nome de usuário e a senha configurados em [Criação do nome de usuário e senha de FTP](#user).
Neste artigo, o nome de usuário é `ftpuser` e a senha é `tf7295TFY`.
4. Faça upload e download de arquivos após o login.

## Apêndice
<span id="add"></span>
### Adicionar todos
1. Na janela **Properties (Propriedades)**, selecione a guia **Security (Segurança)**. Clique em **Edit (Editar)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/f3f056e833fc63c97f23eef646ea8a10.png)
2. Na caixa de diálogo **Properties (Propriedades)**, clique em **Add (Adicionar)**.
3. Na caixa de diálogo "Choose User or Group (Selecionar usuário ou grupo)", clique em **Advanced (Avançado)**.
4. Na caixa de diálogo "Choose User or Group (Escolher usuário ou grupo)" exibida, clique em **Search Now (Pesquisar agora)**.
5. No resultado da pesquisa, selecione `Everyone` (Todos) e clique em **OK**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/32a9d44822ed4db0e82167d0cfb94835.png)
6. Na caixa de diálogo "Choose User or Group (Escolher usuário ou grupo)", clique em **OK**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/1245acedba4be051cf234423460a4345.png)
Vá para a [Etapa 5](#step5) para definir as permissões do usuário `Everyone` (Todos).
<span id="ssl"></span>
### Criação de um certificado de servidor
1. Abra "Server Manager (Gerenciador do servidor)" e selecione **Tools (Ferramentas)** -> **Internet Information Services (IIS) Manager (Gerenciador dos Serviços de Informações da Internet (IIS))** na barra de navegação no canto superior direito.
2. A janela **Internet Information Services (IIS) Manager (Gerenciador dos Serviços de Informações da Internet (IIS))** é exibida. Selecione o servidor na barra lateral esquerda e clique duas vezes em **Server Certificates (Certificados do servidor)** na interface à direita, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/8fc9f67a26475b891f4c50d9c670c08c.png)
3. Selecione **Create Self-Signature Certificate (Criar certificado de auto-assinatura)** na coluna de operação correta.
4. A janela **Create Self-Signature Certificate (Criar certificado de auto-assinatura)** é exibida, insira um nome de certificado e a classe de armazenamento, conforme mostrado na figura abaixo:
Neste documento, um certificado SSL para armazenamento pessoal é criado.
![](https://main.qcloudimg.com/raw/0db81917b5b1e20af19d4d687d0d7fda.png)
5. Clique em **OK**.
